**HTTP-заголовки** — это метаданные, передаваемые в [[HTTP Запрос (HTTP Request)||запросах]] и [[HTTP Ответ (HTTP Response)||ответах]] между клиентом (браузер, API-клиент) и [[Веб Сервер (Web Server)||сервером]]. Они помогают управлять соединением, описывать содержимое, аутентифицировать пользователя и многое другое.


### Виды заголовков

- Общие (General Headers) – не зависят от запроса или ответа, влияют на соединение.
	- `Connection: keep-alive` – поддерживать соединение открытым
	- `Cache-Control: no-cache` – не кэшировать
- Заголовки запроса (Request Headers) – передаются клиентом, уточняют запрос.
	- `User-Agent: Mozilla/5.0` – инфа о браузере/клиенте
	- `Accept: application/json` – какие форматы данных клиент принимает
	- `Authorization: Bearer <token>` – передача токена авторизации
- Заголовки ответа (Response Headers) – сервер отправляет клиенту.
	- `Content-Type: application/json` – формат данных в теле ответа
	- `Set-Cookie: session_id=abc123; HttpOnly` – устанавливает куки
	- `Server: nginx/1.18.0` – информация о сервере
- Заголовки тела (Entity Headers) – описывают передаваемые данные.
	- `Content-Length: 1234` – размер тела в байтах
	- `Content-Encoding: gzip` – сжатие тела


### Пример запроса с заголовками

```http
GET /api/user/123 HTTP/1.1
Host: example.com
User-Agent: curl/7.64.1
Accept: application/json
Authorization: Bearer my-secret-token
```


### Пример ответа сервера

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