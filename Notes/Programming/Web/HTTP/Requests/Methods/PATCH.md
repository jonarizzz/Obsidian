[[HTTP Методы (HTTP Methods)||HTTP-Метод]], который обновляет только указанные поля ресурса.

- Изменяет часть данных, не затрагивая остальные.
- Не [[Идемпотентность (Idempotency)||идемпотентный]] в некоторых реализациях.


### Пример:

```http
PATCH /api/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "email": "new@example.com"
}
```
