**Callable** — это [[Функциональный Интерфейс (Functional Interface)||функциональный интерфейс]] в Java, который представляет задачу, возвращающую результат и потенциально выбрасывающую [[Исключение (Exception)||исключение]].
  

### Основные моменты:

- Находится в пакете `java.util.concurrent`.
- Метод `V call() throws Exception` выполняет задачу и возвращает результат.
- В отличие от [[Runnable (интерфейс)||Runnable]], позволяет вернуть значение и выбросить [[Исключение (Exception)||проверяемое исключение]].
- Используется с [[ExecutorService||ExecutorService]] для выполнения фоновых задач, например, через [[Future (интерфейс)||Future<T>]].


### Пример использования:

```java
import java.util.concurrent.*;

public class CallableExample {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newSingleThreadExecutor();
		
        Callable<String> task = () -> {
            Thread.sleep(1000);
            return "Результат задачи";
        };
		
        Future<String> future = executor.submit(task);
        System.out.println(future.get()); // Ожидание результата
		
        executor.shutdown();
    }
}
```

Здесь [[Callable (интерфейс)||Callable]] выполняется в отдельном [[Поток (Thread)||потоке]], и результат получаем через `Future.get()`