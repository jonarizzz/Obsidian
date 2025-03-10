**Наблюдатель (Observer)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который позволяет [[Объект (Object)||объекту]] уведомлять подписчиков об изменениях.


### Пример

```java
import java.util.*;

interface Observer {
    void update(String message);
}

class Subject {
    private final List<Observer> observers = new ArrayList<>();

    void addObserver(Observer o) { 
	    observers.add(o); 
	}
	
    void notifyObservers(String message) { 
	    observers.forEach(o -> o.update(message)); 
	}
}

class ConcreteObserver implements Observer {
    private final String name;
    
    public ConcreteObserver(String name) { 
	    this.name = name; 
	}
	
    public void update(String message) { 
	    System.out.println(name + " received: " + message); 
	}
}

Subject subject = new Subject();
Observer observer1 = new ConcreteObserver("Observer 1");
subject.addObserver(observer1);
subject.notifyObservers("Update available!");
```