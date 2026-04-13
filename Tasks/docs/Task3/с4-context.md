
```puml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

Person(customer, "Клиент", "Посетитель сайта / Пользователь интернет-банка")
Person(cc_manager, "Менеджер кол-центра", "Подтверждает заявки с сайта")
Person(backoffice, "Сотрудник бэк-офиса депозитов", "Обрабатывает заявки на депозиты")

System(site, "Сайт банка", "PHP/React")
System(ib, "Интернет-банк", "ASP.NET MVC")
System(cc_system, "Система кол-центра", "Java/React")
System(abs, "АБС", "Delphi/Oracle")
System_Ext(sms, "СМС-шлюз", "Отправка уведомлений")

Rel(customer, site, "Просматривает депозиты, подаёт заявку", "HTTPS")
Rel(site, cc_system, "Передаёт заявку с контактами", "REST API")
Rel(cc_manager, cc_system, "Просматривает заявки, подтверждает", "Веб-интерфейс")
Rel(cc_system, abs, "Передаёт подтверждённую заявку", "Очередь / REST API")
Rel(customer, ib, "Просматривает персональные ставки, подаёт заявку с СМС", "HTTPS")
Rel(ib, abs, "Регистрирует заявку из интернет-банка", "Очередь / REST API через сервис")
Rel(backoffice, abs, "Обрабатывает заявки, подтверждает ставки", "Десктоп-клиент")
Rel(abs, sms, "Отправляет СМС о статусе заявки", "HTTP/SMPP")
@enduml
```