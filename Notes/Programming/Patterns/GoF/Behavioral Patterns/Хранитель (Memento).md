**Хранитель (Memento)** – это [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который сохраняет и восстанавливает состояние [[Объект (Object)||объекта]] без нарушения [[Инкапсуляция (Encapsulation)||инкапсуляции]].


Пример

```java
class Memento {
    private final String state;
    
    public Memento(String state) { 
	    this.state = state; 
	}
	
    public String getState() { 
	    return state; 
	}
}

class Originator {
    private String state;
    
    public void setState(String state) { 
	    this.state = state; 
	}
	
    public Memento save() { 
	    return new Memento(state); 
	}
	
    public void restore(Memento memento) { 
	    state = memento.getState(); 
	}
}

Originator originator = new Originator();
originator.setState("State1");
Memento saved = originator.save();
originator.setState("State2");
originator.restore(saved);
```