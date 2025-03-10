**Посредник (Медиатор, Mediator)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который координирует взаимодействие между [[Объект (Object)||объектами]], уменьшая их зависимость друг от друга.


### Пример

```java
import java.util.*;

interface Mediator { 
	void sendMessage(String message, Colleague sender); 
}

class ChatMediator implements Mediator {
    private final List<Colleague> colleagues = new ArrayList<>();
    
    public void addColleague(Colleague colleague) { 
		colleagues.add(colleague); 
	}
	
    public void sendMessage(String message, Colleague sender) {
        colleagues.forEach(colleague -> { 
	        if (colleague != sender) colleague.receive(message); 
		});
    }
}

abstract class Colleague {
    protected Mediator mediator;
    
    public Colleague(Mediator mediator) { 
	    this.mediator = mediator; 
	}
	
    public abstract void receive(String message);
}

class User extends Colleague {

    public User(Mediator mediator) { 
	    super(mediator); 
	}
	
    public void send(String message) { 
	    mediator.sendMessage(message, this); 
	}
	
    public void receive(String message) { 
	    System.out.println("User received: " + message); 
	}
}

Mediator mediator = new ChatMediator();
User user1 = new User(mediator);
User user2 = new User(mediator);
mediator.addColleague(user1);
mediator.addColleague(user2);
user1.send("Hello!");
```