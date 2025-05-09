
**Состояние гонки** (Race Condition) - это ситуация, когда два или более [[Поток (Thread)||потока]] одновременно обращаются к общим данным или ресурсам, и результаты их операций зависят от того, в каком порядке выполняются операции. Это может привести к непредсказуемым и нежелательным результатам, таким как неправильные значения или ошибки в программе. В результате состояния гонки данные или ресурсы могут быть повреждены или использованы неправильно.

## Решения

Синхронизация с использованием ключевого слова [[Синхронизация Потоков (synchronized)||synchronized]]:

``` java
public synchronized void increment() {
    count++;
}
```

С помощью [[Синхронизация Потоков (synchronized)||синхронизации]] блока кода:

``` java
public void increment() {
    synchronized (this) {
        count++;
    }
}
```

Использование [[Локи (Locks)||Lock]] из `java.util.concurrent`:

``` java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Counter {
    private int count = 0;
    private Lock lock = new ReentrantLock();
	
    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();
        }
    }
	
    public int getCount() {
        return count;
    }
}
```

Использование [[Атомики (Atomics)||Атомиков]]:

``` java
import java.util.concurrent.atomic.AtomicInteger;

public class Counter {

    private AtomicInteger count = new AtomicInteger();

    public void increment() {
        count.incrementAndGet();
    }

    public int getCount() {
        return count.get();
    }
}
```

Если возможно, следует уменьшить количество точек взаимодействия между потоками или использовать [[Неизменяемый Объект (Immutable)||неизменяемые объекты]].