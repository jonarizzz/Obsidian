**Легковес (Flyweight)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который оптимизирует использование памяти при работе с большим количеством схожих [[Объект (Object)||объектов]].


### Пример

```java
import java.util.*;

class Flyweight {
    private final String sharedState;
    
    public Flyweight(String sharedState) { 
	    this.sharedState = sharedState; 
	}
	
    public void operation() { 
	    System.out.println("Using Flyweight with state: " + sharedState); 
	}
}

class FlyweightFactory {
    private static final Map<String, Flyweight> cache = new HashMap<>();

    public static Flyweight getFlyweight(String state) {
        return cache.computeIfAbsent(state, Flyweight::new);
    }
}

Flyweight f1 = FlyweightFactory.getFlyweight("State1");
Flyweight f2 = FlyweightFactory.getFlyweight("State1"); // Повторно использует объект
f1.operation();
f2.operation();
```