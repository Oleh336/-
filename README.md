@startuml
!define RECTANGLE class

[*] --> Idle : Запуск програми

state Idle {
    [*] --> Ready : Програма запущена
    Ready --> ConfigurationMode : Вибір "Налаштування"
}

Idle --> EditingEnvironment : Відкриття або створення документа

state EditingEnvironment {
    [*] --> Loading : Завантаження документа
    Loading --> Interactive : Завантаження завершено

    state Interactive {
        [*] --> Editing : Початок редагування тексту
        Editing --> ContentManagement : Вибір об’єкта
        ContentManagement --> Editing : Завершення роботи з об’єктом
        Editing --> Collaboration : Спільне редагування
        Collaboration --> Editing : Завершення спільного редагування
    }

    Interactive --> ConfigurationMode : Перехід до налаштувань
    Interactive --> Idle : Завершення роботи з документом
}

state ConfigurationMode {
    [*] --> AppSettings : Загальні налаштування програми
    AppSettings --> DocumentPreferences : Параметри документа
    DocumentPreferences --> UserPreferences : Налаштування інтерфейсу
    UserPreferences --> AppSettings : Повернення до загальних налаштувань
}

ConfigurationMode --> Idle : Повернення до очікування
@enduml
 
