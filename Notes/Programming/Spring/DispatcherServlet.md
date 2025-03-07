DispatcherServlet — это центральный компонент [[{TODO} Spring MVC||Spring MVC]], который отвечает за обработку входящих [[{TODO} HTTP Запрос||HTTP-запросов]] и маршрутизацию их к соответствующим обработчикам ([[{TODO} Контроллер (Controller)||контроллерам]]). Он действует как [[{TODO} Фронт-Контроллер (Front Controller)||фронт-контроллер (Front Controller)]], управляя потоком запроса в [[{TODO} Веб Приложение (Web Application)||веб-приложении]].


### Основные функции DispatcherServlet:

- **Получение запроса** – принимает [[{TODO} HTTP Запрос||HTTP-запрос]] от сервера.
- **Определение обработчика** – с помощью `HandlerMapping` находит соответствующий контроллер.
- **Вызов контроллера** – передает запрос обработчику (методу контроллера).
- **Обработка результата** – получает объект `ModelAndView` или другой результат.
- **Выбор View** – использует `ViewResolver` для поиска представления.
- **Формирование ответа** – рендерит представление и отправляет ответ клиенту.

  

### Как это работает?

1. [[Веб Сервер (Web Server)||Веб-сервер]] (например, Tomcat) получает [[{TODO} HTTP Запрос||HTTP-запрос]].
2. Запрос передается DispatcherServlet, который определяет, какой [[{TODO} Контроллер (Controller)||контроллер]] должен его обработать.
3. Контроллер возвращает данные (обычно объект `ModelAndView`).
4. DispatcherServlet определяет нужное представление (`View`) и передает данные туда.
5. Генерируется HTTP-ответ и отправляется клиенту.

  

### Пример настройки в web.xml (если используется XML-конфигурация):

```xml
<servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

Здесь DispatcherServlet маппится на корневой URL (/), обрабатывая все запросы.

  

### Современная конфигурация через Java ([[Spring Boot||Spring Boot]]):

В [[Spring Boot||Spring Boot]] DispatcherServlet настраивается автоматически, и достаточно просто создать [[{TODO} Контроллер (Controller)||контроллер]]:

```java
@RestController
@RequestMapping("/api")
public class MyController {
	
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

[[Spring Boot||Spring Boot]] автоматически регистрирует DispatcherServlet, и запрос к `/api/hello` будет корректно обработан.