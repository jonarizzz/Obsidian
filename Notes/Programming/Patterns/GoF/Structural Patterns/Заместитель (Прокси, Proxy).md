**Заместитель (Proxy)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который создаёт [[Объект (Object)||объект-заместитель]], который управляет доступом к другому [[Объект (Object)||объекту]].


### Пример

```java
interface Service {
    void request();
}

class RealService implements Service {
    public void request() { 
	    System.out.println("Executing RealService request"); 
	}
}

class Proxy implements Service {
    private RealService realService;
    public void request() {
        if (realService == null) realService = new RealService();
        System.out.println("Proxy: Checking access before forwarding request");
        realService.request();
    }
}

Service proxy = new Proxy();
proxy.request();
```