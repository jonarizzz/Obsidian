**Посетитель (Visitor)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который позволяет добавлять новые операции для [[Объект (Object)||объектов]] без изменения их [[Класс (Class)||классов]].


### Пример

```java
interface Element {
    void accept(Visitor visitor);
}

class ConcreteElement implements Element {

    public void accept(Visitor visitor) { 
	    visitor.visit(this); 
	}
}

interface Visitor {
    void visit(ConcreteElement element);
}

class ConcreteVisitor implements Visitor {

    public void visit(ConcreteElement element) { 
	    System.out.println("Visited element"); 
	}
}

Element element = new ConcreteElement();
Visitor visitor = new ConcreteVisitor();
element.accept(visitor);
```