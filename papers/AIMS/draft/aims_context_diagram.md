```mermaid
flowchart LR
    classDef entity fill:#ffffff,stroke:#000000,stroke-width:2px;
    classDef process fill:#ffffff,stroke:#000000,stroke-width:2px;

    %% External Entities
    teacher[Teacher]
    student[Student]

    %% Central Process (Level 0)
    aims((0<br><br>A.I.M.S. System))

    %% Apply Classes
    class teacher,student entity;
    class aims process;

    %% Data Flows: Teacher (Left) <-> AIMS (Center)
    teacher -->|Learning Materials & Quiz Configs| aims
    teacher -->|Subjective Grades & Remedial Approvals| aims
    teacher -->|Mastery Lock Overrides| aims
    
    teacher <..|Generated AI Quiz Drafts| aims
    teacher <..|Student Performance & Analytics| aims

    %% Data Flows: AIMS (Center) <-> Student (Right)
    aims -->|Learning Materials & Assessments| student
    aims -->|Mastery Status & Final Grades| student
    
    aims <..|Completed Tasks & Quiz Answers| student
```