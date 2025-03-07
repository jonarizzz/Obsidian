Аннотация @PreAuthorize в [[Spring Security||Spring Security]] используется для контроля доступа к методам на основе выражений безопасности. Она позволяет проверять [[Авторизация (Authorization)||права пользователя]] до выполнения метода.


### Пример:

```java
@PreAuthorize("hasRole('ADMIN')")
public void someAdminMethod() { ... }
```

### Основные возможности:

- Проверка ролей: `hasRole('ADMIN')`.
- Проверка прав: `hasPermission(#user, 'read')`.
- Логические операторы: можно комбинировать условия, например, `and`, `or`.
- Доступ к данным пользователя через `principal`.

  

Для использования нужно включить настройку:

```java
@EnableGlobalMethodSecurity(prePostEnabled = true)
```
