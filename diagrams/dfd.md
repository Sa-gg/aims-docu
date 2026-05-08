## A.I.M.S — DFD Guide for draw.io (Updated)

---

### EXTERNAL ENTITIES (Rectangles — left side)

| ID | Label |
|----|-------|
| E1 | Teacher |
| E2 | Student |

---

### PROCESSES (Circles/Rounded Rectangles — centre)

| ID | Label |
|----|-------|
| P1 | 1.0 Learning Portal — Material & Task Distribution |
| P2 | 2.0 AI Quiz Generator & Instructor Validation |
| P3 | 3.0 Assessment & Grading Engine |
| P4 | 4.0 Remedial Quiz Generator |
| P5 | 5.0 Mastery-Based Progression Lock |

---

### DATA STORES (Open-ended rectangles — right side)

| ID | Label |
|----|-------|
| D1 | D1 — Course & Enrollment |
| D2 | D2 — Resource & Material |
| D3 | D3 — Task & Submission |
| D4 | D4 — Quiz & Question |
| D5 | D5 — Grade & Assessment |
| D6 | D6 — Mastery & Unlock |

---

### DATA FLOWS (Arrows with labels)

#### Process 1.0 — Learning Portal
| From | To | Label |
|------|----|-------|
| Teacher | P1 | Course Setup / Material Upload |
| Teacher | P1 | Task Assignment |
| Student | P1 | Portal Access / Task Submission |
| P1 | Student | Materials & Instructions |
| P1 | D1 | Course / Enrollment Record |
| P1 | D2 | Resource Record |
| P1 | D3 | Task Record |
| P1 | D3 | Submission Record |
| D1 | P1 | Enrollment Data |

#### Process 2.0 — AI Quiz Generator
| From | To | Label |
|------|----|-------|
| Teacher | P2 | Topic Prompt / Material Selection |
| D2 | P2 | Material Content |
| P2 | Teacher | Draft Quiz for Review |
| Teacher | P2 | Approved Quiz / Edits |
| P2 | D4 | Published Quiz Record |

#### Process 3.0 — Assessment & Grading Engine
| From | To | Label |
|------|----|-------|
| Student | P3 | Quiz Responses |
| D4 | P3 | Questions & Answer Key |
| P3 | Teacher | Subjective Items for Review |
| Teacher | P3 | Manual Score |
| P3 | Student | Final Grade & Results |
| P3 | D5 | Grade Record |

#### Process 4.0 — Remedial Quiz Generator
| From | To | Label |
|------|----|-------|
| D5 | P4 | Failed Assessment Data |
| D4 | P4 | Question Bank (Incorrect Items) |
| P4 | Teacher | Remedial Draft for Review |
| Teacher | P4 | Approved Remedial Quiz |
| P4 | D4 | Remedial Quiz Record |
| P4 | Student | Assigned Remedial Quiz |

#### Process 5.0 — Mastery-Based Progression Lock
| From | To | Label |
|------|----|-------|
| Teacher | P5 | Lock Config & Pass Threshold |
| Teacher | P5 | Manual Override |
| D5 | P5 | Assessment Result |
| D6 | P5 | Current Lock Status |
| P5 | Student | Lock / Unlock Status |
| P5 | D6 | Unlock Record |
| P5 | P4 | Trigger Remedial Workflow |

---

### draw.io Layout Tips

- Place *E1 Teacher* and *E2 Student* in a vertical column on the *left*
- Place *P1–P5* in a vertical column in the *centre*, top-to-bottom in order
- Place *D1–D6* in a vertical column on the *right*, top-to-bottom in order
- Teacher has bidirectional feedback loops with *P2* (draft review) and *P3* (manual scoring)
- The *P5 → P4* arrow is a process-to-process flow; route it below both processes to avoid overlap