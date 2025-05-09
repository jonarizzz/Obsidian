**API Gateway** — компонент, управляющий входящими [[HTTP Запрос (HTTP Request)||запросами]] к [[Микросервис (Microservice)||микросервисам]], обеспечивающий [[Маршрутизация (Routing)||маршрутизацию]], безопасность и оптимизацию взаимодействия между клиентами и сервисами.


### Основные характеристики

- **[[Маршрутизация (Routing)||Маршрутизация запросов]]**: API Gateway направляет [[HTTP Запрос (HTTP Request)||запросы]] клиентов к соответствующим [[Микросервис (Microservice)||микросервисам]] в зависимости от пути, метода и других параметров [[HTTP Запрос (HTTP Request)||запроса]].
- **Агрегация запросов**: Объединяет данные от нескольких [[Микросервис (Microservice)||микросервисов]] в одном [[HTTP Ответ (HTTP Response)||ответе]] для упрощения взаимодействия с клиентом.
- **Безопасность**: Обеспечивает [[Аутентификация (Authentication)||аутентификацию]], [[Авторизация (Authorization)||авторизацию]] и защиту от угроз, таких как DDoS-атаки.
- **Трансформация данных**: Может изменять формат данных или [[Протокол (Protocol)||протоколы]] при передаче между клиентами и [[Микросервис (Microservice)||микросервисами]].
- **[[Мониторинг (Monitoring)||Мониторинг]] и логирование**: Служит точкой мониторинга для отслеживания производительности и [[Логирование (Logging)||логирования]] [[HTTP Запрос (HTTP Request)||запросов]] и [[HTTP Ответ (HTTP Response)||ответов]].


### Принципы работы

- Клиенты отправляют [[HTTP Запрос (HTTP Request)||запросы]] на API Gateway.
- API Gateway анализирует [[HTTP Запрос (HTTP Request)||запрос]] и направляет его к нужному [[Микросервис (Microservice)||микросервису]].
- [[Микросервис (Microservice)||Микросервисы]] обрабатывают [[HTTP Запрос (HTTP Request)||запросы]] и возвращают ответ через API Gateway.


### Преимущества

- **Упрощение взаимодействия**: Клиенты взаимодействуют только с одним точечным входом (API Gateway), а не с каждым [[Микросервис (Microservice)||сервисом]] по отдельности.
- **Снижение нагрузки на [[Микросервис (Microservice)||микросервисы]]**: API Gateway обрабатывает кросс-сервисные задачи (например, [[Аутентификация (Authentication)||аутентификацию]], [[Логирование (Logging)||логирование]]), освобождая [[Микросервис (Microservice)||микросервисы]] от этих обязанностей.
- **Масштабируемость**: Легко добавлять новые [[Микросервис (Microservice)||сервисы]] без изменений на стороне клиента, просто обновив маршруты в API Gateway.
- **Управление трафиком**: API Gateway может [[Балансировщик Нагрузки (Load Balancer)||балансировать нагрузку]], ограничивать частоту [[HTTP Запрос (HTTP Request)||запросов]] и обрабатывать ошибки.

