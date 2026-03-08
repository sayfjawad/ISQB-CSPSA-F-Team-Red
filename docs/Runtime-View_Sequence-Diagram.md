3️⃣ Runtime View (Sequence Diagram)

Goal: Show runtime interaction between components during a scenario.

Runtime views describe dynamic behavior such as interactions and workflows.

slides-day-2

Example scenario: Student starts a lesson

PlantUML
```plantuml
@startuml
actor Student

participant "Front-end"
participant "Authentication Service"
participant "IAM System"
participant "Lesson Service"
participant "Progress Service"
database "Learning Database"

Student -> "Front-end" : Open lesson

"Front-end" -> "Authentication Service" : Validate session
"Authentication Service" -> "IAM System" : Verify token
"IAM System" --> "Authentication Service" : OK

"Front-end" -> "Lesson Service" : Request lesson content
"Lesson Service" -> "Learning Database" : Load lesson
"Learning Database" --> "Lesson Service" : Lesson data

"Lesson Service" --> "Front-end" : Lesson content

Student -> "Front-end" : Complete lesson

"Front-end" -> "Progress Service" : Save progress
"Progress Service" -> "Learning Database" : Store progress

@enduml

```
**Scenario flow**

    Student opens lesson
    
    System authenticates via IAM
    
    Lesson content retrieved
    
    Student completes lesson
    
    Progress stored