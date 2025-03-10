
**Декоратор (Decorator)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который добавляет новые функциональности [[Объект (Object)||объекту]] без изменения его структуры.


### Пример

```java
interface Coffee { 
	String getDescription(); 
}

class SimpleCoffee implements Coffee {
    public String getDescription() { 
	    return "Simple Coffee"; 
	}
}

class MilkDecorator implements Coffee {
    private final Coffee coffee;
    
    public MilkDecorator(Coffee coffee) { 
	    this.coffee = coffee; 
	}
	
    public String getDescription() { 
	    return coffee.getDescription() + ", Milk"; 
	}
}

Coffee coffee = new MilkDecorator(new SimpleCoffee());
System.out.println(coffee.getDescription()); // Simple Coffee, Milk
```