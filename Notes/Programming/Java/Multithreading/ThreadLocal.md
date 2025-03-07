**ThreadLocal** — это механизм, предоставляющий каждому [[Поток (Thread)||потоку]] в Java свой собственный экземпляр переменной, который доступен только этому [[Поток (Thread)||потоку]]. То есть, значение переменной, помеченной как [[ThreadLocal||ThreadLocal]], будет уникальным для каждого [[Поток (Thread)||потока]], и другие [[Поток (Thread)||потоки]] не смогут получить доступ к этому значению.

Это может быть полезно, например, при хранении данных, которые не должны быть совместно использованы между [[Поток (Thread)||потоками]], таких как информация о сессии, текущий пользователь или конфигурационные параметры, которые могут изменяться в разных [[Поток (Thread)||потоках]].


### Пример использования:

```java
public class ThreadLocalExample {
	
    private static ThreadLocal<Integer> threadLocalValue = ThreadLocal.withInitial(() -> 0);
	
    public static void main(String[] args) throws InterruptedException {
        // Запуск нескольких потоков
        Thread thread1 = new Thread(() -> {
            threadLocalValue.set(10);
            System.out.println("Thread 1 value: " + threadLocalValue.get());
        });
		
        Thread thread2 = new Thread(() -> {
            threadLocalValue.set(20);
            System.out.println("Thread 2 value: " + threadLocalValue.get());
        });
		
        thread1.start();
        thread2.start();
		
        thread1.join();
        thread2.join();
    }
}
```

В этом примере, каждый [[Поток (Thread)||поток]] получает свою собственную переменную, и результат будет:

```text
Thread 1 value: 10
Thread 2 value: 20
```


###  Методы:

- `ThreadLocal.withInitial(Supplier<T> supplier)` — создаёт новый [[ThreadLocal||ThreadLocal]] с начальным значением, которое предоставляется через `supplier`.
- `get()` — возвращает значение переменной для текущего [[Поток (Thread)||потока]].
- `set(T value)` — задает значение переменной для текущего [[Поток (Thread)||потока]].
- `remove()` — удаляет значение, ассоциированное с текущим [[Поток (Thread)||потоком]].
