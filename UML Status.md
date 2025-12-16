@startuml
skinparam BackgroundColor #F8F9FA
skinparam StateBackgroundColor #E8F5E8
skinparam StateBorderColor #2E7D32
skinparam StateArrowColor #2E7D32
skinparam Shadowing false

top to bottom direction

title Диаграмма состояний заказа на автомойке

state "ЧЕРНОВИК" as draft
state "ОФОРМЛЕН" as created
state "РЕДАКТИРУЕТСЯ" as editing
state "ВЫПОЛНЕН" as completed
state "ОПЛАЧЕН" as paid
state "ЗАВЕРШЕН" as finished
state "ОТМЕНЕН" as cancelled

[*] --> draft

draft --> created : Подтверждение клиентом

created --> editing : Изменение данных
created --> completed : Начало выполнения
created --> paid : Оплата
created --> cancelled : Отмена

editing --> created : Сохранение изменений
editing --> cancelled : Отмена редактирования

completed --> paid : Требуется оплата
completed --> finished : Услуга оказана

paid --> finished : Завершение обслуживания

note right of draft
  Первоначальное состояние
  заказа
end note

note left of created
  Заказ подтвержден
  и ожидает выполнения
end note
@enduml

<img width="726" height="689" alt="image" src="https://github.com/user-attachments/assets/6bd00e1b-01d2-4746-b57c-b54903028275" />
