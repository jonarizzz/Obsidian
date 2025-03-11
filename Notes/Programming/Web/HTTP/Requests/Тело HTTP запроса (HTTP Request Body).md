**Тело HTTP-запроса (HTTP Request Body)** — это часть [[HTTP Запрос (HTTP Request)||запроса]], содержащая данные, которые клиент (например, браузер или API-клиент) отправляет на [[Веб Сервер (Web Server)||сервер]]. Оно присутствует только в некоторых типах запросов, таких как [[POST||POST]], [[PUT||PUT]], [[PATCH||PATCH]], а в [[GET||GET]] запросах отсутствует.


### Ключевые моменты

- **Содержимое:** Может включать [[{TODO} JSON||JSON]], [[{TODO} XML||XML]], данные форм (`application/x-www-form-urlencoded`), [[{TODO} Файл (File)||файлы]] (`multipart/form-data`) и другие форматы.
- **[[HTTP Заголовки (HTTP Headers)||Заголовки]]:** Формат тела указывается в [[HTTP Заголовки (HTTP Headers)||заголовке]] `Content-Type`, а его размер — в `Content-Length`.
- **Обработка:** [[Веб Сервер (Web Server)||Сервер]] парсит тело запроса в зависимости от `Content-Type` и выполняет соответствующие действия.


### Пример

```http
POST /api/user HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 38

{
  "name": "Yauheni",
  "age": 30
}
```