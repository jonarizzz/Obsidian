**Команда (Command)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который [[Инкапсуляция (Encapsulation)||инкапсулирует]] запрос как [[Объект (Object)||объект]], позволяя параметризовать клиентов с различными запросами.


### Пример

```java
interface Command { 
	void execute(); 
}

class Light {
    void turnOn() { 
	    System.out.println("Light is ON"); 
	}
}

class LightOnCommand implements Command {
    private final Light light;
    
    public LightOnCommand(Light light) { 
	    this.light = light; 
	}
	
    public void execute() { 
	    light.turnOn(); 
	}
}

class RemoteControl {
    private Command command;
    
    public void setCommand(Command command) { 
	    this.command = command; 
	}
	
    public void pressButton() { 
	    command.execute(); 
	}
}

Light light = new Light();
Command lightOn = new LightOnCommand(light);
RemoteControl remote = new RemoteControl();
remote.setCommand(lightOn);
remote.pressButton();
```