**Стратегия (Strategy)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который позволяет изменять поведение [[Объект (Object)||объекта]] во время выполнения.


### Пример

```java
interface Strategy {
    void execute();
}

class ConcreteStrategyA implements Strategy {
    public void execute() { 
	    System.out.println("Strategy A executed"); 
	}
}

class Context {
    private Strategy strategy;
    
    public void setStrategy(Strategy strategy) { 
	    this.strategy = strategy; 
	}
	
    public void performAction() { 
	    strategy.execute(); 
	}
}

Context context = new Context();
context.setStrategy(new ConcreteStrategyA());
context.performAction();
```