**@ExceptionHandler** — это аннотация в [[Спринг Фреймворк (Spring Framework)||Spring Framework]], которая используется для указания метода, который будет обрабатывать исключения, возникшие в [[{TODO} Контроллер (Controller)||контроллерах]]. Этот метод перехватывает [[Исключение (Exception)||исключения]], выбрасываемые в процессе выполнения [[HTTP Запрос (HTTP Request)||HTTP-запроса]], и позволяет задать логику обработки [[{TODO} Error||ошибок]] (например, возврат соответствующего [[Статусы ответов HTTP (HTTP Statuses)||HTTP-статуса]] или пользовательского сообщения).


### Пример использования:

```java
@ExceptionHandler(SomeException.class)
public ResponseEntity<String> handleSomeException(SomeException ex) {
    return new ResponseEntity<>("Error occurred: " + ex.getMessage(), HttpStatus.BAD_REQUEST);
}
```

Такой метод будет вызван, если в контроллере произойдет [[Исключение (Exception)||исключение]] типа `SomeException`.