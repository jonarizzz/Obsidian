**Цепочка Ответственности (Chain of Responsibility)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который передаёт запрос по цепочке обработчиков, пока один из них не обработает его.


### Пример

```java
abstract class Handler {
    protected Handler next;
    
    public void setNext(Handler next) { 
	    this.next = next; 
	}
	
    public abstract void handleRequest(String request);
}

class ConcreteHandlerA extends Handler {
    public void handleRequest(String request) {
        if (request.equals("A")) System.out.println("Handled by A");
        else if (next != null) next.handleRequest(request);
    }
}

Handler handlerA = new ConcreteHandlerA();
Handler handlerB = new ConcreteHandlerA();
handlerA.setNext(handlerB);
handlerA.handleRequest("A");
```