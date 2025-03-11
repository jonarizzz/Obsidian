**URL** — это адрес, который указывает, где находится ресурс в интернете и как к нему получить доступ.


### Структура

```http
https://example.com:8080/path/to/page?query=value#section
```

- **Протокол** → `https://` ([[HTTP (Hypertext Transfer Protocol)||HTTP]], [[HTTPS (Hypertext Transfer Protocol Secure)||HTTPS]], [[{TODO} FTP (File Transfer Protocol)||FTP]] и др.)
- **Домен** → `example.com` (имя [[Веб Сервер (Web Server)||сервера]] или [[IP Адрес (Internet Protocol Address, IP Address)||IP-адрес]])
- **Порт** → `:8080` (необязательный, по умолчанию `80` для [[HTTP (Hypertext Transfer Protocol)||HTTP]], `443` для [[HTTPS (Hypertext Transfer Protocol Secure)||HTTPS]])
- **Путь** → `/path/to/page` (разделы сайта)
- **Запрос (Query String)** → `?query=value` (параметры, передаваемые на [[Веб Сервер (Web Server)||сервер]])
- **Фрагмент (Anchor)** → `#section` (указание на часть страницы)


### Где используется?

- В браузерах для загрузки веб-страниц.
- В API для передачи параметров.
- В системах навигации по файлам.