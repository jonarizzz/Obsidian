**Отказоустойчивость (Fault Tolerance)** — это способность системы продолжать работать корректно, даже если в ней происходят сбои (отказы отдельных компонентов).


### Ключевые аспекты

- **Избыточность (Redundancy)** — дублирование критически важных компонентов (серверов, дисков, сетевых подключений).
- **Обнаружение отказов** — [[Мониторинг (Monitoring)||мониторинг]] состояния системы и выявление проблем.
- **Автоматическое восстановление** — переключение на резервные ресурсы (например, реплицированные базы данных).
- **Деградация вместо полного отказа** — частичная потеря функциональности, но не полный выход системы из строя.  


### Примеры

- **RAID-массивы** — сохраняют данные, даже если выходит из строя один или несколько дисков.
- **Кластеры серверов** — если один сервер выходит из строя, нагрузка перераспределяется на другие.
- **[[Микросервис (Microservice)||Микросервисная архитектура]]** — сбой одного сервиса не останавливает всю систему.
- **[[Репликация Базы Данных (Database Replication, DB Replication)||Репликация баз данных]]** — если один сервер [[База данных (БД, Database, DB)||базы данных]] недоступен, запросы перенаправляются на реплику.