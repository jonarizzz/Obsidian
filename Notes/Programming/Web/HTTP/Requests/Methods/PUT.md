[[HTTP Методы (HTTP Methods)||HTTP-Метод]], который заменяет существующий ресурс новыми данными.

- Требует передать весь объект.
- Если ресурс не существует, может создать его (но не всегда).
- [[Идемпотентность (Idempotency)||Идемпотентный]] (повторный запрос не меняет результат).


### Пример:

```http
PUT /api/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Yauheni",
  "email": "test@example.com"
}
```
