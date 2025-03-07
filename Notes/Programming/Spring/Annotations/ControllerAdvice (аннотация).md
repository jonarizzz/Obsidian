Аннотация @ControllerAdvice в [[Спринг Фреймворк (Spring Framework)||Spring]] используется для обработки [[Исключение (Exception)||исключений]] и для конфигурации глобальных аспектов обработки запросов в приложении. Она предоставляет удобный способ централизованно обрабатывать [[{TODO} Error||ошибки]] и [[Исключение (Exception)||исключения]] в одном месте, без необходимости прописывать обработчики ошибок в каждом [[{TODO} Контроллер (Controller)||контроллере]].

### Вот основные моменты, что делает @ControllerAdvice:

1. **Глобальная обработка исключений**: С помощью [[ExceptionHandler (аннотация)||@ExceptionHandler]] внутри [[ControllerAdvice (аннотация)||@ControllerAdvice]] можно перехватывать исключения, которые происходят в [[{TODO} Контроллер (Controller)||контроллерах]], и обрабатывать их централизованно. Это позволяет избежать повторения кода и делать обработку ошибок более структурированной.
2. **Глобальные модели атрибутов**: Внутри [[ControllerAdvice (аннотация)||@ControllerAdvice]] можно использовать аннотацию [[{TODO} ModelAttribute (аннотация)||@ModelAttribute]], чтобы добавлять атрибуты в [[{TODO} Модель (Model)||модель]], которые будут доступны во всех [[{TODO} Контроллер (Controller)||контроллерах]]. Это полезно, например, для добавления общих данных, которые должны быть доступны во всех [[{TODO} Представление (View)||представлениях]].
3. **Глобальная настройка**: Можно использовать [[ControllerAdvice (аннотация)||@ControllerAdvice]] для настройки, например, преобразования ответов или глобальных фильтров для всех контроллеров.


### Пример использования:

```java
@ControllerAdvice
public class GlobalExceptionHandler {
	
    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleException(Exception e) {
        return new ResponseEntity<>("Ошибка: " + e.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }
	
    @ModelAttribute("globalAttribute")
    public String globalAttribute() {
        return "Some global data";
    }
}
```

В этом примере:
- [[Исключение (Exception)||Исключения]], происходящие в [[{TODO} Контроллер (Controller)||контроллерах]], будут обрабатываться методом `handleException`.
- Атрибут `globalAttribute` будет добавлен в [[{TODO} Модель (Model)||модель]] всех [[{TODO} Контроллер (Controller)||контроллеров]].