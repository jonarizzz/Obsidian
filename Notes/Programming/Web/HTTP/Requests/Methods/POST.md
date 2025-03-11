[[HTTP Методы (HTTP Methods)||HTTP-Метод]], который используется для отправки данных на [[Веб Сервер (Web Server)||сервер]].

- Создает новый ресурс.
- Может содержать тело запроса ([[{TODO} JSON||JSON]], FormData и др.).
- Не [[Идемпотентность (Idempotency)||идемпотентный]] (один и тот же запрос может создать несколько ресурсов).


### Пример

```http
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Yauheni"
}
```

Ответ:

```http
HTTP/1.1 201 Created
```
