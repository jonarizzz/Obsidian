Принцип открытости-закрытости (OCP) – “Программные сущности (классы, модули, функции) должны быть открыты для расширения, но закрыты для модификации.”


### Что это значит?

- **Открытость для расширения** – можно добавлять новую функциональность без изменения существующего кода.
- **Закрытость для модификации** – не нужно изменять уже работающий код, чтобы избежать ошибок и нежелательных побочных эффектов.


### Как реализовать?

- Использовать [[Абстракция (Abstraction)||абстракции]] ([[Интерфейс (Interface)||интерфейсы]], [[Абстрактный Класс (Abstract Class)||абстрактные классы]]).
- Применять [[Полиморфизм (Polymorphism)||полиморфизм]] (создавать новые [[Класс (Class)||классы]], реализующие общий [[Интерфейс (Interface)||интерфейс]], вместо изменения старых).
- Использовать [[Паттерны Банды Четырёх (Gang of Four Patterns, GOF Patterns)||паттерны проектирования]], такие как [[Шаблонный Метод (Template Method)||Шаблонный метод]], [[Стратегия (Strategy)||Стратегия]], [[Декоратор (Decorator)||Декоратор]].


### Пример

До [[Принцип Открытости-Закрытости (Opened-Closed Principle, OCP)||OCP]]:

```java
class NotificationService {
    void sendNotification(String type, String message) {
        if (type.equals("EMAIL")) {
            System.out.println("Sending email: " + message);
        } else if (type.equals("SMS")) {
            System.out.println("Sending SMS: " + message);
        }
    }
}
```

При добавлении нового типа уведомлений придется менять код.


После [[Принцип Открытости-Закрытости (Opened-Closed Principle, OCP)||OCP]]:

```java
interface Notifier {
    void send(String message);
}

class EmailNotifier implements Notifier {
    public void send(String message) {
        System.out.println("Sending email: " + message);
    }
}

class SMSNotifier implements Notifier {
    public void send(String message) {
        System.out.println("Sending SMS: " + message);
    }
}

class NotificationService {
    private final Notifier notifier;
    
    NotificationService(Notifier notifier) {
        this.notifier = notifier;
    }

    void sendNotification(String message) {
        notifier.send(message);
    }
}
```

Теперь можно добавить новый тип уведомления (например, `PushNotifier`) без изменения существующего кода.