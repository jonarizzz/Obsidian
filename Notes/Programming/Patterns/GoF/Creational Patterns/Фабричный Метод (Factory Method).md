**Фабричный Метод (Factory Method)** – [[Порождающие паттерны (Creational Patterns)||порождающий паттерн]], который определяет [[Интерфейс (Interface)||интерфейс]] для создания [[Объект (Object)||объектов]], позволяя подклассам решать, какой [[Класс (Class)||класс]] создавать.


### Пример

```java
interface Product {
    void use();
}

class ConcreteProductA implements Product {
    public void use() { 
	    System.out.println("Using Product A"); 
	}
}

class Factory {
    public static Product createProduct(String type) {
        return switch (type) {
            case "A" -> new ConcreteProductA();
            default -> throw new IllegalArgumentException("Unknown product");
        };
    }
}

Product product = Factory.createProduct("A");
product.use();
```