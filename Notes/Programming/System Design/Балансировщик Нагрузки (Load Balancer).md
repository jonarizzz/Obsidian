**Балансировщик нагрузки** — это система, которая распределяет входящий трафик между несколькими [[Веб Сервер (Web Server)||серверами]], чтобы повысить отказоустойчивость и производительность.


### Как работает

1. Клиент отправляет [[HTTP Запрос (HTTP Request)||запрос]] на балансировщик.
2. Балансировщик перенаправляет запрос на один из доступных [[Веб Сервер (Web Server)||серверов]].
3. [[Веб Сервер (Web Server)||Сервер]] обрабатывает [[HTTP Запрос (HTTP Request)||запрос]] и возвращает [[HTTP Ответ (HTTP Response)||ответ]] через балансировщик.


### Типы балансировки

- **L4 (Сетевой, Transport Layer)** — балансировка на уровне [[TCP||TCP]]/[[UDP||UDP]] ([[IP Адрес (Internet Protocol Address, IP Address)||IP-адреса]], порты).
- **L7 (Прикладной, Application Layer)** — балансировка на уровне [[HTTP (Hypertext Transfer Protocol)||HTTP]]/[[HTTPS (Hypertext Transfer Protocol Secure)||HTTPS]] ([[HTTP Заголовки (HTTP Headers)||заголовки]], [[{TODO} Cookie||куки]], [[URL (Uniform Resource Locator)||URL]]).


### Алгоритмы распределения трафика

- **Round Robin** — [[HTTP Запрос (HTTP Request)||запросы]] равномерно отправляются по кругу.
- **Least Connections** — выбирается [[Веб Сервер (Web Server)||сервер]] с наименьшей нагрузкой.
- **IP Hash** — назначает сервер в зависимости от [[IP Адрес (Internet Protocol Address, IP Address)||IP]] клиента.


### Где используется

- В [[Микросервис (Microservice)||микросервисах]] (распределение нагрузки между [[{TODO} Docker Container||контейнерами]]).
- В [[Веб Приложение (Web Application)||веб-приложениях]] (направление трафика на несколько [[Веб Сервер (Web Server)||серверов]]).
- В облачных сервисах (AWS ELB, Nginx, HAProxy, Cloudflare).