**Абстрактный класс (Abstract Class)** — это [[Класс (Class)||класс]], который нельзя создать как [[Объект (Object)||объект]], но можно использовать как основу для других [[Класс (Class)||классов]]. Это шаблон для других [[Класс (Class)||классов]], который определяет основную структуру и обязывает подклассы реализовать определённые методы.


### Основные особенности

- Может содержать абстрактные методы (без реализации) и обычные методы (с реализацией).
- Используется для создания общего шаблона для подклассов.
- Подклассы должны переопределить абстрактные методы или сами стать абстрактными.


### Пример

```java
abstract class Animal {
    String name;
	
    Animal(String name) {
        this.name = name;
    }
	
    abstract void makeSound(); // Абстрактный метод (без реализации)
	
    void sleep() { // Обычный метод (с реализацией)
        System.out.println(name + " спит...");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);
    }
	
    @Override
    void makeSound() {
        System.out.println(name + " говорит: Гав-гав!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Бобик");
        dog.makeSound(); // "Бобик говорит: Гав-гав!"
        dog.sleep();     // "Бобик спит..."
    }
}
```
