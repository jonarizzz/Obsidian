**Фасад (Facade)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который предоставляет простой [[Интерфейс (Interface)||интерфейс]] для сложной системы.


### Пример:

```java
class SubsystemA { 
	void operationA() { 
		System.out.println("Subsystem A operation"); 
	} 
}

class SubsystemB { 
	void operationB() { 
		System.out.println("Subsystem B operation"); 
	} 
}

class Facade {
    private final SubsystemA a = new SubsystemA();
    private final SubsystemB b = new SubsystemB();

    void operation() {
        a.operationA();
        b.operationB();
    }
}

Facade facade = new Facade();
facade.operation();
```