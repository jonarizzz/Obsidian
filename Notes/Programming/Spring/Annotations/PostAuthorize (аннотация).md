Аннотация @PostAuthorize в [[Spring Security||Spring Security]] применяется для проверки прав доступа после выполнения метода. Она позволяет использовать выражения [[{TODO} SpEL||SpEL]] для проверки доступа к возвращаемому значению метода, например:

```java
@PostAuthorize("returnObject.owner == authentication.name")
public Document getDocumentById(Long id) {
    return documentRepository.findById(id).orElseThrow(() -> new DocumentNotFoundException(id));
}
```

В этом примере проверяется, что владелец документа совпадает с текущим пользователем. Это полезно, когда права доступа зависят от данных, которые доступны только после выполнения метода.

  
### Когда использовать:

Когда необходимо провести проверку прав доступа на основе данных, возвращаемых методом, и когда эти данные можно проверить только после выполнения метода (например, когда они зависят от состояния [[Объект (Object)||объекта]], который был получен в результате выполнения метода).

  
### Важное замечание:

[[PostAuthorize (аннотация)||@PostAuthorize]] работает с результатом, который возвращает метод, и в отличие от аннотации [[PreAuthorize (аннотация)||@PreAuthorize]], которая выполняет проверку до выполнения метода, эта аннотация проверяет права доступа после того, как метод уже был вызван.