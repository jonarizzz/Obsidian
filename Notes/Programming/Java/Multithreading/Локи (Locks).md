Локи (Locks) используются для управления доступом к ресурсам при работе с [[Многопоточное Программирование (Многопоточка, Multithreading)||многопоточностью]]. Они предоставляют более гибкие и функциональные механизмы синхронизации по сравнению с ключевым словом [[Синхронизация Потоков (synchronized)||synchronized]]. Основной интерфейс для работы с локами в Java — это `java.util.concurrent.locks.Lock`.


## Важные интерфейсы и классы

- **Lock:** Базовый интерфейс, предоставляющий основные методы:
	- lock() — захватывает лок, блокируя поток до его освобождения.
	- unlock() — освобождает лок.
	- tryLock() — пытается захватить лок без блокировки, возвращая true в случае успеха.
	- tryLock(long time, TimeUnit unit) — пытается захватить лок в течение заданного времени.
	- lockInterruptibly() — захватывает лок, но поток может быть прерван во время ожидания.
- [[ReentrantLock||ReentrantLock]]: Реализация интерфейса Lock, поддерживающая:
	- **Рекурсивную блокировку**: Тот же поток может захватить лок несколько раз, и он освободится только после соответствующего количества вызовов unlock.
	- **Честность**: Возможность настроить приоритет доступа (например, с флагом true в конструкторе).
- **ReadWriteLock:** Интерфейс, позволяющий разделить доступ на чтение и запись:
	- readLock() — позволяет нескольким потокам одновременно читать, если ни один поток не выполняет запись.
	- writeLock() — позволяет только одному потоку выполнять запись, блокируя других.
- **StampedLock:** Более производительная альтернатива ReadWriteLock, которая поддерживает оптимистичные чтения, где блокировка вообще может не требоваться.


## Имплементация

``` java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class LockExample {
    private final Lock lock = new ReentrantLock();
    private int counter = 0;
	
    public void increment() {
        lock.lock(); // Захват лока
        try {
            counter++;
        } finally {
            lock.unlock(); // Освобождение лока
        }
    }
	
    public int getCounter() {
        lock.lock();
        try {
            return counter;
        } finally {
            lock.unlock();
        }
    }
	
    public static void main(String[] args) throws InterruptedException {
        LockExample example = new LockExample();
		
        Thread t1 = new Thread(example::increment);
        Thread t2 = new Thread(example::increment);
		
        t1.start();
        t2.start();
		
        t1.join();
        t2.join();
		
        System.out.println("Counter: " + example.getCounter());
    }
}
```