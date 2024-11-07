# PlanZajecUML

W systemie znajdują się następujące typy kont:

- `Teacher`
- `Student`
- `Administrator`

Każde konto ma różne poziomy uprawnień.

`Student` odpowiadający uczniom o najbardziej ograniczonym dostępie może tylko i wyłącznie obejrzeć już utworzony i zaakceptowany plan zajęć. 

`Teacher` odpowiadający wykładowcom poza oczywistym obejrzeniem planu zajęć ma możliwość dodania pod siebie nowej klasy oraz zaznaczania obecności uczniów. 

`Administrator` całego systemu posiada nieograniczone możliwości w edycji, aktualizacji i usuwaniu planu oraz przynależności wykładowców do danych zajęć. 

Za to klasy odpowiadające wykładowi - `Class` , sali wykładowej - `Room` oraz planu zajęć - `Shedule` posiadają również niezbędne elementy funkcyjne. 

`Room` zawiera informacje o pojemności i lokalizacji sali oraz moze wyświetlić indywidualny plan jakie zajęcie się w niej odbywają. 

`Class` zawiera między innymi informacje o czasie trwania zajęć i miejscu, dniu w którym one się odbywają przy pomocy enumeratora `WeekDay` oraz listę studentów uczeszczających na zajęcia i wykładowcę prowadzącego te zajęcia. Daje ona możliwość zmiany terminu odbywania się zajęć i miejsca , aktualizację aktywnych studentów oraz wyświetlenia szczegółowych danych o zajęciach.

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

<>...>

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

Made by:
Łukasz Stajkowski, Mateusz Bryniak
