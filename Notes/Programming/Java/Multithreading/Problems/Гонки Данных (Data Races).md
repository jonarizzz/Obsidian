
Гонка данных возникает, когда два или более [[Поток (Thread)||потока]] одновременно обращаются к одной переменной, и хотя бы один из них её изменяет, при этом отсутствует соответствующая [[Синхронизация Потоков (synchronized)||синхронизация]]. Это частный случай [[Состояние Гонки (Race Condition)||состояния гонки]], связанный с небезопасной конкурентной модификацией памяти.

### Пример гонки данных:

```java
class SharedResource {
    int counter = 0;
	
    void increment() {
        counter++; // Операция не атомарна!
    }
}

public class DataRaceExample {
    public static void main(String[] args) throws InterruptedException {
        SharedResource resource = new SharedResource();
		
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                resource.increment();
            }
        });
		
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                resource.increment();
            }
        });
		
        t1.start();
        t2.start();
        t1.join();
        t2.join();
		
        System.out.println("Counter: " + resource.counter); // Ожидали 2000, а получаем меньше
    }
}
```

**Почему это гонка данных?**

- Операция `counter++` не [[Атомарность (Atomacy)||атомарна]] (разбивается на чтение, увеличение и запись).
- [[Поток (Thread)||Потоки]] могут одновременно читать и записывать `counter`, приводя к потере обновлений.

### Как исправить?

Использовать [[Синхронизация Потоков (synchronized)||synchronized]] или [[AtomicInteger||AtomicInteger]]:

```java
class SharedResource {
    private final AtomicInteger counter = new AtomicInteger(0);
	
    void increment() {
        counter.incrementAndGet();
    }
}
```