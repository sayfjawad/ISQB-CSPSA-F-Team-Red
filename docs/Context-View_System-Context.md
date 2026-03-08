1️⃣ Context View (System Context)

Goal: Show the e-learning system as a black box and its interactions with external actors and systems.
A context view shows the system scope and external interfaces.

slides-day-2

PlantUML
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

**What this diagram shows**

The E-learning system

External actors:

    Student
    
    Teacher
    
    Admin
    
    Author

External systems:

    IAM system
    
    CMS
    
    School/LMS system

This is the business context of the system.