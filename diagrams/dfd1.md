
```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                          A.I.M.S. — LEVEL 1 DATA FLOW DIAGRAM                                  ║
║           Figure 1: Data Flow Diagram — All Actors, Processes, and Data Stores                 ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝

ACTORS (Left)         PROCESSES (Center)                      DATA STORES (Right)
─────────────────     ──────────────────────────────────────   ───────────────────────────────────

                   ┌─────────────────────────────────┐
                   │  P1.0                           │
                   │  Authenticate & Manage          │
                   │  User Accounts                  │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P2.0                           │
                   │  Manage Courses                 │
                   │  & Enrollments                  │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P3.0                           │
                   │  Manage Learning                │
                   │  Materials & Library            │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P4.0                           │
                   │  Manage Tasks                   │
                   │  & Submissions                  │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P5.0                           │
                   │  Deliver & Grade                │
                   │  Assessments                    │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P6.0                           │
                   │  Generate & Approve             │
                   │  Remedial Interventions         │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P7.0                           │
                   │  Control Mastery-Based          │
                   │  Progression                    │
                   └─────────────────────────────────┘

                   ┌─────────────────────────────────┐
                   │  P8.0                           │
                   │  Manage Grades, Weights         │
                   │  & Notifications                │
                   └─────────────────────────────────┘
```

---

## COMPLETE NAMED DATA FLOW CONNECTIONS

---

### P1.0 — Authenticate & Manage User Accounts

```
TEACHER ──── Login Credentials ──────────────────────────────────────────────────► P1.0
TEACHER ──── Registration Details ───────────────────────────────────────────────► P1.0
TEACHER ──── Google OAuth Authorization Code ────────────────────────────────────► P1.0
TEACHER ──── Profile Update Details ─────────────────────────────────────────────► P1.0
TEACHER ──── Email Verification Token ───────────────────────────────────────────► P1.0
TEACHER ◄─── Access Token & Session Data ────────────────────────────────────────── P1.0
TEACHER ◄─── Authenticated User Profile ─────────────────────────────────────────── P1.0
TEACHER ◄─── Verification Email Status ──────────────────────────────────────────── P1.0
TEACHER ◄─── Google Drive Connection Status ─────────────────────────────────────── P1.0

STUDENT ──── Login Credentials ──────────────────────────────────────────────────► P1.0
STUDENT ──── Registration Details ───────────────────────────────────────────────► P1.0
STUDENT ──── Google OAuth Authorization Code ────────────────────────────────────► P1.0
STUDENT ──── Email Verification Token ───────────────────────────────────────────► P1.0
STUDENT ◄─── Access Token & Session Data ────────────────────────────────────────── P1.0
STUDENT ◄─── Authenticated User Profile ─────────────────────────────────────────── P1.0
STUDENT ◄─── Verification Email Status ──────────────────────────────────────────── P1.0

P1.0 ──── User Account Record ───────────────────────────────────────────────────► DS1 : users
P1.0 ──── Profile Update ────────────────────────────────────────────────────────► DS1 : users
P1.0 ──── Google Token Fields ───────────────────────────────────────────────────► DS1 : users
DS1  ──── User Profile & Role ───────────────────────────────────────────────────► P1.0
P1.0 ──── Session Token Record ──────────────────────────────────────────────────► DS2 : refresh_tokens
P1.0 ──── Token Revocation ──────────────────────────────────────────────────────► DS2 : refresh_tokens
DS2  ──── Token Validation Data ─────────────────────────────────────────────────► P1.0
DS3  ──── School Identity Data ──────────────────────────────────────────────────► P1.0
```

---

### P2.0 — Manage Courses & Enrollments

```
TEACHER ──── Course Configuration Data ──────────────────────────────────────────► P2.0
              (name, code, subject, grade level, school year, color)
TEACHER ──── Topic Details ──────────────────────────────────────────────────────► P2.0
TEACHER ──── Topic Reorder Index ────────────────────────────────────────────────► P2.0
TEACHER ──── Announcement Content & File ────────────────────────────────────────► P2.0
TEACHER ──── Announcement Schedule ─────────────────────────────────────────────► P2.0
TEACHER ──── Announcement Comment ──────────────────────────────────────────────► P2.0
TEACHER ──── Archive Course Request ─────────────────────────────────────────────► P2.0
TEACHER ──── Enrollment Archive Toggle ──────────────────────────────────────────► P2.0
TEACHER ──── Printed Copy Flag ──────────────────────────────────────────────────► P2.0
TEACHER ──── Reuse Post Selection ───────────────────────────────────────────────► P2.0
TEACHER ◄─── Course Record & Class Code ─────────────────────────────────────────── P2.0
TEACHER ◄─── Enrolled Student Roster ────────────────────────────────────────────── P2.0
TEACHER ◄─── Topic List with Order ──────────────────────────────────────────────── P2.0
TEACHER ◄─── Announcement Confirmation ──────────────────────────────────────────── P2.0

STUDENT ──── Class Join Code ────────────────────────────────────────────────────► P2.0
STUDENT ──── Enrollment Request ─────────────────────────────────────────────────► P2.0
STUDENT ──── Archive Enrollment Request ─────────────────────────────────────────► P2.0
STUDENT ──── Announcement Comment ──────────────────────────────────────────────► P2.0
STUDENT ◄─── Enrollment Confirmation ────────────────────────────────────────────── P2.0
STUDENT ◄─── Course Access Details ──────────────────────────────────────────────── P2.0
STUDENT ◄─── Announcement & Comment Feed ────────────────────────────────────────── P2.0

P2.0 ──── Course Record ─────────────────────────────────────────────────────────► DS4 : courses
P2.0 ──── Course Archive Flag ───────────────────────────────────────────────────► DS4 : courses
DS4  ──── Course Configuration ──────────────────────────────────────────────────► P2.0
P2.0 ──── Enrollment Record ─────────────────────────────────────────────────────► DS5 : enrollments
P2.0 ──── Enrollment Archive Status ─────────────────────────────────────────────► DS5 : enrollments
P2.0 ──── Printed Copy Flag ─────────────────────────────────────────────────────► DS5 : enrollments
DS5  ──── Enrollment List & Status ──────────────────────────────────────────────► P2.0
P2.0 ──── Topic Record ──────────────────────────────────────────────────────────► DS6 : topics
P2.0 ──── Topic Reorder Update ──────────────────────────────────────────────────► DS6 : topics
DS6  ──── Topic List ────────────────────────────────────────────────────────────► P2.0
P2.0 ──── Announcement Record ───────────────────────────────────────────────────► DS10 : announcements
DS10 ──── Announcement Feed ─────────────────────────────────────────────────────► P2.0
P2.0 ──── Comment Record ────────────────────────────────────────────────────────► DS11 : announcement_comments
DS11 ──── Comment Thread ────────────────────────────────────────────────────────► P2.0
DS1  ──── User Profile Lookup ───────────────────────────────────────────────────► P2.0
```

---

### P3.0 — Manage Learning Materials & Library

```
TEACHER ──── Material Upload (File / Link / YouTube) ────────────────────────────► P3.0
TEACHER ──── Material Metadata (title, topic, description) ──────────────────────► P3.0
TEACHER ──── Publish / Schedule / Draft Command ─────────────────────────────────► P3.0
TEACHER ──── Attachment Files ───────────────────────────────────────────────────► P3.0
TEACHER ──── Library Resource Details ───────────────────────────────────────────► P3.0
TEACHER ──── Deploy to Course Request ───────────────────────────────────────────► P3.0
TEACHER ──── Drive Storage Preference ───────────────────────────────────────────► P3.0
TEACHER ──── Resource Delete Request ────────────────────────────────────────────► P3.0
TEACHER ◄─── Published Material Confirmation ────────────────────────────────────── P3.0
TEACHER ◄─── Library Resource List ──────────────────────────────────────────────── P3.0
TEACHER ◄─── Deployment History ─────────────────────────────────────────────────── P3.0
TEACHER ◄─── File Download Stream ───────────────────────────────────────────────── P3.0

STUDENT ──── Material Access Request ────────────────────────────────────────────► P3.0
STUDENT ──── File Download Request ──────────────────────────────────────────────► P3.0
STUDENT ──── Offline Save Request ───────────────────────────────────────────────► P3.0
STUDENT ◄─── Material Content & Attachments ─────────────────────────────────────── P3.0
STUDENT ◄─── File Download Stream ───────────────────────────────────────────────── P3.0
STUDENT ◄─── Offline File Data ──────────────────────────────────────────────────── P3.0

P3.0 ──── Resource Record ───────────────────────────────────────────────────────► DS7 : resources
P3.0 ──── Status Update (DRAFT/SCHEDULED/PUBLISHED) ────────────────────────────► DS7 : resources
DS7  ──── Resource Metadata & File Path ─────────────────────────────────────────► P3.0
P3.0 ──── Attachment File Record ────────────────────────────────────────────────► DS8 : resource_attachments
DS8  ──── Attachment List & Download Path ───────────────────────────────────────► P3.0
P3.0 ──── Deployment Record ─────────────────────────────────────────────────────► DS9 : resource_deployments
DS9  ──── Deployment History ────────────────────────────────────────────────────► P3.0
P3.0 ──── Resource View / Download Log Entry ────────────────────────────────────► DS30 : activity_logs
DS4  ──── Course & Storage Backend Configuration ────────────────────────────────► P3.0
DS5  ──── Student Access Verification ───────────────────────────────────────────► P3.0
DS6  ──── Topic Association ─────────────────────────────────────────────────────► P3.0
```

---

### P4.0 — Manage Tasks & Submissions

```
TEACHER ──── Task Details (title, type, points, due date, topic) ────────────────► P4.0
TEACHER ──── Task Attachment Files ──────────────────────────────────────────────► P4.0
TEACHER ──── Rubric Configuration (criteria & levels) ───────────────────────────► P4.0
TEACHER ──── Grade Entry & Feedback ─────────────────────────────────────────────► P4.0
TEACHER ──── Rubric Grade Entry per Criterion ───────────────────────────────────► P4.0
TEACHER ──── Bulk Status Update (MISSING / EXCUSED) ─────────────────────────────► P4.0
TEACHER ──── Return Grades Command ──────────────────────────────────────────────► P4.0
TEACHER ──── Private Comment & Feedback ─────────────────────────────────────────► P4.0
TEACHER ──── Task Delete Request ────────────────────────────────────────────────► P4.0
TEACHER ◄─── Task Creation Confirmation ─────────────────────────────────────────── P4.0
TEACHER ◄─── All Student Submissions ────────────────────────────────────────────── P4.0
TEACHER ◄─── Rubric Grade Detail ────────────────────────────────────────────────── P4.0
TEACHER ◄─── Comment Thread ─────────────────────────────────────────────────────── P4.0

STUDENT ──── Submitted Task Files ───────────────────────────────────────────────► P4.0
STUDENT ──── Task Comment ───────────────────────────────────────────────────────► P4.0
STUDENT ──── Unsubmit Request ───────────────────────────────────────────────────► P4.0
STUDENT ◄─── Assigned Task Details ──────────────────────────────────────────────── P4.0
STUDENT ◄─── Submission Confirmation ────────────────────────────────────────────── P4.0
STUDENT ◄─── Grade & Feedback ───────────────────────────────────────────────────── P4.0
STUDENT ◄─── Rubric Assessment Result ───────────────────────────────────────────── P4.0
STUDENT ◄─── Comment Reply ──────────────────────────────────────────────────────── P4.0

P4.0 ──── Task Record ───────────────────────────────────────────────────────────► DS12 : tasks
P4.0 ──── Status Update (DRAFT/PUBLISHED) ───────────────────────────────────────► DS12 : tasks
DS12 ──── Task Details & Instructions ───────────────────────────────────────────► P4.0
P4.0 ──── Attachment Record ─────────────────────────────────────────────────────► DS13 : task_attachments
DS13 ──── Attachment Download Path ──────────────────────────────────────────────► P4.0
P4.0 ──── Submission Record ─────────────────────────────────────────────────────► DS14 : task_submissions
P4.0 ──── Grade, Feedback & Return Flag ─────────────────────────────────────────► DS14 : task_submissions
P4.0 ──── Bulk Status Update ────────────────────────────────────────────────────► DS14 : task_submissions
DS14 ──── Submission List & Grade Data ──────────────────────────────────────────► P4.0
P4.0 ──── Submitted File Record ─────────────────────────────────────────────────► DS15 : task_submission_files
DS15 ──── Submitted File Path ───────────────────────────────────────────────────► P4.0
P4.0 ──── Comment Record ────────────────────────────────────────────────────────► DS16 : task_comments
DS16 ──── Comment Thread ────────────────────────────────────────────────────────► P4.0
P4.0 ──── Rubric Record (upsert) ────────────────────────────────────────────────► DS23 : rubrics
DS23 ──── Rubric Configuration ──────────────────────────────────────────────────► P4.0
P4.0 ──── Criterion Record ──────────────────────────────────────────────────────► DS24 : rubric_criteria
DS24 ──── Criterion List ────────────────────────────────────────────────────────► P4.0
P4.0 ──── Level Record ──────────────────────────────────────────────────────────► DS25 : rubric_levels
DS25 ──── Level Options ─────────────────────────────────────────────────────────► P4.0
P4.0 ──── Rubric Grade per Criterion ────────────────────────────────────────────► DS26 : rubric_grades
DS26 ──── Graded Rubric for Submission ──────────────────────────────────────────► P4.0
DS27 ──── Weight Category Lookup ────────────────────────────────────────────────► P4.0
DS5  ──── Student Enrollment Verification ───────────────────────────────────────► P4.0
```

---

### P5.0 — Deliver & Grade Assessments

```
TEACHER ──── Quiz Configuration (title, passing score, time limit, due date) ────► P5.0
TEACHER ──── AI Generation Request (resource / topic / prompt) ──────────────────► P5.0
TEACHER ──── Question Set & Answer Keys ─────────────────────────────────────────► P5.0
TEACHER ──── Quiz Attachment Files ──────────────────────────────────────────────► P5.0
TEACHER ──── Grading Weight Assignment ──────────────────────────────────────────► P5.0
TEACHER ──── Publish / Schedule Command ─────────────────────────────────────────► P5.0
TEACHER ──── Manual Score Override ──────────────────────────────────────────────► P5.0
TEACHER ──── Direct Grade Entry (no submission) ─────────────────────────────────► P5.0
TEACHER ──── Quiz Rubric Configuration ──────────────────────────────────────────► P5.0
TEACHER ──── Bulk Status Update (MISSING / EXCUSED) ─────────────────────────────► P5.0
TEACHER ──── Quiz Comment & Feedback ────────────────────────────────────────────► P5.0
TEACHER ◄─── AI-Generated Draft Quiz for Review ─────────────────────────────────── P5.0
TEACHER ◄─── All Student Submissions Summary ────────────────────────────────────── P5.0
TEACHER ◄─── Pending Manual Review Items ────────────────────────────────────────── P5.0
TEACHER ◄─── Quiz Grade Report ──────────────────────────────────────────────────── P5.0
TEACHER ◄─── Quiz Comment Thread ────────────────────────────────────────────────── P5.0

STUDENT ──── Quiz Start Request ─────────────────────────────────────────────────► P5.0
STUDENT ──── Quiz Answers (on submit) ───────────────────────────────────────────► P5.0
STUDENT ──── Offline Quiz Session Sync ──────────────────────────────────────────► P5.0
STUDENT ──── Quiz Comment ───────────────────────────────────────────────────────► P5.0
STUDENT ◄─── Active Quiz with Questions ─────────────────────────────────────────── P5.0
STUDENT ◄─── Score & Pass / Fail Result ─────────────────────────────────────────── P5.0
STUDENT ◄─── Correct Answers Revealed (post-grading) ───────────────────────────── P5.0
STUDENT ◄─── Quiz Comment Reply ─────────────────────────────────────────────────── P5.0

P5.0 ──── Quiz Record ───────────────────────────────────────────────────────────► DS17 : quizzes
P5.0 ──── Status Update (DRAFT/PUBLISHED/CLOSED) ───────────────────────────────► DS17 : quizzes
P5.0 ──── Multi-Course Copy Record ──────────────────────────────────────────────► DS17 : quizzes
DS17 ──── Quiz Configuration & Threshold ────────────────────────────────────────► P5.0
P5.0 ──── Attachment Record ─────────────────────────────────────────────────────► DS18 : quiz_attachments
DS18 ──── Attachment Download Path ──────────────────────────────────────────────► P5.0
P5.0 ──── Question Record & Answer Key ──────────────────────────────────────────► DS19 : questions
P5.0 ──── AI-Generated Question Set ─────────────────────────────────────────────► DS19 : questions
DS19 ──── Question Set for Delivery ─────────────────────────────────────────────► P5.0
P5.0 ──── Submission Record ─────────────────────────────────────────────────────► DS20 : submissions
P5.0 ──── Auto-Graded Score & Status ────────────────────────────────────────────► DS20 : submissions
DS20 ──── Submission History & Score ────────────────────────────────────────────► P5.0
P5.0 ──── Answer Record & Correctness Flag ──────────────────────────────────────► DS21 : answers
DS21 ──── Student Answers for Review ────────────────────────────────────────────► P5.0
P5.0 ──── Comment Record ────────────────────────────────────────────────────────► DS22 : quiz_comments
DS22 ──── Comment Thread ────────────────────────────────────────────────────────► P5.0
P5.0 ──── Quiz Rubric Record ────────────────────────────────────────────────────► DS23 : rubrics
DS23 ──── Rubric Configuration ──────────────────────────────────────────────────► P5.0
P5.0 ──── Criterion Record ──────────────────────────────────────────────────────► DS24 : rubric_criteria
DS24 ──── Criterion List ────────────────────────────────────────────────────────► P5.0
P5.0 ──── Level Record ──────────────────────────────────────────────────────────► DS25 : rubric_levels
DS25 ──── Level Options ─────────────────────────────────────────────────────────► P5.0
P5.0 ──── Rubric Grade Entry ────────────────────────────────────────────────────► DS26 : rubric_grades
DS26 ──── Graded Rubric for Submission ──────────────────────────────────────────► P5.0
P5.0 ──── Grading Weight Assignment ─────────────────────────────────────────────► DS27 : grading_weights
DS27 ──── Weight Configuration ──────────────────────────────────────────────────► P5.0
DS7  ──── Source Material Text (for AI) ─────────────────────────────────────────► P5.0
DS4  ──── Course Mastery Threshold ──────────────────────────────────────────────► P5.0
P5.0 ──── Quiz Start / Submit Log Entry ─────────────────────────────────────────► DS30 : activity_logs
```

---

### P6.0 — Generate & Approve Remedial Interventions

```
TEACHER ──── Remedial Approval Decision ─────────────────────────────────────────► P6.0
TEACHER ──── Question Revision ──────────────────────────────────────────────────► P6.0
TEACHER ──── Manual Remedial Generation Request ─────────────────────────────────► P6.0
TEACHER ◄─── Remedial Pending Notification ──────────────────────────────────────── P6.0
TEACHER ◄─── Draft Remedial Quiz for Review ─────────────────────────────────────── P6.0

P5.0   ──── Failed Submission Trigger ───────────────────────────────────────────► P6.0
STUDENT ◄─── Remedial Quiz Assignment Notification ──────────────────────────────── P6.0

DS20 ──── Wrong Answer Analysis (Gap Identification) ────────────────────────────► P6.0
DS21 ──── Incorrect Answer Details ──────────────────────────────────────────────► P6.0
DS19 ──── Original Question Data for Context ────────────────────────────────────► P6.0
DS7  ──── Source Material Text for AI Generation ────────────────────────────────► P6.0
P6.0 ──── Remedial Quiz Draft (isRemedial, forStudentId) ────────────────────────► DS17 : quizzes
DS17 ──── Approved Remedial Quiz ────────────────────────────────────────────────► P6.0
P6.0 ──── AI-Generated Remedial Question Set ────────────────────────────────────► DS19 : questions
P6.0 ──── REMEDIAL_PENDING Notification Record ──────────────────────────────────► DS29 : notifications
DS29 ──── Notification Delivery Status ──────────────────────────────────────────► P6.0
```

---

### P7.0 — Control Mastery-Based Progression

```
TEACHER ──── Mastery Lock Configuration (enable / disable / threshold) ──────────► P7.0
TEACHER ──── Lock Mode Selection (PROSPECTIVE / RETROACTIVE) ────────────────────► P7.0
TEACHER ──── masteryLockActivatedAt Timestamp ───────────────────────────────────► P7.0
TEACHER ──── Manual Student Unlock Request ──────────────────────────────────────► P7.0
TEACHER ──── Bulk Unlock Request (for quiz) ─────────────────────────────────────► P7.0
TEACHER ◄─── Locked Student Report ──────────────────────────────────────────────── P7.0
TEACHER ◄─── Mastery Status per Student ─────────────────────────────────────────── P7.0
TEACHER ◄─── Flagged Students Preview ───────────────────────────────────────────── P7.0

STUDENT ──── Resource / Quiz Access Request ─────────────────────────────────────► P7.0
STUDENT ◄─── Access Granted / Locked Status ─────────────────────────────────────── P7.0
STUDENT ◄─── Next Resource Unlocked ─────────────────────────────────────────────── P7.0

P7.0 ──── Mastery Lock Settings Record ──────────────────────────────────────────► DS4 : courses
P7.0 ──── Lock Mode & masteryLockActivatedAt ────────────────────────────────────► DS4 : courses
DS4  ──── Mastery Lock Configuration ────────────────────────────────────────────► P7.0
DS17 ──── Quiz Passing Threshold ────────────────────────────────────────────────► P7.0
DS20 ──── Student Score Records for Gate Evaluation ─────────────────────────────► P7.0
DS5  ──── Enrollment Date (for PROSPECTIVE mode check) ──────────────────────────► P7.0
DS7  ──── Resource Upload Date (for PROSPECTIVE lock boundary) ──────────────────► P7.0
P7.0 ──── Manual Unlock Record (courseId, studentId, quizId) ────────────────────► DS28 : mastery_unlocks
DS28 ──── Override Unlock Records ───────────────────────────────────────────────► P7.0
```

---

### P8.0 — Manage Grades, Weights & Notifications

```
TEACHER ──── Grading Weight Category (name, percentage, color) ──────────────────► P8.0
TEACHER ──── Gradebook View Request ─────────────────────────────────────────────► P8.0
TEACHER ──── Notification Read Command ──────────────────────────────────────────► P8.0
TEACHER ──── Mark All Notifications Read ────────────────────────────────────────► P8.0
TEACHER ◄─── Full Gradebook (DepEd WW / PT / QA weighted) ──────────────────────── P8.0
TEACHER ◄─── Per-Student DepEd Grade Descriptor ─────────────────────────────────── P8.0
TEACHER ◄─── Unread Notification Count ──────────────────────────────────────────── P8.0
TEACHER ◄─── Notification List ──────────────────────────────────────────────────── P8.0

STUDENT ──── Personal Progress View Request ─────────────────────────────────────► P8.0
STUDENT ──── Notification Read Command ──────────────────────────────────────────► P8.0
STUDENT ◄─── Personal Grade Summary ────────────────────────────────────────────── P8.0
STUDENT ◄─── Course Performance Data ───────────────────────────────────────────── P8.0
STUDENT ◄─── DepEd Grade Descriptor ────────────────────────────────────────────── P8.0
STUDENT ◄─── Unread Notification Count ──────────────────────────────────────────── P8.0
STUDENT ◄─── Notification List ──────────────────────────────────────────────────── P8.0

P8.0 ──── Grading Weight Record ─────────────────────────────────────────────────► DS27 : grading_weights
P8.0 ──── Weight Update / Delete ────────────────────────────────────────────────► DS27 : grading_weights
DS27 ──── Weight Configuration for Grade Computation ───────────────────────────► P8.0
DS14 ──── Task Grades for Gradebook ─────────────────────────────────────────────► P8.0
DS20 ──── Quiz Scores for Gradebook ─────────────────────────────────────────────► P8.0
DS12 ──── Task Type for DepEd Category Mapping ──────────────────────────────────► P8.0
DS17 ──── Quiz Task Type for DepEd Category Mapping ─────────────────────────────► P8.0
DS5  ──── Student Enrollment List & Printed Copy Flag ───────────────────────────► P8.0
P8.0 ──── Notification Read Status ──────────────────────────────────────────────► DS29 : notifications
DS29 ──── Notification List & Unread Count ──────────────────────────────────────► P8.0
```

---

## DATA STORE REGISTRY (30 Tables)

```
DS1  : users                   — P1.0, P2.0
DS2  : refresh_tokens          — P1.0
DS3  : schools                 — P1.0
DS4  : courses                 — P2.0, P3.0, P5.0, P7.0, P8.0
DS5  : enrollments             — P2.0, P3.0, P4.0, P7.0, P8.0
DS6  : topics                  — P2.0, P3.0
DS7  : resources               — P3.0, P5.0, P6.0, P7.0
DS8  : resource_attachments    — P3.0
DS9  : resource_deployments    — P3.0
DS10 : announcements           — P2.0
DS11 : announcement_comments   — P2.0
DS12 : tasks                   — P4.0, P8.0
DS13 : task_attachments        — P4.0
DS14 : task_submissions        — P4.0, P8.0
DS15 : task_submission_files   — P4.0
DS16 : task_comments           — P4.0
DS17 : quizzes                 — P5.0, P6.0, P7.0, P8.0
DS18 : quiz_attachments        — P5.0
DS19 : questions               — P5.0, P6.0
DS20 : submissions             — P5.0, P6.0, P7.0, P8.0
DS21 : answers                 — P5.0, P6.0
DS22 : quiz_comments           — P5.0
DS23 : rubrics                 — P4.0, P5.0
DS24 : rubric_criteria         — P4.0, P5.0
DS25 : rubric_levels           — P4.0, P5.0
DS26 : rubric_grades           — P4.0, P5.0
DS27 : grading_weights         — P4.0, P5.0, P8.0
DS28 : mastery_unlocks         — P7.0
DS29 : notifications           — P6.0, P8.0
DS30 : activity_logs           — P3.0, P5.0
```

---

## DRAW.IO CONSTRUCTION NOTES

**Layout guide (left → center → right):**
- Place `TEACHER` and `STUDENT` as rectangles on the **far left**
- Place `P1.0` through `P8.0` as rounded rectangles (or circles) stacked **vertically in the center**
- Place `DS1` through `DS30` as **open-ended horizontal rectangles** on the **far right**, stacked vertically in DS number order
- Draw labeled arrows between actor ↔ process, and process ↔ data store
- Flows from **P5.0 → P6.0** (failed submission trigger) are **process-to-process** arrows (drawn between the two center boxes)
- All DS arrows that are **read-only** (DS → Process, one-way) should be drawn with a **single arrowhead pointing left** (toward the process)
- DS arrows that are **read + write** should use **double arrowheads** (bidirectional)
