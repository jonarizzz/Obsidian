**Полиморфизм (Polymorphism)** — это принцип, позволяющий использовать один и тот же [[Интерфейс (Interface)||интерфейс]] для работы с разными типами [[Объект (Object)||объектов]]. Делает код гибким, позволяя использовать общий [[Интерфейс (Interface)||интерфейс]] для разных реализаций, что упрощает поддержку и расширение системы.

Основная идея – один метод или [[Интерфейс (Interface)||интерфейс]] может работать с разными реализациями.

Реализуется через:
- **Перегрузка методов (Compile-time полиморфизм)** – несколько методов с одинаковым именем, но разными параметрами.
- **Переопределение методов (Runtime полиморфизм)** – подклассы изменяют поведение унаследованных методов.
- Работа через общий [[Интерфейс (Interface)||интерфейс]] или [[Абстрактный Класс (Abstract Class)||абстрактный класс]].


### Пример с переопределением методов:

```java
abstract class Animal {
    abstract void makeSound();
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Гав-гав!");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Мяу!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        Animal myCat = new Cat();
        
        myDog.makeSound(); // "Гав-гав!"
        myCat.makeSound(); // "Мяу!"
    }
}
```


### Пример с перегрузкой методов:

```java
class MathUtils {
    static int add(int a, int b) {
        return a + b;
    }
	
    static double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(MathUtils.add(2, 3));       // 5 (int)
        System.out.println(MathUtils.add(2.5, 3.5));   // 6.0 (double)
    }
}
```

