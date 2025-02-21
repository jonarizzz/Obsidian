Функциональный интерфейс в Java — это [[Интерфейс (Interface)||интерфейс]], который содержит ровно **один** абстрактный метод. Он предназначен для использования в [[Лямбда Функция (Lambda)||лямбда-выражениях]] и **ссылках на методы**.

### Определение

Функциональный интерфейс помечается аннотацией `@FunctionalInterface`, но её использование **необязательно** (компилятор сам проверяет, что [[Интерфейс (Interface)||интерфейс]] содержит только один абстрактный метод).

```java
@FunctionalInterface
public interface MyFunctionalInterface {
    void doSomething(); // единственный абстрактный метод
}
```


### Использование

Такой [[Интерфейс (Interface)||интерфейс]] можно использовать с [[Лямбда Функция (Lambda)||лямбда-выражением]]:

```java
MyFunctionalInterface func = () -> System.out.println("Hello, Functional Interface!");
func.doSomething(); // Выведет: Hello, Functional Interface!
```


### Примеры встроенных функциональных интерфейсов

В Java уже есть готовые функциональные интерфейсы в пакете `java.util.function`. Например:

- `Supplier<T>` — без аргументов, возвращает результат
- `Consumer<T>` — принимает аргумент, но ничего не возвращает
- `Function<T, R>` — принимает аргумент и возвращает результат
- `Predicate<T>` — принимает аргумент и возвращает [[boolean||boolean]]


### Пример с Predicate:

```java
import java.util.function.Predicate;

public class Main {
    public static void main(String[] args) {
        Predicate<Integer> isEven = x -> x % 2 == 0;
        System.out.println(isEven.test(4)); // true
        System.out.println(isEven.test(5)); // false
    }
}
```


### Дополнительные методы

[[Функциональный Интерфейс (Functional Interface)||Функциональный интерфейс]] **может** содержать:
- статические методы
- default-методы

Но он не должен иметь больше одного абстрактного метода.

```java
@FunctionalInterface
interface MyInterface {
    void execute(); // единственный абстрактный метод
	
    default void printInfo() {
        System.out.println("This is a functional interface");
    }
	
    static void staticMethod() {
        System.out.println("Static method in interface");
    }
}
```