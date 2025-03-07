ExecutorService — это [[Интерфейс (Interface)||интерфейс]], который предоставляет API для управления [[Thread Pool||пулом потоков]].

  
### ExecutorService управляет пулом потоков

Когда создаётся [[Thread Pool||пул потоков]] (например, через `Executors.newFixedThreadPool(n)`), он возвращает экземпляр [[ExecutorService||ExecutorService]]. Этот [[Объект (Object)||объект]] управляет созданием, исполнением и завершением [[Поток (Thread)||потоков]].


### Пул потоков выполняет задачи

Вместо создания потоков вручную, можно отправлять задачи ([[Runnable (интерфейс)||Runnable]] или [[Callable (интерфейс)||Callable]]) в [[ExecutorService||ExecutorService]], а он сам распределяет их между доступными [[Поток (Thread)||потоками]] в [[Thread Pool||пуле]].


### Гибкость в управлении потоками

[[ExecutorService||ExecutorService]] позволяет управлять жизненным циклом [[Thread Pool||пула]]:

- `shutdown()` — завершает приём новых задач, но выполняет оставшиеся.
- `shutdownNow()` — пытается остановить все выполняемые задачи.
- `awaitTermination(timeout, unit)` — ожидает завершения всех задач в течение заданного времени.


### Пример кода:

```java
import java.util.concurrent.*;

public class ThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);
		
        for (int i = 1; i <= 5; i++) {
            final int taskNumber = i;
            executor.submit(() -> {
                System.out.println("Task " + taskNumber + " выполняется в " + Thread.currentThread().getName());
                try {
                    Thread.sleep(1000); // Симуляция работы
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            });
        }
		
        executor.shutdown(); // Завершаем приём задач
    }
}
```


### Имплементации в стандартной библиотеке:

- **[[ThreadPoolExecutor||ThreadPoolExecutor]]** – наиболее гибкая и мощная реализация, лежащая в основе большинства фабричных методов Executors. Позволяет настраивать количество потоков, политику очереди, таймауты и обработку отказов.
	- Можно создавать вручную или через фабричные методы.
	- Позволяет ограничивать количество потоков, управлять стратегиями отбрасывания задач (RejectedExecutionHandler).
- **ScheduledThreadPoolExecutor** – расширяет ThreadPoolExecutor, добавляя поддержку выполнения задач с задержкой или периодическим запуском.
	- Используется для задач типа “запустить через 10 секунд” или “повторять каждые 5 минут”.

Также доступны удобные фабричные методы в классе Executors:

- **Executors.newFixedThreadPool(int nThreads)**
	- Создаёт пул фиксированного размера `nThreads`.
	- Потоки используются повторно, если доступны.
- **Executors.newCachedThreadPool()**
	- Динамически создаёт потоки по мере необходимости.
	- Неограниченное количество потоков (если требуется).
	- Неиспользуемые потоки завершаются через 60 секунд.
- **Executors.newSingleThreadExecutor()**
	- Создаёт пул с одним потоком.
	- Очередь бесконечная, задачи выполняются последовательно.
- **Executors.newScheduledThreadPool(int corePoolSize)**
	- Основан на ScheduledThreadPoolExecutor.
	- Поддерживает отложенное и периодическое выполнение задач.
- **Executors.newSingleThreadScheduledExecutor()**
	- Однопоточная версия ScheduledThreadPoolExecutor.