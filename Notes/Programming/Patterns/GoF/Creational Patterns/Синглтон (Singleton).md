**Синглтон (Singleton)** – [[Порождающие паттерны (Creational Patterns)||порождающий паттерн]], который гарантирует, что у [[Класс (Class)||класса]] есть только один [[Объект (Object)||экземпляр]].


### Пример

```java
public class Singleton {

    private static Singleton instance;
    private Singleton() {} // Закрытый конструктор

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```