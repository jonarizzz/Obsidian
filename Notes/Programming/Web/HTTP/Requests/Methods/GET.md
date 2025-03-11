[[HTTP Методы (HTTP Methods)||HTTP-Метод]], который используется для запроса данных с [[Веб Сервер (Web Server)||сервера]].

- Не изменяет ресурс ([[Идемпотентность (Idempotency)]]).
- Не содержит [[Тело HTTP запроса (HTTP Request Body)||тело запроса]].
- Можно [[Кэш (Cache)||кэшировать]].


### Пример

```http
GET /api/users/123 HTTP/1.1
Host: example.com
```

Ответ:

```http
{
  "id": 123,
  "name": "Yauheni"
}
```
