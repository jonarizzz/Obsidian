**Принцип инверсии зависимостей (DIP)** гласит:

1. Модули верхнего уровня не должны зависеть от модулей нижнего уровня. Оба должны зависеть от [[Абстракция (Abstraction)||абстракций]].
2. [[Абстракция (Abstraction)||Абстракции]] не должны зависеть от деталей. Детали должны зависеть от [[Абстракция (Abstraction)||абстракций]].

Проще говоря – вместо того чтобы высокоуровневый код напрямую зависел от конкретных реализаций ([[Класс (Class)||классов]]), он должен зависеть от [[Интерфейс (Interface)||интерфейсов]] или [[Абстрактный Класс (Abstract Class)||абстрактных классов]]. Конкретные реализации уже зависят от этих [[Абстракция (Abstraction)||абстракций]].


### Пример:

Нарушение [[Принцип Инверсии Зависимостей (Dependency Inversion Principle, DIP)||DIP]]:

```java
class MySQLDatabase {
    void connect() { System.out.println("Connected to MySQL"); }
}

class Service {
    private MySQLDatabase db = new MySQLDatabase(); // Жёсткая зависимость

    void performOperation() {
        db.connect();
        System.out.println("Operation performed");
    }
}
```

Здесь `Service` напрямую зависит от `MySQLDatabase`, что делает код негибким.

Следуем [[Принцип Инверсии Зависимостей (Dependency Inversion Principle, DIP)||DIP]]:

```java
interface Database {
    void connect();
}

class MySQLDatabase implements Database {
    public void connect() { System.out.println("Connected to MySQL"); }
}

class Service {
    private Database db;
	
    Service(Database db) { this.db = db; } // Внедрение зависимости
	
    void performOperation() {
        db.connect();
        System.out.println("Operation performed");
    }
}
```

Теперь `Service` зависит от [[Абстракция (Abstraction)||абстракции]] (`Database`), а не от конкретного [[Класс (Class)||класса]]. Это позволяет легко подменять реализацию (например, заменить `MySQLDatabase` на `PostgreSQLDatabase`).