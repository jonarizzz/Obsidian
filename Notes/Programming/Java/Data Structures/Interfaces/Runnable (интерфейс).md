**Runnable** — это [[Функциональный Интерфейс (Functional Interface)||функциональный интерфейс]] в Java, предназначенный для описания задачи, которую можно выполнить в отдельном [[Поток (Thread)||потоке]].


### Основные особенности:

- Находится в пакете `java.lang`.
- Содержит единственный метод `void run()`, который должен быть реализован.
- Не возвращает результат и не принимает аргументов.
- Используется для создания [[Поток (Thread)||потоков]] в сочетании с [[Поток (Thread)||Thread]].


### Пример использования:

```java
class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Задача выполняется в отдельном потоке");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyTask());
        thread.start();
    }
}
```

С [[{TODO} Java 8||Java 8]] можно использовать [[Лямбда Функция (Lambda)||лямбда-выражение]]:

```java
Thread thread = new Thread(() -> System.out.println("Поток запущен"));
thread.start();
```

В отличие от [[Callable (интерфейс)||Callable]], [[Runnable (интерфейс)||Runnable]] не может возвращать значение или выбрасывать [[Исключение (Exception)||проверяемые исключения]].