**Starvation (голодание)** — это ситуация, когда один или несколько [[Поток (Thread)||потоков]] не получают доступа к ресурсу из-за того, что другие [[Поток (Thread)||потоки]] постоянно его захватывают. Starvation — это несправедливое распределение ресурсов, когда одни [[Поток (Thread)||потоки]] «голодают», а другие постоянно работают.


### Как возникает:

- [[Поток (Thread)||Потоки]] с более высоким приоритетом постоянно выполняются, а низкоприоритетный поток не получает процессорное время.
- Неравномерное распределение [[Синхронизация Потоков (synchronized)||блокировок]], например, поток не может получить доступ к [[Синхронизация Потоков (synchronized)||synchronized]]-методу, потому что другие [[Поток (Thread)||потоки]] его постоянно занимают.
- Неограниченный доступ к ресурсу, когда жадные [[Поток (Thread)||потоки]] (например, в `ReentrantLock.tryLock()`) постоянно перехватывают его.


### Пример starvation:

Один [[Поток (Thread)||поток]] с высоким [[Приоритет Потока (Thread Priority)||приоритетом]] постоянно выполняется, а [[Поток (Thread)||поток]] с низким [[Приоритет Потока (Thread Priority)||приоритетом]] почти не получает процессорного времени:

```java
class StarvationExample {
    public static void main(String[] args) {
        Runnable task = () -> {
            while (true) {
                System.out.println(Thread.currentThread().getName() + " выполняется...");
                try { Thread.sleep(100); } catch (InterruptedException ignored) {}
            }
        };
		
        Thread highPriority = new Thread(task, "Высокий приоритет");
        Thread lowPriority = new Thread(task, "Низкий приоритет");
		
        highPriority.setPriority(Thread.MAX_PRIORITY); // 10
        lowPriority.setPriority(Thread.MIN_PRIORITY);  // 1
		
        highPriority.start();
        lowPriority.start();
    }
}
```


### Как избежать starvation?

- Использовать fair-блокировки, например, [[ReentrantLock||new ReentrantLock(true)]], чтобы [[Поток (Thread)||потоки]] получали ресурс в порядке [[Очередь (Queue)||очереди]].
- Избегать крайних [[Приоритет Потока (Thread Priority)||приоритетов]] (`Thread.MIN_PRIORITY` и `Thread.MAX_PRIORITY`).
- Использовать `wait()` / `notify()`, `Thread.yield()`, чтобы дать шанс другим [[Поток (Thread)||потокам]].