Аннотация @CrossOrigin используется в [[Спринг Фреймворк (Spring Framework)||Spring Framework]] для настройки политики кросс-доменных запросов ([[CORS||CORS]]). Это позволяет контролировать, с каких доменов может быть доступен ресурс на сервере. Эта аннотация используется в основном в [[Веб Приложение (Web Application)||веб-приложениях]], чтобы разрешить или ограничить доступ с различных источников (доменов, портов или протоколов) к ресурсам API.



### Простое использование:

Аннотация применяется к контроллеру или методу, чтобы разрешить запросы с другого домена.

```java
@CrossOrigin
@RestController
public class MyController {
    @GetMapping("/hello")
    public String hello() {
        return "Hello, world!";
    }
}
```

В этом примере сервер будет разрешать кросс-доменные запросы ко всем методам [[{TODO} Контроллер (Controller)||контроллера]].

  

### Настройка параметров:

Аннотация позволяет настроить различные параметры, такие как список разрешённых источников, [[HTTP Методы (HTTP Methods)||методы HTTP]] и [[HTTP Заголовки (HTTP Headers)||заголовки]].

```java
@CrossOrigin(origins = "http://example.com", allowedHeaders = "Authorization", methods = {RequestMethod.GET, RequestMethod.POST})
@RestController
public class MyController {
    @GetMapping("/hello")
    public String hello() {
        return "Hello, world!";
    }
}
```

- `origins` — список доменов, которым разрешено делать запросы.
- `allowedHeaders` — список заголовков, которые могут быть использованы в запросах.
- `methods` — список методов [[HTTP Методы (HTTP Methods)||HTTP]] (например, GET, POST), которые разрешены для использования с кросс-доменными запросами.

  

### Глобальная настройка:

Вместо того чтобы использовать аннотацию на каждом [[{TODO} Контроллер (Controller)||контроллере]], можно настроить [[CORS||CORS]] для всего приложения в конфигурации [[Спринг Фреймворк (Spring Framework)||Spring]].

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://example.com")
                .allowedMethods("GET", "POST")
                .allowedHeaders("Authorization");
    }
}
```

Это позволяет управлять настройками [[CORS||CORS]] для всего приложения в одном месте.