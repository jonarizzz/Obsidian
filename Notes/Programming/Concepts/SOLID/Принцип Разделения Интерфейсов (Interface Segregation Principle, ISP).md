**Принцип Разделения Интерфейсов (ISP)** – «Клиенты не должны зависеть от [[Интерфейс (Interface)||интерфейсов]], которые они не используют».

Проще говоря – большие [[Интерфейс (Interface)||интерфейсы]] следует разделять на более мелкие, чтобы [[Класс (Class)||классы-реализации]] не были вынуждены реализовывать методы, которые им не нужны.


### Пример

Нарушение [[Принцип Разделения Интерфейсов (Interface Segregation Principle, ISP)||ISP]] (слишком общий [[Интерфейс (Interface)||интерфейс]]):

```java
interface Worker {
    void work();
    void eat();
}

class Robot implements Worker {
    public void work() { System.out.println("Working..."); }
    
    public void eat() { 
	    throw new UnsupportedOperationException("Robots don't eat"); 
	}
}
```

Робот не должен реализовывать `eat()`, но вынужден из-за общего [[Интерфейс (Interface)||интерфейса]].


### Использование [[Принцип Разделения Интерфейсов (Interface Segregation Principle, ISP)||ISP]] (разделение [[Интерфейс (Interface)||интерфейсов]]):

```java
interface Workable { void work(); }
interface Eatable { void eat(); }

class Robot implements Workable {
    public void work() { System.out.println("Working..."); }
}
class Human implements Workable, Eatable {
    public void work() { System.out.println("Working..."); }
    public void eat() { System.out.println("Eating..."); }
}
```

Теперь [[Класс (Class)||классы]] реализуют только нужные методы.