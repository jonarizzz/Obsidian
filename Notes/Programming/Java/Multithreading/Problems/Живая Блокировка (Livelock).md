**Livelock** — это ситуация, когда [[Поток (Thread)||потоки]] не блокируются (как при [[Взаимная блокировка (Deadlock)||deadlock]]), но бесконечно реагируют друг на друга, не выполняя реальной работы. Livelock — это бесконечные попытки «уступить дорогу» без прогресса.


### Пример:

Два [[Поток (Thread)||потока]] (человека) уступают дорогу друг другу, но продолжают ждать:

```java
class Person {
    private boolean moved = false;
    public boolean hasMoved() { return moved; }
    public void move(Person other) {
        while (other.hasMoved()) { // Ждём другого
            System.out.println(Thread.currentThread().getName() + " ждёт...");
        }
        moved = true;
        System.out.println(Thread.currentThread().getName() + " двигается!");
    }
}

public class LivelockExample {
    public static void main(String[] args) {
        Person p1 = new Person(), p2 = new Person();
        new Thread(() -> p1.move(p2), "Человек 1").start();
        new Thread(() -> p2.move(p1), "Человек 2").start();
    }
}
```


### Как избежать:

- Ограничить количество попыток (таймер, счётчик).
- Добавить случайные задержки (`Thread.sleep(randomDelay)`).
- Назначить [[Приоритет Потока (Thread Priority)||приоритеты]] (например, один [[Поток (Thread)||поток]] всегда двигается первым).