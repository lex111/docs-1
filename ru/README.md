# Введение

**GraphQL** — это современная замена, в некотором роде, устаревшего подхода 
**REST** в разработке API. Прошло почти 17 лет с момента, когда идея **REST** была 
разработана Роем Филдингом в 2000 году. И со всей любовью ко всему, что было сделано
с помощью **REST**, пришло время изменить что-то в лучшую сторону.
 
**GraphQL** является шагом в будущее во многих отношениях и имеет фундаментальные 
улучшения над старым добрым **REST**:

- Базовая проверка типов, встроенная на уровне архитектуры ПО.
- Переиспользуемый **API** для разных клиентов и устройств, 
т.е. нет необходимости в поддержке `/v1`, `/v2` или `/v10002545.07E20`.
- Совершенно новый уровень абстракции между логикой _backend_ и _frontend_.
- Автогенерируемая документация и интуитивный способ изучения нового **API**.
- После завершения архитектуры проекта – большинство "клиентских" модификаций не потребует изменения "бэкенда".

В это может быть трудно поверить, но стоит просто попробовать и вы будете вознаграждены гораздо лучшей архитектурой, 
и гораздо легче поддерживаемым кодом.

Сервис **GraphQL** создается путем определения типов и полей в этих типах, 
а затем предоставления функций для каждого поля и для каждого определённого типа.

**Railt**, в свою очередь, предоставляет возможность [описания схемы](/sdl) и [обработки запросов](/http).
