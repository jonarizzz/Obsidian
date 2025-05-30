**Кэш** — это механизм временного хранения часто используемых данных для ускорения доступа к ним и снижения нагрузки на систему.


### Как работает

При первом запросе данные загружаются и сохраняются в кэше. При последующих запросах система использует уже сохраненные данные, вместо того чтобы загружать их заново.


### Где используется

- **Процессоры (CPU Cache)** — хранит часто используемые команды и данные для быстрого доступа.
- **[[{TODO} Операционная Система (ОС, Operating System, OS)||Операционная система]] (Disk Cache, RAM Cache)** — ускоряет работу с жестким диском.
- **Браузеры (Browser Cache)** — сохраняют веб-страницы, изображения, стили для быстрого повторного открытия.
- **CDN (Content Delivery Network)** — кешируют контент на серверах, ближе к пользователям.
- **[[База данных (БД, Database, DB)||Базы данных]] (Query Cache)** — сохраняют результаты запросов для ускорения работы.


### Плюсы

- Уменьшает задержки.
- Снижает нагрузку на сеть и серверы.
- Повышает производительность системы.


### Минусы

- Может устаревать, вызывая несоответствия данных.
- Требует дополнительной памяти для хранения.
- Иногда требует ручной очистки (например, в браузерах).