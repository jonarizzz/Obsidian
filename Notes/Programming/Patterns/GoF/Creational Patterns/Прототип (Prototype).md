**Прототип (Prototype)** – [[Порождающие паттерны (Creational Patterns)||порождающий паттерн]], который создаёт [[Объект (Object)||объект]] путём копирования другого [[Объект (Object)||объекта]].


### Пример

```java
class Prototype implements Cloneable {
    String data;
	
    public Prototype(String data) { this.data = data; }
	
    public Prototype clone() throws CloneNotSupportedException {
        return (Prototype) super.clone();
    }
}

Prototype original = new Prototype("Hello");
Prototype copy = original.clone();
```