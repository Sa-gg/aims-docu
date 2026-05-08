# A.I.M.S. (Automated Intervention and Mastery System) — System Update Documentation

**System Development Accomplishment Report**

**Submitted by:**
- Mikhoel Runo B. Orbigoso
- Patrick R. Sagum
- Maika T. Zambra

**Course:** Capstone Project
**Program:** Bachelor of Science in Information Technology
**Institution:** Carlos Hilado Memorial State University — Alijis Campus, Bacolod City

---

## System Overview

A.I.M.S. (Automated Intervention and Mastery System) is a web-based Learning Management System (LMS) designed as one of three interconnected modules within a School ERP (Enterprise Resource Planning) system for Philippine public high schools. The system's user interface and experience design is modeled after Google Classroom, ensuring a minimal learning curve for teachers and students who are already familiar with Google's educational ecosystem.

The three ERP modules work together as follows:

- **Schedule Module (School ERP)** — Manages class schedules, section assignments, and teacher loads. The LMS fetches schedule data from this module to auto-enroll teachers and students into their respective classes, eliminating the need for manual enrollment.
- **A.I.M.S. LMS Module** — Provides AI-powered quiz generation, automated grading, module distribution, mastery-based progression, and performance tracking for asynchronous learning activities (online quizzes, assignments, and materials).
- **Class Records Module (School ERP)** — Maintains the complete official class record of student grades. Since A.I.M.S. handles partial grades from asynchronous activities, the LMS automatically updates and syncs these grades to the Class Records module, ensuring a unified and up-to-date academic record.

This documentation presents the current state of the developed system, organized by feature and user flow, with accompanying descriptions for each page.

---

## Page 1: Authentication — Login Page with Google Sign-In Integration

**[Insert Screenshot: Login Page]**

The A.I.M.S. login page serves as the entry point to the system. It features an integrated Google Sign-In option, allowing teachers and students to authenticate using their existing Google accounts. This integration eliminates the need for users to create and manage separate credentials, streamlining the onboarding process. Upon clicking the "Sign in with Google" button, users are redirected through Google's OAuth 2.0 authentication flow, which securely verifies their identity and returns them to the system. The design follows Google Classroom's familiar authentication pattern, reducing the learning curve for first-time users.

---

## Page 2: Authentication — Role Selection (First-time Google Sign-In)

**[Insert Screenshot: Role Selection Page]**

When a user signs in with Google for the first time, the system prompts them to select their role — either **Teacher** or **Student**. This one-time selection determines the user's access level, interface layout, and feature availability throughout the system. Teachers gain access to course management, quiz generation, material uploads, and grading tools, while students see enrolled courses, assignments, and their performance dashboard. After selecting a role, the user is directed to the Home page and does not see this selection screen again on subsequent logins.

---

## Page 3: Home Page — Class Cards Overview (Teacher View)

**[Insert Screenshot: Teacher Home Page with class cards]**

The Home page displays all classes assigned to the teacher as visually distinct class cards, styled after Google Classroom's card-based layout. Each card shows the subject name, grade level and section (e.g., "Grade 7 — 1"), the class code, and the number of enrolled students. The cards use a color-coded banner for quick visual identification. Teachers can click on any card to enter the course detail page. The sidebar navigation on the left provides quick access to Home, Schedule, Materials, and other system sections. Under the "Teaching" section in the sidebar, each active class is also listed for direct access.

---

## Page 4: Home Page — Class Cards Overview (Student View)

**[Insert Screenshot: Student Home Page with class cards]**

The student Home page follows the same card-based layout as the teacher view for visual consistency. Each card displays the subject name, grade level and section, the class code, and the teacher's name. Students can click any card to view course content, assignments, and their grades. The sidebar shows navigation links including Home, Schedule, Materials, My Quizzes, and Progress. Under the "Enrolled" section in the sidebar, each class the student is enrolled in is listed, with the grade and section shown beneath each class name.

---

## Page 5: Course Detail — Stream Tab (Teacher View)

**[Insert Screenshot: Teacher course page — Stream tab]**

The Stream tab serves as the main activity feed for the course, combining all announcements, posted quizzes, and uploaded materials into a single chronological timeline. At the top of the stream, teachers can compose and post announcements to communicate with the class. Below the composer, each feed item displays the poster's Google profile picture, name, a description of the action (e.g., "posted a new assignment: Quiz 1" or "posted a new material: Lesson 2"), and a relative timestamp. The right sidebar shows a class code card for easy sharing, upcoming work, and mastery-lock alerts when students have been locked due to failed assessments. The breadcrumb navigation at the top of the page shows the full path: Classes > Subject (Grade Level — Section).

---

## Page 6: Course Detail — Stream Tab (Student View)

**[Insert Screenshot: Student course page — Stream tab]**

The student Stream tab displays the same chronological activity feed — announcements, quizzes, and materials posted by the teacher. Students can view announcements with the ability to add comments, click on quiz posts to navigate to the quiz detail page, and click on material posts to view uploaded learning resources. The right sidebar displays an "Upcoming Work" card listing quizzes that the student has not yet completed. The Google Classroom-inspired layout ensures students can quickly scan recent class activity and identify pending tasks.

---

## Page 7: Course Detail — Classwork Tab (Teacher View)

**[Insert Screenshot: Teacher course page — Classwork tab]**

The Classwork tab organizes course content by topics. Teachers can create topic groupings and assign quizzes and materials under each topic. Each quiz entry shows its title, type (AI-generated or manual), number of questions, and creation date. Materials are listed alongside quizzes within their respective topics. This structured view gives teachers a comprehensive overview of all course content and assessments, enabling them to manage the curriculum flow and ensure alignment with DepEd competencies.

---

## Page 8: Course Detail — Classwork Tab (Student View)

**[Insert Screenshot: Student course page — Classwork tab]**

The student Classwork tab displays the same topic-based organization but with a student-focused perspective. Each quiz shows the student's submission status — whether it is "Not yet taken," "Passed," "Failed," or "Locked" due to the mastery-lock system. The mastery-lock feature restricts access to subsequent quizzes until the student achieves a passing score (70% or higher) on the previous assessment. When a student fails, the system automatically generates and deploys a remediation quiz. Resources and materials uploaded by the teacher are also accessible within each topic.

---

## Page 9: Course Detail — People Tab (Teacher View)

**[Insert Screenshot: Teacher course page — People tab]**

The People tab displays all members of the course. The teacher's section shows the teacher's name and Google profile picture. Below that, the Classmates/Students section lists all enrolled students with their profile pictures, names, and the date they joined the class. This tab provides a quick overview of class composition. Student enrollment is handled automatically through the Schedule module of the School ERP — when a student is assigned to a section in the schedule system, they are auto-enrolled in the corresponding LMS course.

---

## Page 10: Course Detail — People Tab (Student View)

**[Insert Screenshot: Student course page — People tab]**

The student view of the People tab shows the teacher at the top with their Google profile picture and name, followed by a list of classmates. The current user is tagged with a "You" badge for easy identification. This tab allows students to see their teacher and fellow classmates, fostering a sense of classroom community in the online environment.

---

## Page 11: Course Detail — Grades Tab (Teacher View)

**[Insert Screenshot: Teacher course page — Grades tab / Gradebook]**

The Grades tab presents a comprehensive gradebook view for the teacher, displaying all students and their scores across all quizzes in the course. The table format shows each student's name, individual quiz scores, passing status, and overall course performance. Teachers can review which students have passed, failed, or not yet taken each assessment. Color-coded indicators (green for passing, red for failing) provide at-a-glance performance tracking. This partial grade data from asynchronous activities is automatically synced to the Class Records module of the School ERP, ensuring the official academic record stays current without manual data entry by the teacher.

---

## Page 12: Course Detail — Grades Tab (Student View)

**[Insert Screenshot: Student course page — Grades tab]**

The student Grades tab shows the individual student's own quiz scores, submission statuses, and overall course performance. Each row displays the quiz title, the student's score, and whether they passed or failed. Students who failed are shown their remedial quiz status. This transparency empowers students to monitor their own academic progress and identify areas needing improvement, supporting self-directed learning.

---

## Page 13: Quiz Detail Page — Quiz Information and Actions

**[Insert Screenshot: Quiz detail page — showing quiz info, questions, and take/review buttons]**

The Quiz detail page shows complete quiz information including the title, creator (with profile picture), creation date, number of questions, time limit, passing threshold, and quiz type (AI-generated or manual). For students, a "Take Quiz" button appears if the quiz has not been submitted, or a score summary is shown if already completed. For teachers, the page provides options to edit, publish/close, or review student submissions. This page serves as the central hub for quiz interaction for both user roles.

---

## Page 14: Take Quiz Page (Student View)

**[Insert Screenshot: Student taking a quiz — showing questions, timer, and submission]**

The Take Quiz page presents questions one at a time or in a scrollable list format, depending on the quiz configuration. A timer is displayed if the teacher set a time limit. Students select their answers for multiple-choice and true/false questions, or type responses for short-answer items. Upon completion, students submit the quiz for immediate automated grading. The system evaluates responses against the answer key and customizable rubrics, computes the score instantly, and determines whether the student has achieved mastery (70% or higher).

---

## Page 15: Quiz Results Page

**[Insert Screenshot: Quiz results page — showing score, pass/fail status, and question breakdown]**

After quiz submission, the Results page displays the student's score, pass/fail status, and a per-question breakdown showing which answers were correct and incorrect. This immediate feedback loop is central to the A.I.M.S. learning model. If the student fails, the mastery-lock system is triggered — the next quiz in the topic sequence becomes locked, and a remediation quiz is automatically generated and made available. This dynamic remediation process ensures students address knowledge gaps before proceeding.

---

## Page 16: AI-Powered Quiz Generation (Teacher View)

**[Insert Screenshot: Generate Quiz dialog — showing document selection, quiz type options, AI generation]**

The AI-Powered Quiz Generator allows teachers to create assessments automatically from uploaded learning materials. Teachers select a source document (PDF, DOCX, or TXT), choose the question type (multiple-choice, true/false, or short answer), set the number of questions and difficulty level, and click generate. The system uses the Google Gemini API to analyze the document content and produce curriculum-aligned questions. Generated quizzes go through a review process — teachers can edit, add, remove, or rearrange questions before publishing. This instructor validation control ensures that AI-generated content meets pedagogical standards before reaching students.

---

## Page 17: Material / Resource Detail Page

**[Insert Screenshot: Material detail page — showing file info, uploader, and download option]**

The Material detail page displays the uploaded resource's title, file name, upload date, and the uploader's name with their Google profile picture. Students and teachers can view file details and download the material for offline study. The breadcrumb navigation shows the full path: Classes > Subject (Grade Level — Section) > Material Title. This centralized digital library feature ensures all learning modules are accessible from a single organized location.

---

## Page 18: Materials / Resources Library Page

**[Insert Screenshot: Materials library page — showing all uploaded resources across courses]**

The Materials page provides a centralized view of all learning resources available to the user. For teachers, this shows all materials they have uploaded across their courses. For students, it displays materials from their enrolled courses. Resources can be browsed, searched, and accessed directly from this page, serving as the system's digital library for module distribution and management.

---

## Page 19: Schedule Page

**[Insert Screenshot: Schedule page showing class schedule]**

The Schedule page displays the user's class schedule as fetched from the Schedule module of the School ERP system. For teachers, it shows their teaching load — which subjects, sections, and time slots they are assigned to. For students, it shows their class schedule for the week. This integration is critical to the auto-enrollment feature: when a teacher is assigned to teach "English — Grade 7, Section 1" in the Schedule module, the corresponding LMS course is automatically created and both the teacher and all students in that section are enrolled without manual intervention. This seamless data flow between the ERP Schedule module and the LMS eliminates enrollment errors and administrative overhead.

---

## Page 20: Sidebar Navigation and System Layout

**[Insert Screenshot: Full page showing sidebar expanded with all navigation items]**

The sidebar navigation provides persistent access to all major system sections. The top section shows the school name and logo. Navigation items include Home, Schedule, Materials, My Quizzes (for students), Progress (for students), and teacher-specific tools. Below the navigation, the sidebar lists the user's active classes — labeled "Teaching" for teachers and "Enrolled" for students — with each class showing the subject name, grade level, and section. The bottom of the sidebar displays the current user's Google profile picture, name, and email. This layout mirrors Google Classroom's navigation paradigm, ensuring immediate familiarity for users transitioning from Google's educational tools.

---

## Page 21: Course Banner and Breadcrumb Navigation

**[Insert Screenshot: Close-up of the course banner header and breadcrumb bar]**

Each course page features a color-coded banner displaying the subject name, grade level and section, class code, and additional context (teacher name for students; enrollment count for teachers). Above the banner, the breadcrumb navigation bar shows the hierarchical path — "Classes > English (Grade 7 — 1)" — enabling one-click navigation back to the Home page. This breadcrumb system is consistent across both teacher and student views and updates dynamically based on the current page context, including nested pages like material and quiz detail views.

---

## Summary of System Objectives Achievement

| Objective | Feature Implemented | Status |
|---|---|---|
| 1.1 Centralized digital library for module distribution and management | Materials library, per-course resource uploads, material detail pages | ✅ Implemented |
| 1.2 AI-powered quiz generator with instructor validation controls | Google Gemini API integration, quiz generation from documents, teacher review/edit before publish | ✅ Implemented |
| 1.3 Automated grading module with customizable rubrics | Instant scoring on quiz submission, configurable passing thresholds, score breakdown | ✅ Implemented |
| 1.4 Mastery-lock system for automated student remediation | Sequential quiz locking on failure, auto-generated remediation quizzes, 70% mastery threshold | ✅ Implemented |
| 1.5 Student performance dashboard for real-time academic tracking | Per-student grades tab, teacher gradebook, progress tracking, submission status indicators | ✅ Implemented |

---

## ERP Module Integration Summary

The A.I.M.S. LMS does not operate in isolation — it is part of a three-module School ERP ecosystem:

1. **Schedule Module → LMS**: Class schedules, teacher assignments, and section rosters are fetched from the ERP Schedule module. The LMS uses this data to automatically create courses and enroll teachers and students, ensuring accurate and up-to-date class composition without manual intervention.

2. **LMS → Class Records Module**: Partial grades generated from asynchronous activities (online quizzes and assignments) within the LMS are automatically pushed to the ERP Class Records module. This ensures that the teacher's official class record reflects all student performance data — both from face-to-face and online activities — in a single consolidated record.

3. **Bidirectional Sync**: The three modules maintain data consistency through automatic synchronization, reducing administrative burden and ensuring accuracy across the school's academic management system.
