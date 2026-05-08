# A.I.M.S. Use Case Diagram

This use case diagram is derived from the current A.I.M.S. paper revision and the defined system behavior in Chapter 1 and Chapter 2.

```mermaid
flowchart LR
    classDef actor fill:#ffffff,stroke:#000000,color:#000000;
    classDef usecase fill:#ffffff,stroke:#000000,color:#000000;
    classDef boundary fill:#ffffff,stroke:#000000,color:#000000;

    teacher[Teacher]
    student[Student]

    subgraph aims[A.I.M.S.]
        direction TB
        uc1([Upload Learning Materials])
        uc2([Access Learning Materials])
        uc3([Submit Completed Tasks])
        uc4([Generate AI Quiz Draft])
        uc5([Review and Publish Quiz])
        uc6([Take Quiz Assessment])
        uc7([Validate Subjective Responses])
        uc8([View Final Grades])
        uc9([Review and Approve Remedial Quiz])
        uc10([Take Remedial Quiz])
        uc11([Configure Mastery Locks])
        uc12([Override Progression Lock])
    end

    class teacher,student actor;
    class uc1,uc2,uc3,uc4,uc5,uc6,uc7,uc8,uc9,uc10,uc11,uc12 usecase;
    class aims boundary;

    teacher --- uc1
    teacher --- uc4
    teacher --- uc5
    teacher --- uc7
    teacher --- uc9
    teacher --- uc11
    teacher --- uc12

    uc2 --- student
    uc3 --- student
    uc6 --- student
    uc8 --- student
    uc10 --- student
```

This version follows the sample format more closely:

- Actors are placed outside the system boundary.
- Use cases are grouped inside a single A.I.M.S. system box.
- The use cases are written at a higher level so the diagram stays readable in a thesis document.
- Only the two primary actors from the paper, Teacher and Student, are shown.
- The process labels are kept generic and major-process oriented rather than feature-by-feature.