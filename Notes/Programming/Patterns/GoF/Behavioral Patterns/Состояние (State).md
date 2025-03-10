**Состояние (State)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который позволяет объекту изменять своё поведение в зависимости от текущего состояния.

### Пример

```java
interface State { 
	void handle(); 
}

class ConcreteStateA implements State {

    public void handle() { 
	    System.out.println("State A handling request"); 
	}
}

class Context {
    private State state;
    
    public void setState(State state) { 
	    this.state = state; 
	}
	
    public void request() { 
	    state.handle(); 
	}
}

Context context = new Context();
context.setState(new ConcreteStateA());
context.request();
```