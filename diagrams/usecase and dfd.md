## Context Diagram (Level 0) — Complete

**Teacher → AIMS:**
1. Learning Materials & Class Configurations
2. Task & Grade Management Data
3. Quiz Approval & Subjective Grades
4. Remedial Approvals & Lock Overrides

**AIMS → Teacher:**
1. Generated AI Quiz Drafts
2. Student Performance & Analytics
3. Pending Notifications & Alerts

**Student → AIMS:**
1. Class Join Code
2. Completed Tasks & Quiz Answers

**AIMS → Student:**
1. Learning Materials & Active Assessments
2. Remedial Quizzes
3. Mastery Status & Final Grades
4. Notifications & Grade Updates

---

## Use Case Diagram — Complete (16 use cases)

| # | Use Case | Actor(s) |
|---|---|---|
| 1 | Create & Manage Course | Teacher |
| 2 | Join Course via Class Code | Student |
| 3 | Upload Learning Materials | Teacher |
| 4 | Access Learning Materials | Student |
| 5 | Create & Grade Tasks | Teacher |
| 6 | Submit Completed Task | Student |
| 7 | Generate AI Quiz | Teacher |
| 8 | Review and Publish Quiz | Teacher |
| 9 | Take Quiz Assessment | Student |
| 10 | Validate Subjective Response | Teacher |
| 11 | Manage Grading Weights | Teacher |
| 12 | View Final Grades | Teacher + Student |
| 13 | Review & Approve Remedial Quiz | Teacher |
| 14 | Take Remedial Quiz | Student |
| 15 | Configure Mastery Locks | Teacher |
| 16 | View & Manage Notifications | Teacher + Student |

---

**Changes from your current diagrams:**
- **Context diagram:** Add "Task & Grade Management Data" (Teacher→AIMS), "Pending Notifications & Alerts" (AIMS→Teacher), "Class Join Code" (Student→AIMS), "Notifications & Grade Updates" (AIMS→Student)
- **Use case diagram:** Add use cases 1, 2, 5, 11, 12 (update), 16 — keep all existing 11 as-is