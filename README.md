# PlanZajecUML

Uni project for pcz

```mermaid
---
title: Class system diagram
---
classDiagram
    class WeekDay {
        <<enumeration>>
        MONDAY
        TUESDAY
        WEDNESDAY
        THURSDAY
        FRIDAY
        SATURDAY
        SUNDAY
    }

    class Student {
        +int id
        +String name
        +String surname
        +String email
        +viewSchedule()
    }

    class Teacher {
        +int id
        +String name
        +String surname
        +String email
        +String phoneNumber
        +String subjectSpecialization
        +List~Class~ assignedClasses
        +viewSchedule()
        +assignClasses(Class newClass)
        +markAttendance(Class class, Student student)

    }

    class Administrator {
        +int id
        +String name
        +String surname
        +String email
        +String phoneNumber
        +createSchedule()
        +modifySchedule()
        +assignTeacherToClass(Teacher teacher, Class class)
        +assignRoomToClass(Class class, Room room)
        +viewAllSchedules()
    }

    class Schedule {
        +int scheduleId
        +List~Class~ classes
        +addClass(Class newClass)
        +removeClass(Class class)
        +modifyClass(Class class, Room newRoom)
        +viewSchedule()
    }

    class Class {
        +WeekDay Day
        +int classId
        +String subject
        +List~Student~ enrolledStudents
        +Teacher teacher
        +Double StartTime
        +Double Duration
        +Room room
        +addStudent(Student student)
        +removeStudent(Student student)
        +viewClassDetails()
        +updateClassTime(Double StartTime, Double Duration)
        +updateClassDay(WeekDay Day)
        +assignRoom(Room newRoom)
    }

    class Room {
        +int roomId
        +String location
        +int capacity
                +viewRoomSchedule()
    }

    Student --> Schedule : "views"
    Teacher --> Schedule : "views and assigns"
    Administrator --> Schedule : "creates and modifies"
    Schedule --> Class : "contains"
    Class --> Room : "assigned to"
    WeekDay --> Class : "uses"
```

note: W systemie znajdują się następujące typu kont: Teacher , Student , Administrator o różnych poziomach uprawnień. Student odpowiadający uczniom o najbardziej ograniczonym dostępie może tylko i wyłącznie obejrzec już utworzony i zaakceptowany plan zajęć. Teacher odpowiadający wykładowcom poza oczywistym obejrzeniem planu zajęć ma możliwość dodania pod siebie nowej klasy oraz zaznaczania obecności uczniów. 


```mermaid
sequenceDiagram
    participant Admin as Administrator
    participant Sched as Schedule
    participant Cls as Class

    Admin->>Sched: createSchedule()
    Sched->>Cls: addClass(class details)
    Cls-->>Sched: confirmClassAdded()
    Sched-->>Admin: scheduleCreated()
```

tutaj pokaż przykład zastosowań jeśli chcesz dodać jakieś jeszcze by lepiej pokazać użycie tego "systemu" napisz klazule 
```
'''mermaid
<opis co ma być wykonane>
'''
```

Made by:
Łukasz Stajkowski
