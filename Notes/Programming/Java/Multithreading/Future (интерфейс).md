`Future<T>` — это [[Интерфейс (Interface)||интерфейс]] из пакета `java.util.concurrent`, предназначенный для работы с [[Многопоточное Программирование (Многопоточка, Multithreading)||асинхронными задачами]]. Он представляет собой результат вычисления, которое может завершиться в будущем.


### Основные возможности `Future<T>`:

- Проверка, завершилась ли задача (`isDone()`).
- Отмена выполнения задачи (`cancel(boolean mayInterruptIfRunning)`).
- Проверка, была ли задача отменена (`isCancelled()`).
- Получение результата (`get()`), который блокирует выполнение до завершения задачи.
- Получение результата с таймаутом (`get(long timeout, TimeUnit unit)`).

### Пример использования `Future<T>`:

```java
import java.util.concurrent.*;

public class FutureExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();
		
        // Запускаем асинхронную задачу
        Future<Integer> future = executor.submit(() -> {
            Thread.sleep(2000); // Симуляция долгой операции
            return 42;
        });
		
        try {
            System.out.println("Ожидание результата...");
            Integer result = future.get(); // Блокируется, пока задача не завершится
            System.out.println("Результат: " + result);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```


### Недостатки `Future<T>`:

- **Блокирующий `get()`** — пока результат не готов, поток будет ждать.
- **Нет удобных механизмов обработки** — нельзя выполнить код после завершения задачи без явного вызова `get()`.


Из-за этих ограничений в [[{TODO} Java 8||Java 8]] был введен [[CompletableFuture||CompletableFuture]], который предлагает более мощные инструменты для работы с асинхронными задачами, такие как цепочки вызовов (`thenApply`, `thenAccept`, `handle`) и неблокирующие методы.