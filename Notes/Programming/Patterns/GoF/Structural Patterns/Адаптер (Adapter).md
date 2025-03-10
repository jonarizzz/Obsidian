**Адаптер (Adapter)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который позволяет [[Объект (Object)||объектам]] с несовместимыми [[Интерфейс (Interface)||интерфейсами]] работать вместе.

### Пример

```java
interface Target {
    void request();
}

class Adaptee {
    void specificRequest() { System.out.println("Specific request"); }
}

class Adapter implements Target {
    private final Adaptee adaptee = new Adaptee();

    public void request() { adaptee.specificRequest(); }
}

Target adapter = new Adapter();
adapter.request();
```