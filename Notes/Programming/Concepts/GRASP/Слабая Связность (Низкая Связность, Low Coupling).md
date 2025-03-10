**Слабая Связность (Low Coupling)** — это принцип проектирования программного обеспечения, при котором модули (классы, компоненты, сервисы) зависят друг от друга минимально. Это означает, что изменения в одном модуле оказывают минимальное влияние на другие.


### Основные идеи

- **Минимизация зависимостей** – каждый модуль должен иметь как можно меньше зависимостей от других частей системы.
- **Легкость замены и модификации** – можно изменить один модуль без необходимости менять другие.
- **Упрощенное тестирование** – модули можно тестировать изолированно (юнит-тестирование).
- **Повышенная повторная используемость** – слабосвязанные модули можно использовать в разных контекстах.


### Пример

Допустим, у нас есть [[Класс (Class)||класс]], который напрямую работает с конкретной реализацией [[База данных (БД, Database, DB)||БД]]:

```java
class UserService {
    private MySQLDatabase db; // Жесткая зависимость
	
    public UserService() {
        this.db = new MySQLDatabase();
    }
	
    public void saveUser(User user) {
        db.insert(user);
    }
}
```

Здесь высокая связность: `UserService` зависит от конкретной реализации `MySQLDatabase`. Если нам нужно заменить [[База данных (БД, Database, DB)||базу данных]] (например, на PostgreSQL), придется менять код `UserService`.

Используем [[Интерфейс (Interface)||интерфейс]] для снижения зависимости:

```java
interface Database {
    void insert(User user);
}

class MySQLDatabase implements Database {
    public void insert(User user) {
        System.out.println("Saving to MySQL");
    }
}

class UserService {
    private Database db;
	
    public UserService(Database db) { // Внедрение зависимости
        this.db = db;
    }
	
    public void saveUser(User user) {
        db.insert(user);
    }
}
```

Теперь `UserService` зависит не от конкретной [[База данных (БД, Database, DB)||базы данных]], а от [[Абстракция (Abstraction)||абстракции]] (`Database`). Это позволяет легко подменять реализацию, например, использовать `PostgreSQLDatabase` без изменения кода `UserService`.


### Как достичь слабой связности?

1. Использовать [[Интерфейс (Interface)||интерфейсы]] и [[Абстрактный Класс (Abstract Class)||абстрактные классы]] вместо жестких зависимостей.
2. Применять инъекцию зависимостей ([[Внедрение Зависимостей (Dependency Injection)||Dependency Injection]]).
3. Разделять ответственность ([[SOLID||SRP – Single Responsibility Principle]]).
4. Следовать принципу инверсии зависимостей ([[SOLID||DIP – Dependency Inversion Principle]]).