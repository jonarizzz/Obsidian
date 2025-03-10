**Абстрактная Фабрика (Abstract Factory)** – [[Порождающие паттерны (Creational Patterns)||порождающий паттерн]], который создаёт семейства связанных [[Объект (Object)||объектов]], не указывая их конкретные [[Класс (Class)||классы]].

### Пример

```java
interface Button { 
	void render(); 
}

class WindowsButton implements Button {
    public void render() { 
	    System.out.println("Windows Button"); 
	}
}

class MacButton implements Button {
    public void render() { 
	    System.out.println("Mac Button"); 
	}
}

interface GUIFactory { 
	Button createButton(); 
}

class WindowsFactory implements GUIFactory {
    public Button createButton() { 
	    return new WindowsButton(); 
	}
}

class MacFactory implements GUIFactory {
    public Button createButton() { 
	    return new MacButton(); 
	}
}

GUIFactory factory = new WindowsFactory();
Button button = factory.createButton();
button.render();
```