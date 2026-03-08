# ISQB-CSPSA-F-Team-Red
Some fun exercise workouts of Team Red.

## Exercise 5: Create Three Views

This section presents three architectural views of the e-learning system: Context View, Component (Building Block) View, and Runtime View. These views provide different perspectives on the system's architecture, scope, and behavior.

### 1. Context View (System Context)

**Goal:** Show the e-learning system as a black box and its interactions with external actors and systems. It defines the system scope and external interfaces.

![Context View](docs/Context-View_System-Context.png)

```plantuml
@startuml
skinparam componentStyle rectangle

actor Student
actor Teacher
actor Admin
actor Author

component "E-learning System" as ELS
component "IAM System" as IAM
component "CMS (Content Management System)" as CMS
component "School System / LMS" as LMS

Student --> ELS : follow lessons\nsubmit assessments
Teacher --> ELS : monitor progress\nmanage courses
Admin --> ELS : manage users\nmanage groups
Author --> CMS : create learning content

CMS --> ELS : publish course content
ELS --> IAM : authenticate users
IAM --> ELS : provide identity/token

LMS --> ELS : open course
ELS --> LMS : progress updates
@enduml
```

**What this diagram shows:**
* **The E-learning system**
* **External actors:** Student, Teacher, Admin, Author.
* **External systems:** IAM system, CMS, School/LMS system.

This represents the business context of the system.

---

### 2. Component View (Building Block View)

**Goal:** Show the internal structure of the e-learning system by decomposing it into components and their dependencies.

![Component View](docs/Component-View_Building-Block-View.png)

```plantuml
@startuml
skinparam componentStyle rectangle

package "E-learning System" {

component "Front-end Web App" as FE

component "Authentication Service"
component "Course Service"
component "Lesson Service"
component "Assessment Service"
component "Progress Service"
component "Group Service"
component "Teacher Dashboard Service"

database "Learning Database"

FE --> "Authentication Service"
FE --> "Course Service"
FE --> "Lesson Service"
FE --> "Assessment Service"
FE --> "Teacher Dashboard Service"

"Course Service" --> "Lesson Service"
"Assessment Service" --> "Progress Service"
"Lesson Service" --> "Progress Service"

"Teacher Dashboard Service" --> "Progress Service"
"Teacher Dashboard Service" --> "Group Service"

"Course Service" --> "Learning Database"
"Lesson Service" --> "Learning Database"
"Assessment Service" --> "Learning Database"
"Progress Service" --> "Learning Database"
"Group Service" --> "Learning Database"

}

@enduml
```

**Components Explained:**

| Component | Responsibility |
| :--- | :--- |
| **Front-end** | UI for students and teachers |
| **Authentication service** | Login and IAM integration |
| **Course service** | Manage courses |
| **Lesson service** | Deliver lesson content |
| **Assessment service** | Quizzes/tests |
| **Progress service** | Track student progress |
| **Teacher dashboard** | Teacher overview |
| **Group service** | Manage classes/groups |

---

### 3. Runtime View (Sequence Diagram)

**Goal:** Show runtime interaction between components during a specific scenario.

**Example scenario:** Student starts a lesson

![Runtime View](docs/Runtime-View_Sequence-Diagram.png)

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

**Scenario Flow:**
1. Student opens lesson.
2. System authenticates via IAM.
3. Lesson content is retrieved.
4. Student completes lesson.
5. Progress is stored.
