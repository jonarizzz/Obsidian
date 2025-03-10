**Наследование (Inheritance)** — это принцип, позволяющий одному [[Класс (Class)||классу]] унаследовать свойства и методы другого [[Класс (Class)||класса]]. Позволяет избежать дублирования кода.
  
Основная идея – создавать новые [[Класс (Class)||классы]] на основе существующих, переиспользуя код и дополняя его.

Реализуется через:
- Ключевое слово [[{TODO} extends||extends]] – для наследования от другого класса.
- Ключевое слово [[{TODO} super||super]] – для вызова конструктора или методов родительского класса.


### Пример

```java
class Animal {
    String name;
	
    Animal(String name) {
        this.name = name;
    }
	
    void makeSound() {
        System.out.println("Какой-то звук...");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name); // Вызов конструктора родительского класса
    }
	
    @Override
    void makeSound() {
        System.out.println(name + " говорит: Гав-гав!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog("Бобик");
        myDog.makeSound(); // "Бобик говорит: Гав-гав!"
    }
}
```