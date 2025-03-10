**Мост (Bridge)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который разделяет [[Абстракция (Abstraction)||абстракцию]] и её реализацию.


### Пример

```java
interface Device { 
	void turnOn(); 
}

class TV implements Device { 
	public void turnOn() { 
		System.out.println("TV on"); 
	} 
}

class Remote { 
	protected Device device; 
	public Remote(Device device) { 
		this.device = device; 
	} 
}

class AdvancedRemote extends Remote {
    public AdvancedRemote(Device device) { 
	    super(device); 
	}
	
    public void togglePower() { 
	    device.turnOn(); 
	}
}

AdvancedRemote remote = new AdvancedRemote(new TV());
remote.togglePower();
```