# Диаграмма вариантов использования

Составьте диаграмму вариантов использования. Выделите действующие лица, расставьте связи, не забудьте внешние системы, которые требуется учесть.

```plantuml
@startuml
skinparam actorStyle awesome
left to right direction
actor "Ресторанный критик" as fc
rectangle Ресторан {
usecase "Есть" as UC1
usecase "Платить" as UC2
usecase "Пить" as UC3
usecase "Составлять отзыв" as UC4
}
fc --> UC1
fc --> UC2
fc --> UC3
fc --> UC4
@enduml
```

```plantuml
@startuml
actor Гость as g
package Специалисты {
  actor "Шеф повар" as c
  actor "Ресторанный критик" as fc
}
package Ресторан {
  usecase "Есть" as UC1
  usecase "Платить" as UC2
  usecase "Пить" as UC3
  usecase "Составлять отзыв" as UC4
}
fc --> UC1
fc --> UC2
fc --> UC3
fc --> UC4
g --> UC1
g --> UC2
g --> UC3
@enduml

```


<code-block lang="plantuml" collapsible="true" src="RegistryNotificationService.puml">

</code-block>