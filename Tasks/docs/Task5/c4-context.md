@startuml title DepositService-CallServiceIntegration Context Diagram

!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

Person(customer, "Клиент", "Подаёт заявку на кредит онлайн")
Person(front_manager, "Сотрудник отделения", "Работает с заявкой в АБС")
Person(back_manager, "Сотрудник бэк-офиса кредитов", "Обрабатывает заявки в Кредитном конвейере")

System(site, "Сайт банка", "PHP/React")
System(ib, "Интернет-банк", "ASP.NET MVC")
System(credit_service, "Сервис кредитных заявок", "Java Spring Boot")
System(abs, "АБС", "Delphi/Oracle")
System(conveyor, "Кредитный конвейер", "Camunda/Java")
System(scoring, "Система кредитного скоринга", "Python/Flask")
System_Ext(bki, "Бюро кредитных историй", "Внешняя система")
System_Ext(sms, "СМС-шлюз", "Отправка уведомлений")

Rel(customer, site, "Просмотр предложений, подача заявки", "HTTPS")
Rel(site, credit_service, "Отправка заявки", "REST API")
Rel(customer, ib, "Просмотр предодобренных предложений, подача заявки", "HTTPS")
Rel(ib, credit_service, "Получение предложений, отправка заявки", "REST API")
Rel(credit_service, scoring, "Запрос скоринга", "REST API")
Rel(scoring, bki, "Получение кредитной истории", "REST API")
Rel(credit_service, conveyor, "Передача заявки для бэк-офиса", "REST API (или Kafka)")
Rel(credit_service, abs, "Регистрация заявки для отделения", "Kafka")
Rel(front_manager, abs, "Просмотр заявки", "Десктоп-клиент")
Rel(back_manager, conveyor, "Обработка заявки", "Веб-интерфейс")
Rel(credit_service, sms, "Отправка СМС", "HTTP")
Rel(conveyor, sms, "Отправка СМС", "HTTP")

@enduml