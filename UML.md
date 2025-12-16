@startuml
skinparam monochrome true
skinparam shadowing false

left to right direction
actor "Клиент" as Client
actor "Директор" as Director

rectangle "Система CarWasher" {
usecase "US_A01: Регистрация в системе" as Register
usecase "Верификация номера телефона" as PhoneConfirm
usecase "Ошибка верификации" as PhoneError

usecase "US_S01: Поиск автомойки" as CarWashChoice
usecase "Указание города" as CityChoice
usecase "Выбор адреса мойки" as AddressChoice
usecase "Поиск по названию" as SearchChoice

usecase "US_P01: Оплата услуг" as PaymentService
usecase "Процесс оплаты" as Payment
usecase "Выбор платежного метода" as PaymentMethod

usecase "US_M01: Аналитика работы" as Statistics
usecase "Визуализация статистики" as Graphs
usecase "Экспорт отчетов" as CSVExport
}

rectangle "СМС сервис" as SMS
rectangle "Платежный шлюз" as PaySystem
rectangle "Бухгалтерия 1С" as System1C

' Регистрация
Client --> Register
Register ..> PhoneConfirm : включает
Register ..> PhoneError : расширяет при ошибке
PhoneConfirm --> SMS

' Поиск мойки
Client --> CarWashChoice
CarWashChoice --> CityChoice : начинается с
CarWashChoice --> AddressChoice : или выбор из списка
CarWashChoice --> SearchChoice : или поиск

' Оплата
Client --> PaymentService
PaymentService --> Payment : основной процесс
PaymentService --> PaymentMethod : выбор способа
Payment --> PaySystem : интеграция
Payment --> System1C : синхронизация

' Аналитика
Director --> Statistics
Statistics --> Graphs : визуальное представление
Statistics --> CSVExport : данные для выгрузки

note right of Register
Регистрация с подтверждением
номера телефона
end note

note left of Statistics
Статистика по мойщикам
и эффективности работы
end note
@enduml
