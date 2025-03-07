**ThreadPoolExecutor** — это [[Класс (Class)||класс]] из пакета `java.util.concurrent`, который управляет [[Thread Pool||пулом потоков]] и выполняет задачи асинхронно. Он используется для эффективного управления [[Многопоточное Программирование (Многопоточка, Multithreading)||многозадачностью]], позволяя повторно использовать [[Поток (Thread)||потоки]], что значительно уменьшает накладные расходы на создание новых [[Поток (Thread)||потоков]].


### Основные особенности:

- [[Thread Pool||Пул потоков]]: Он создает [[Thread Pool||пул потоков]], который управляет несколькими [[Поток (Thread)||потоками]] и повторно использует их для выполнения задач, что позволяет избежать накладных расходов на создание и уничтожение [[Поток (Thread)||потоков]].
- **Работа с задачами**: [[ThreadPoolExecutor||ThreadPoolExecutor]] принимает задачи в виде объектов [[Runnable (интерфейс)||Runnable]] или [[Callable (интерфейс)||Callable]], которые могут быть выполнены в параллельных [[Поток (Thread)||потоках]].


### Конфигурация:
- `corePoolSize`: минимальное количество [[Поток (Thread)||потоков]], которые остаются в [[Thread Pool||пуле]].
- `maximumPoolSize`: максимальное количество [[Поток (Thread)||потоков]], которое может быть в [[Thread Pool||пуле]].
- `keepAliveTime`: время, в течение которого [[Поток (Thread)||поток]] будет ожидать выполнения задачи перед завершением.
- `workQueue`: [[Очередь (Queue)||очередь]], в которой задачи ожидают выполнения, если все [[Поток (Thread)||потоки]] заняты.


### Пример использования:

```java
import java.util.concurrent.*;

public class ThreadPoolExecutorExample {
    public static void main(String[] args) {
        int corePoolSize = 2;
        int maximumPoolSize = 4;
        long keepAliveTime = 10;
		
        // Создание пула с параметрами
        ThreadPoolExecutor executor = new ThreadPoolExecutor(
            corePoolSize,
            maximumPoolSize,
            keepAliveTime,
            TimeUnit.SECONDS,
            new LinkedBlockingQueue<Runnable>()
        );
		
        // Добавление задач в пул
        for (int i = 0; i < 10; i++) {
            final int taskId = i;
            executor.submit(() -> {
                System.out.println("Executing task " + taskId + " in thread " + Thread.currentThread().getName());
            });
        }
		
        // Закрытие пула
        executor.shutdown();
    }
}
```

В этом примере [[Thread Pool||пул потоков]] создает от 2 до 4 потоков в зависимости от нагрузки, выполняя 10 задач. Каждая задача выводит свой идентификатор и имя [[Поток (Thread)||потока]], который ее выполняет.