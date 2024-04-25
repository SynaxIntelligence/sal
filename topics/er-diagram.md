# Диаграмма ER

## Концептуальная модель данных

```plantuml
@startuml

entity User {
    + ID : int
    + Name : string
    + Email : string
    + PasswordHash : string
    + ProfileData : string
}

entity Museum {
    + ID : int
    + Name : string
    + Address : string
    + City : string
    + Website : string
    + OpeningHours : string
}

entity Exhibition {
    + ID : int
    + Name : string
    + StartDate : date
    + EndDate : date
}

entity Artwork {
    + ID : int
    + Name : string
    + Description : string
    + Author : string
    + Year : int
}

entity Ticket {
    + ID : int
    + Type : string
    + Price : float
    + VisitDateTime : datetime
}

entity ChecklistNote {
    + ID : int
    + Text : string
    + CreatedDate : datetime
}

entity News {
    + ID : int
    + Title : string
    + Text : string
    + PublicationDate : datetime
}

User --|{ Ticket
User --|{ ChecklistNote

Museum ||--o{ Exhibition
Exhibition }o--|| Artwork
Museum ||--o{ News

@enduml

```

```plantuml
@startuml

skinparam class {
    BackgroundColor White
    BorderColor Black
}

rectangle "User" {
    rectangle "Auth" as Auth {
    }
}

rectangle "Museum" {
    rectangle "Info" as Info {
    }
}

rectangle "Plan" as Plan {
}

rectangle "Ticket" as Ticket {
}

rectangle "Checklist" as Checklist {
}

rectangle "News" as News {
}

rectangle "Exhibition" as Exhibition {
}

rectangle "Artwork" as Artwork {
}

rectangle "User" --* Auth
User --* Plan
User --* Checklist
User --* Ticket
Museum --* Info
Museum --* Exhibition
Exhibition --* Artwork
Museum --* News

@enduml

```

### В данной ER-диаграмме:

* User представляет пользователей приложения.
* SocialAccount содержит информацию о социальных аккаунтах пользователей.
* MuseumVisit отображает посещения музея пользователями.
* Museum представляет музеи.
* Ticket содержит информацию о билетах на посещение музея.
* Checklist позволяет пользователям создавать заметки и чек-листы о посещении музея.
* ExhibitionNews содержит информацию о новостях выставок в музеях.
