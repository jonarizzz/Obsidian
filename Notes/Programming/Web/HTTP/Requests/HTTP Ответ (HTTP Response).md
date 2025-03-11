**HTTP-ответ** — это сообщение, которое [[Веб Сервер (Web Server)||сервер]] отправляет клиенту (браузеру, API-клиенту) в ответ на [[HTTP Запрос (HTTP Request)||HTTP-запрос]]. Он содержит статус выполнения запроса, заголовки и (иногда) тело с данными.


### Структура

**Статусная строка (Status Line)** – указывает версию [[HTTP (Hypertext Transfer Protocol)||HTTP]], [[Статусы ответов HTTP (HTTP Statuses)||код состояния]] и текстовое описание.

```http
HTTP/1.1 200 OK
```

**Заголовки ответа (Response Headers)** – передают метаданные.

```http
Content-Type: application/json
Content-Length: 58
Server: nginx/1.18.0
```

**Тело ответа (Response Body)** – содержит данные, если они есть.

```http
{
  "id": 123,
  "name": "Yauheni",
  "role": "admin"
}
```


### Пример

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 58
Cache-Control: no-cache
Server: nginx/1.18.0

{
  "id": 123,
  "name": "Yauheni",
  "role": "admin"
}
```


### [[Статусы ответов HTTP (HTTP Statuses)||Коды состояния HTTP-ответа (Статусы)]]

- **1xx (Информационные)** – 100 Continue
- **2xx (Успех)** – 200 OK, 201 Created
- **3xx (Перенаправление)** – 301 Moved Permanently, 302 Found
- **4xx (Ошибка клиента)** – 400 Bad Request, 401 Unauthorized, 404 Not Found
- **5xx (Ошибка сервера)** – 500 Internal Server Error, 503 Service Unavailable