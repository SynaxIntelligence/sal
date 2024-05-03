# Диаграмма вариантов использования

Диаграмма вариантов использования представляет собой графическое описание основных функций мобильного приложения для планирования и организации посещения музеев и выставок.

```plantuml
@startuml
skinparam linetype ortho
skinparam actorStyle awesome
skinparam ArrowFontSize 12
skinparam UsecaseFontSize 12
skinparam Shadowing false

left to right direction
:Пользователь: as User
:Администратор приложения: as Admin

rectangle Musemium {
    usecase "Заполнить поле" as uc_common_1
    usecase "Зарегистрироваться" as uc_reg_1
    usecase "Зарегистрироваться через соцсети" as uc_reg_2
    usecase "Авторизоваться" as uc_auth_1
    usecase "Авторизоваться через соцсети" as uc_auth_2
    usecase "Заполнить профиль" as uc_prof_1
    usecase "Добавить фото к профилю" as uc_prof_2
    usecase "Загрузить файл на сервис" as uc_prof_2.1
    usecase "Редактировать профиль" as uc_prof_3
    usecase "Удалить аккаунт" as uc_acc_1
    usecase "Просмотреть список музеев" as uc_museum_1
    usecase "Просмотреть подробную информацию о музее" as uc_museum_2
    usecase "Запланировать посещения музея" as uc_museum_3
    usecase "Прикрепить билеты к посещению" as uc_tckt_1    
    usecase "Создать чек-лист/заметку о посещении" as uc_chcklst_1
    usecase "Добавить экспонаты к чеклисту" as uc_chcklst_2
    usecase "Изменить статус пункта в чеклисте" as uc_chcklst_3
    usecase "Рассчитать маршрут" as uc_route_1    
}

uc_auth_1 <-. uc_auth_2: <<расширяет>>
uc_reg_1 <-. uc_reg_2: <<расширяет>>
uc_prof_2 .-> uc_prof_2.1: <<включает>>
uc_prof_1 .-> uc_common_1: <<включает>>
uc_prof_3 .-> uc_common_1: <<включает>>
uc_chcklst_1 <-. uc_chcklst_2: <<расширяет>>
uc_chcklst_1 <--. uc_chcklst_3: <<расширяет>>
uc_museum_1 <-. uc_museum_2: <<расширяет>>
uc_museum_3 <--. uc_route_1: <<расширяет>>
uc_museum_3 <--. uc_chcklst_1: <<расширяет>>

User --> uc_auth_1
User --> uc_reg_1
User --> uc_prof_1
User --> uc_prof_2
User --> uc_acc_1
User --> uc_museum_1
User --> uc_museum_2
User --> uc_museum_3
User --> uc_tckt_1
User --> uc_chcklst_1
User --> uc_route_1

Admin --> uc_auth_1

'Employee --> Просмотр списка музеев
'Employee --> Просмотр подробной информации о музее
'Employee --> Планирование посещения музея
'
'Admin --> Авторизация в приложении
'Admin --> Регистрация нового пользователя
'Admin --> Просмотр списка музеев
'Admin --> Просмотр подробной информации о музее
'Admin --> Планирование посещения музея
'Admin --> Прикрепление билетов к посещению
'Admin --> Создание чек-листа/заметки о посещении
'Admin --> Просмотр ленты новостей о выставках
'Admin --> Просмотр запланированных визитов
@enduml
```

[//]: # ()
[//]: # (<code-block lang="plantuml" collapsible="true" src="RegistryNotificationService.puml">)

[//]: # ()
[//]: # (</code-block>)
