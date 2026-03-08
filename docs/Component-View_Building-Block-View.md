2️⃣ Component View (Building Block View)

Goal: Show internal structure of the e-learning system.

The building block view decomposes the system into components and their dependencies.

slides-day-2

PlantUML
![Architecture](Component-View_Building-Block-View.png)
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

**Components explained**

    Component	            Responsibility
    Front-end	            UI for students and teachers
    Authentication service	    login and IAM integration
    Course service	            manage courses
    Lesson service	            deliver lesson content
    Assessment service	    quizzes/tests
    Progress service	    track student progress
    Teacher dashboard	    teacher overview
    Group service	            manage classes/groups