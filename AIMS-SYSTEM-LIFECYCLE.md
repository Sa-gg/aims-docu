# AIMS — System Documentation

> **Audience:** Project manager / school stakeholders. **Purpose:** one readable reference for what AIMS does, how each feature works, and its lifecycle.
> **Product name:** AIMS — Automated Intervention and Mastery System. An LMS for Philippine high schools.

---

## 1. What AIMS Is

AIMS is the **classroom layer** of the school's systems. It does not replace the school's enrollment, scheduling, or official grading systems — it connects to them and runs teaching, assessment, and **intervention** on top.

| AIMS is | AIMS is not |
|---|---|
| Assignments, quizzes, grading, remediation, mastery | The enrollment register (that's **EnrollPro**) |
| Auto-built classes from official data | The class scheduler (that's **ATLAS**) |
| The activity record + intervention trail | The official quarterly grade of record (that's **SMART**) |

**The problem it solves:** teachers spend time encoding classes, writing quizzes, computing scores, and manually chasing failing students. AIMS automates those four things and makes sure no failing student is forgotten.

---

## 2. Architecture at a Glance

```
EnrollPro (students, sections, school years)  ──►  AIMS  ◄──  ATLAS (teaching load, schedule)
SMART (DepEd grading weights)                 ──►  AIMS  ──►  SMART (public scores API)
```

- **AIMS** — courses, content, quizzes, submissions, gradebook, intervention (hosted on the school's Tailscale tailnet).
- **EnrollPro (EP)** — the source of truth for **who** is in which section, every school year.
- **ATLAS** — the source of truth for **what a teacher teaches** (load) and the **timetable**.
- **SMART** — the source of truth for **grading weights** (WW/PT/QA); it pulls graded scores back from AIMS.
- **Term events** — EnrollPro owns the school calendar and broadcasts a `TERM_CHANGED` event over a RabbitMQ fanout (hosted on AIMS). AIMS applies the rollover and updates its UI live; it never republishes.

**Roles:** `TEACHER`, `STUDENT`, `ADMIN`. Every record is scoped to a **school** (tenant isolation); users never see another school's data.

---

## 3. Core Concepts (short glossary)

| Concept | Meaning |
|---|---|
| **Course** | One class + one subject (`EP-{sectionId}-{subject}`, e.g. `EP-81-AP` = Grade 7 Luna, Araling Panlipunan). Exactly one teacher. |
| **Topic / Module** | A folder inside a course. Classwork items live in topics ("Term 1", "Module 2:", …). |
| **Classwork item** | A **material** (learning resource), **task** (submission work), or **quiz** (assessment). |
| **Enrollment** | A student ↔ course link, with status (active / removed) + intervention flags. |
| **Submission** | A student's attempt at a quiz or task, with answers and a score. |
| **Grading weight** | The DepEd category a score belongs to: **WW** (Written Work), **PT** (Performance Task), **QA** (Quarterly Assessment). |
| **Mastery gate** | A quiz that locks materials/quizzes until the student submits (or passes) it. |
| **Remedial quiz** | An AI-generated, per-student follow-up quiz built from that student's wrong answers. |
| **Remedial kit** | Auto-written study material (summary + links + attachments) that comes with a remedial quiz. |

---

## 4. Feature Catalogue (how each works + lifecycle)

### 4.1 Accounts & automatic class setup

| Feature | How it works | Lifecycle |
|---|---|---|
| **Login** | Students log in with **LRN + password**; teachers/admins with employee account; Google SSO also supported. Accounts are verified against EnrollPro. | Login → EP verification → local account created/refreshed → post-login sync |
| **Teacher class sync** | On login, AIMS asks ATLAS for the teacher's **annual teaching load** and creates/updates their courses; EP supplies the section rosters. | Login → load check (`EMPTY`/`POPULATED`) → create/update courses → enroll students → archive removed |
| **Student section sync** | On login (and from Home), the student's active section is resolved; AIMS enrols them into that section's courses. | Login → resolve section via EP (falls back to AIMS history when EP is unreachable) → enroll → stale classes archived |
| **School-wide bulk sync** | Admin/background job re-syncs all sections + teachers, and self-heals stale rows. | Scheduled every 30 min (or admin-triggered) → sections → rosters → archives → SSE refresh |
| **Year rollover** | New school year → old courses are **archived** (not deleted) with the year they belonged to; new courses are created. | EP rolls year → term/bulk sync → archive old-year courses + ghost enrollments → archive history view |
| **Rotating subjects** | Subjects like Science (Bio → Chem → ES per term) are stored individually and only the active term's subject is shown; others sit in **Hidden Classes**. | ATLAS rank data stored on the course → active term changes → visible subject auto-swaps |
| **Homeroom Guidance** | HG courses are auto-materialized per year and auto-hidden (advisory), never auto-archived mid-year. | Section sync → HG ensured → shown in Hidden Classes |
| **Archived classes** | Archived courses remain viewable read-only for teacher and student. | Rollover/reset → archive → `/archived` page |

### 4.2 Classwork & content

| Feature | How it works | Lifecycle |
|---|---|---|
| **Materials** | Teacher attaches files (upload or **Google Drive**), links, or YouTube. Students open/download; offline copies can be saved. | Create → (draft) → post/schedule → student views → tracked as viewed |
| **Tasks** | Submission-based work with instructions, points, due date, optional rubric and attachments. | Create → post/schedule → student submits (file/text) → teacher grades → returned |
| **Quizzes** | Built in the Quiz Builder (below); delivered online with auto/manual grading. | Build → publish/schedule → student takes → graded → returned |
| **Topics & ordering** | Items are drag-and-drop reorderable **within and across topics** (desktop and long-press on touch). New items are added on top. | Topic created → item created (prepends) → drag/move → order persisted |
| **Scheduling** | Materials/quizzes/tasks can be scheduled; the system sends a **heads-up notification** shortly before go-live, then publishes automatically. | Set schedule → upcoming notice → publish → students notified |
| **Announcements** | Teacher posts announcements (draft/schedule/attachments). Students can **comment** and **acknowledge**; teachers see who acknowledged (count + names). | Post → students view (viewed = cleared from dashboard) → comment/acknowledge → teacher sees receipt |
| **Live updates (SSE)** | Edits (new items, grades, locks, announcements) stream to open pages instantly — no refresh. | Any teacher action → `course-update` event → student/teacher views refresh silently |
| **File reuse** | "From my files" attaches a previously uploaded file to any class without re-uploading. | Pick existing file → metadata copy → deleted only when no longer referenced |

### 4.3 Quiz Builder & AI

| Feature | How it works | Lifecycle |
|---|---|---|
| **Question types** | Multiple choice, true/false, identification, enumeration, short answer, paragraph (+ instruction/section blocks that are display-only). | Add/edit → reorder → save (reconciles by id) |
| **Points modes** | **Reflect** (sum of question points), **Pts** (teacher's total, e.g. /100 for hybrid/printed), **Ungraded** (excluded from grades). | Set in the Points card → used by every display + gradebook |
| **Time limit** | Optional minutes-per-quiz; countdown on the student page, auto-submit at deadline, late flag server-side. | Configure → student sees timer → auto-submit/late marking |
| **Grading mode** | **Automatic** (objective scores instantly) or **Manual** (teacher confirms/finalises). | Submit → auto-score → (manual: review queue) → return |
| **AI generate** | Generates questions from **an attached file** *or* **a typed prompt only**; teacher reviews/edits everything. | Teacher asks → AI cascade generates → draft questions → teacher validates → publish |
| **AI variations** | Produces a different version of the same quiz to deter answer-sharing between students. | Open quiz → "Make a different version" → new question set |
| **Import & reuse** | Import questions from a file (DOCX/PDF/PPT) or reuse an existing quiz across sections/classes. | Import → mapping/preview → questions added |
| **Shared quizzes** | One quiz, many classes: a master quiz + per-class settings (points, weight, due, locks, targeting). | Create → assign to classes → each class gets its own responses/scores; teacher sees the union |
| **Export** | DOCX, PPTX, printable paper, and present mode; optional answer key. | Export tab → preview → download/print/present |
| **Item Analysis** | After attempts exist: per-question difficulty, option/distractor distribution, common-distractor notes, score distribution. | Students submit → analysis fills in per question |

### 4.4 Taking an assessment (student)

| Feature | How it works | Lifecycle |
|---|---|---|
| **Online quiz** | Start → answer → submit; objective answers graded instantly, written answers queue for the teacher. | Start → in progress → submit → graded/pending |
| **Deadlines & reopen** | Due date (optionally hard-close). Teachers can reopen or extend; students are notified with old → new dates. | Deadline passes → closed (or late accepted) → reopened/extended → notice |
| **One-attempt remedial** | A student may take only **one** remedial per failed quiz. | Fail → remedial assigned → one attempt → done |
| **Offline mode (PWA)** | The app installs like a native app; quizzes and task submissions can be done **offline**, stored on the device, and synced when back online. | Install → go offline → take/submit → pending sync → auto-sync |
| **Results** | Score shown as earned/total, pass/fail vs threshold; pending written answers shown as "Pending review", never as wrong. | Submit → result card → after grading, final score |

### 4.5 Grading & gradebook

| Feature | How it works | Lifecycle |
|---|---|---|
| **Auto-scoring** | Objective questions are checked against the key immediately; written answers wait for the teacher. | Submit → scored → pending count shown to teacher |
| **Manual grading** | Teacher grades answers inline, per student or in bulk; every change is logged. | Open submission → grade → save → optionally return |
| **Gradebook** | All assessments normalized into **WW / PT / QA** averages + a weighted standing, with weights from **SMART** (or DepEd defaults). | Grades exist → category averages → weighted standing |
| **Direct & bulk grading** | Teachers can grade students who never took an item; bulk actions for MISSING/EXCUSED. | Select students → apply score/status |
| **Grade history & rollback** | Every score change records who/when/why; any earlier score can be restored. | Change → history entry → restore → new history entry |
| **Remedial blending** | Failed + remedial scores can be combined: Highest (default), Average, Original, Remedial, or Custom weights. | Remedial exists → rule applied → blended final |
| **Return flow** | Scores become visible to students only when **returned**; re-grading sends it back to draft for a new return. | Grade (draft) → return → student sees; edit again → draft → return |
| **SMART-owned official grade** | AIMS shows activity scores — the weighted quarterly grade of record belongs to SMART (AIMS feeds it via API). | AIMS scores → SMART pull → official grade |

### 4.6 Mastery & locks

| Feature | How it works | Lifecycle |
|---|---|---|
| **Prerequisite quizzes** | A material/quiz can require other quizzes; the student is released by **submitting** each (score ignored) — or, with the strict option, only by **passing**. | Teacher configures on the item → student locked → submits/passes → unlock |
| **Gate tree ("Lock items until this quiz is submitted")** | A quiz can lock chosen items/topics; optionally require the **remedial** to unlock. | Quiz published → locked items shown with 🔒 → submit (or pass/remedial) → unlock |
| **Gate expiry** | A closed/draft/archived gate stops blocking, so students can never be trapped permanently. | Gate closes → dependent items auto-unlock |
| **Manual unlock** | Teacher can permanently unlock a student or a whole roster from the lock modal. | Teacher unlocks → student released (auditable) |
| **Unlock paths** | Submit the gate · pass the gate · complete the remedial · teacher override. | Any path → item accessible |

### 4.7 Interventions & remediation (the flagship)

| Feature | How it works | Lifecycle |
|---|---|---|
| **Intervention roster** | Teacher marks a student for **monitoring** (global `/interventions` + course tab). | Add → monitored → remove |
| **Recommended list** | Students who failed at least one quiz are surfaced automatically — even if never added to the roster. | Fail → appears in recommendations → one-click add |
| **Auto-remediation toggle** | Per student. On = a remedial is generated on failure; off = monitor-only. | Roster add defaults it on |
| **Auto-remedial generation** | On a failing submit, AIMS collects the **exact wrong answers** and asks AI to write a **new remedial quiz** + **study kit**. | Fail → wrong answers analysed → DRAFT remedial + kit → teacher notified |
| **Teacher review** | The teacher sees what the student got wrong, edits/regenerates the kit, then **assigns** it (publishes). | DRAFT → review → Assign → PUBLISHED |
| **Student remedial** | Student studies the kit, takes the one remedial attempt. | Assigned → kit + quiz → one attempt → submitted |
| **Mastery release** | Submitting the remedial clears the mastery gate **regardless of score** (the effort closes the loop). | Submit remedial → gate cleared |
| **Failure recovery** | If AI generation fails (e.g. model overload), the teacher's notification has a **retry** action; the intervention modal shows **Generate** for any failed quiz with no remedial. | Failure → retry/Generate → remedial created |

### 4.8 Notifications & dashboards

| Feature | How it works |
|---|---|
| **Notification bell** | New class, scheduled upcoming, due soon, quiz reopened/extended, grade returned, student added/removed, remedial ready, unlocked, archived. Clicking opens the right item. |
| **Teacher dashboard** | Class & section rankings, per-section **Needs Intervention** counts, per-student performance dialog, remedial approvals, upcoming items. |
| **Student dashboard** | Recent results (earned/total), upcoming scheduled items, to-do list, progress. |
| **To-Do / To-Review** | Student: what's due, by date. Teacher: submissions waiting for grading, per class. |

### 4.9 Schedule

| Feature | How it works |
|---|---|
| **Timetable** | Pulled from ATLAS: days × time slots with room, teacher, section; break banners; "Now" highlight; mobile day-by-day view. |
| **Term-aware** | The term selector follows the school's calendar (e.g. trimester: 3 terms) sourced from EnrollPro; a drift warning shows if the timetable lags the enrollment system. |

### 4.10 Admin & operations

| Feature | How it works |
|---|---|
| **Integrations page** | Live status of the connected systems (EnrollPro, ATLAS, SMART) + Google Drive policy, strict-sync controls, historical backfill. |
| **School-Year Reset / Full Reset** | Cleans stale data safely: archive or purge by **year**, per-teacher breakdown, ghost enrollments, inactive users, always protecting the active year. |
| **Roster reconciliation** | Re-checks every class roster against EnrollPro and archives students who are no longer enrolled. |
| **Section coverage** | Shows which sections are fully synced (courses created, rosters, rotation metadata) and which need attention. |
| **Virtual Calendar (test-only)** | A gated mock clock + event log for testing term rollover and the `TERM_CHANGED` bus without changing real dates. |
| **Dev tools** | Clear notifications, brand/logo settings, etc. |

### 4.11 Offline / PWA

| Feature | How it works |
|---|---|
| **Installable app** | Adds to the phone's home screen; install prompt plus a sidebar fallback. |
| **Offline content** | Materials and quiz sessions are cached on the device (IndexedDB); offline quizzes and task submissions are stored and marked pending. |
| **Sync & recovery** | Pending work syncs automatically when back online; the app shows sync state/errors. |

---

## 5. The Three Unique Features (in depth)

### 5.1 AI Quiz Generation
- **Input:** a teacher's learning material **or** a plain-language prompt ("10 multiple-choice questions about photosynthesis, easy").
- **Engine:** a model cascade (several AI models configured in one place); if a model is rate-limited, overloaded, or missing, the next model is tried automatically.
- **Output:** draft questions with options and answer keys — nothing is published until the teacher reviews and edits it.
- **Anti-cheating:** "Make a different version" generates a parallel quiz so students can't share answers.
- **Why it matters:** creating a quality quiz drops from ~30 minutes to ~2 minutes of review.

### 5.2 Mastery-Based Progression
- Teachers attach **prerequisite quizzes** to materials/quizzes, or use the **gate tree** to lock items until a quiz is submitted.
- Students see exactly what is locked and why ("Requires: Quiz 1").
- Unlocks happen automatically (submit/pass/remedial) or by teacher override; gates **expire** when closed so no student is ever trapped.
- **Why it matters:** competency-based learning is enforced by the system, not by memory.

### 5.3 Intervention & Remedial System (flagship)
1. **Detect** — a student fails a quiz (or is flagged by the teacher/roster/recommended list).
2. **Diagnose** — AIMS extracts the exact items they got wrong.
3. **Generate** — AI creates a **new remedial quiz** on those gaps **plus a study kit** (summary, key points, source links) — as a draft.
4. **Approve** — the teacher reviews, edits, and assigns it.
5. **Practice** — the student reads the kit and takes **one** remedial attempt.
6. **Release** — submitting the remedial clears the mastery gate; the teacher can blend the scores (highest/average/…) into the gradebook.
- **If generation fails** (e.g. the AI model is overloaded), the retry is one click: from the failure notification or the intervention modal.
- **Why it matters:** remediation goes from "teacher writes a make-up test by hand" to a two-minute review — and every failing student is tracked to closure.

---

## 6. Integration Contracts (summary)

| Direction | What moves | Notes |
|---|---|---|
| EnrollPro → AIMS | Students, sections, school years, terms | AIMS never edits enrollment |
| ATLAS → AIMS | Teaching load, timetable, rotation ranks | Drives class creation + schedule |
| SMART → AIMS | Grading weights (WW/PT/QA) | Falls back to DepEd defaults if SMART is unavailable |
| AIMS → SMART | Public score feed (`x-api-key`) | Per-course, per-class correct; shared quizzes handled per class |
| EnrollPro → bus → AIMS/ATLAS/SMART | `TERM_CHANGED` event (RabbitMQ fanout) | AIMS applies the rollover + live UI refresh; never republishes |

---

## 7. Key Statuses (quick reference)

**Quiz:** `DRAFT` → `SCHEDULED` → `PUBLISHED` → (`CLOSED` / `ARCHIVED`)

**Student submission:** `IN_PROGRESS` → `SUBMITTED` → `GRADED` (draft to teacher) → `RETURNED` (student sees it) · plus `MISSING` / `EXCUSED` roster flags.

**Only `RETURNED` grades are final to the student.** Objective answers score instantly; written answers wait for review and never display as failures while pending.

---

*End of system documentation. Deeper technical references live alongside this file: `GRADING-AND-POINTS.md`, `REMEDIATION-AND-MASTERY.md`, `quiz-builder.md`, `CLASS-SYNC.md`, `AIMS-SMART-INTEGRATION.md`, `ARCHITECTURE_MICROSERVICES.md`.*