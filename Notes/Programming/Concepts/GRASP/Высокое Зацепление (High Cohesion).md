Высокое Зацепление (High Cohesion) — это одно из ключевых свойств хорошо спроектированных модулей в программировании, особенно в [[ООП – Объектно-Ориентированное Программирование (OOP, Object Oriented Programming)||объектно-ориентированном]] дизайне. Оно означает, что все элементы внутри модуля (класса, пакета, метода) тесно связаны друг с другом и выполняют одну четко определенную задачу.
  

### Плохой дизайн (низкое зацепление)

```java
public class UserManager {
    public void registerUser(String username, String password) {
        // Логика регистрации пользователя
    }
	
    public void sendEmail(String email, String message) {
        // Логика отправки email
    }
	
    public void generateReport() {
        // Логика создания отчета
    }
}
```

Здесь класс выполняет сразу три несвязанных задачи:
- управление пользователями
- отправку email
- генерацию отчетов

Это снижает его зацепление и усложняет поддержку.


### Хороший дизайн (высокое зацепление)

```java
public class UserService {
    public void registerUser(String username, String password) {
        // Логика регистрации пользователя
    }
}

public class EmailService {
    public void sendEmail(String email, String message) {
        // Логика отправки email
    }
}

public class ReportService {
    public void generateReport() {
        // Логика создания отчета
    }
}
```

Теперь каждая сущность выполняет одну конкретную задачу, что:

- упрощает поддержку
- уменьшает зависимости
- делает код гибче  


### [[Высокое Зацепление (High Cohesion)||Зацепление]] и [[Слабая Связность (Низкая Связность, Low Coupling)||Связность]]

[[Высокое Зацепление (High Cohesion)||Высокое зацепление]] обычно сочетается с [[Слабая Связность (Низкая Связность, Low Coupling)||низкой связностью (low coupling)]] — это означает, что модули мало зависят друг от друга. Такой подход соответствует принципам [[SOLID||SOLID]], особенно SRP (Single Responsibility Principle).