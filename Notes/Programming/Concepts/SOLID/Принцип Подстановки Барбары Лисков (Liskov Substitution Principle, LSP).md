Принцип подстановки Барбары Лисков (Liskov Substitution Principle, LSP) – “[[Объект (Object)||Объекты]] наследуемого (дочернего) [[Класс (Class)||класса]] должны быть заменяемы на [[Объект (Object)||объекты]] базового (родительского) [[Класс (Class)||класса]] без изменения правильности программы.” 

Проще говоря – потомка всегда должно быть возможно заменить родителем без проблем. 


### Признаки нарушения [[Принцип Подстановки Барбары Лисков (Liskov Substitution Principle, LSP)||LSP]]:

- **Методы потомка ведут себя неожиданно** – например, метод, который должен возвращать число, внезапно выбрасывает [[Исключение (Exception)||исключение]].
- **Ненужные заглушки** – если в потомке приходится оставлять пустые методы (`return;` или `throw new Exception("Not implemented");`), это сигнал к проблеме.
- **Изменение контракта** – например, базовый [[Класс (Class)||класс]] обещает, что метод `get_items()` вернет [[List (интерфейс)||список]], а потомок начинает возвращать `null` или [[String||строку]].

  

### Пример нарушения:

```java
class Bird {
    void fly() {
        System.out.println("Я лечу!");
    }
}

class Penguin extends Bird {
    @Override
    void fly() {
        throw new UnsupportedOperationException("Пингвины не летают!");
    }
}
```

Здесь `Penguin` нарушает [[Принцип Подстановки Барбары Лисков (Liskov Substitution Principle, LSP)||LSP]], так как не может корректно подставляться вместо `Bird`.


### Как исправить?

Выделить [[Интерфейс (Interface)||интерфейсы]] или [[Абстрактный Класс (Abstract Class)||абстрактные классы]], например:

```java
interface Flyable {
    void fly();
}

class Bird { }

class Eagle extends Bird implements Flyable {
    public void fly() {
        System.out.println("Я лечу!");
    }
}

class Penguin extends Bird { }
```

Теперь `Penguin` не наследует метод `fly()`, и [[Принцип Подстановки Барбары Лисков (Liskov Substitution Principle, LSP)||LSP]] не нарушается.