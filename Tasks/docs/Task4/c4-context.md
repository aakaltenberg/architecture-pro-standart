```puml
@startuml title DepositService-CallServiceIntegration Context Diagram

!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

Person(cc_operator, "Сотрудник кол-центра банка")
Person(partner_operator, "Сотрудник партнёрского кол-центра")

System(cc_system, "Система кол-центра", "Java/React")
System(deposit_service, "Сервис депозитных ставок", "Java Spring Boot")

System_Ext(partner_cc, "Система партнёрского кол-центра", "Внешняя")
System_Ext(sftp, "SFTP-сервер банка", "Хранение файлов для партнёра")

Rel(cc_operator, cc_system, "Просматривает ставки", "Веб-интерфейс")
Rel(cc_system, deposit_service, "Запрашивает актуальные ставки", "REST API (HTTPS)")
Rel(deposit_service, sftp, "Выгружает файл ставок", "SFTP")
Rel(partner_operator, partner_cc, "Использует", "Веб-интерфейс")
Rel(partner_cc, sftp, "Забирает файл ставок", "SFTP")

@enduml
```