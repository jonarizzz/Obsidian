`CompletableFuture` — это класс в Java, представляющий собой улучшенную версию [[Future (интерфейс)||Future]], который используется для работы с [[Многопоточное Программирование (Многопоточка, Multithreading)||асинхронными задачами]]. Он был добавлен в [[{TODO} Java 8||Java 8]] и предоставляет мощный API для работы с отложенными вычислениями, позволяя легко управлять [[Многопоточное Программирование (Многопоточка, Multithreading)||многопоточностью]] и выполнять операции без [[Блокировки (Locking)||блокировки]] основного [[Поток (Thread)||потока]]. Он упрощает управление потоками и позволяет строить сложные асинхронные цепочки без явного использования [[Поток (Thread)||Thread]] и [[{TODO} ExecutorService||ExecutorService]]

### Основные возможности:

- **[[Многопоточное Программирование (Многопоточка, Multithreading)||Асинхронное]] выполнение задач** — позволяет запускать задачи в отдельных [[Поток (Thread)||потоках]] без блокировки главного [[Поток (Thread)||потока]].
- Цепочки обработки (`thenApply`, `thenAccept`, `thenCompose`) — можно задавать последовательность операций.
- Комбинирование (`allOf`, `anyOf`) — объединение нескольких `CompletableFuture`.
- Обработка [[{TODO} Исключение (Exception)||исключений]] (`exceptionally`, `handle`) — упрощает работу с [[{TODO} Исключение (Exception)||ошибками]].
- Возможность вручную завершить (`complete`, `completeExceptionally`) — можно самому управлять состоянием `CompletableFuture`.


### Пример использования


##### Запуск асинхронной задачи

```java
import java.util.concurrent.CompletableFuture;

public class AsyncExample {
    public static void main(String[] args) {
        CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
            System.out.println("Запускаем фоновую задачу в потоке: " +
            Thread.currentThread().getName());
        });
		
        future.join(); // Дожидаемся завершения
    }
}
```

`runAsync` запускает задачу, не возвращающую результат.


##### Асинхронный возврат результата (`supplyAsync`)

```java
import java.util.concurrent.CompletableFuture;

public class SupplyExample {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            return "Привет, мир!";
        });
		
        System.out.println(future.join()); // Выведет: Привет, мир!
    }
}
```

`supplyAsync` выполняет задачу и возвращает результат.


##### Цепочка вызовов (`thenApply`, `thenAccept`)

```java
import java.util.concurrent.CompletableFuture;

public class ChainingExample {
    public static void main(String[] args) {
        CompletableFuture.supplyAsync(() -> "Java")
            .thenApply(str -> str + " CompletableFuture") // Преобразуем результат
            .thenAccept(System.out::println) // Выводим
            .join(); // Дожидаемся завершения
    }
}
```

`thenApply` изменяет результат, `thenAccept` выполняет действие без изменения результата.


##### Объединение нескольких `CompletableFuture`

```java
import java.util.concurrent.CompletableFuture;

public class CombineExample {
    public static void main(String[] args) {
        CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> "Привет");
        CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> "мир");
		
        CompletableFuture<String> combined = future1.thenCombine(future2, (res1, res2) -> res1 + ", " + res2 + "!");
        
        System.out.println(combined.join()); // Выведет: Привет, мир!
    }
}
```

`thenCombine` объединяет два `CompletableFuture`.


##### Обработка ошибок

```java
import java.util.concurrent.CompletableFuture;

public class ExceptionExample {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            if (true) throw new RuntimeException("Ошибка!");
            return "Успех";
        }).exceptionally(ex -> "Ошибка обработана: " + ex.getMessage());
		
        System.out.println(future.join()); // Выведет: Ошибка обработана: java.lang.RuntimeException: Ошибка!
    }
}
```

`exceptionally` позволяет обработать [[{TODO} Исключение (Exception)||исключения]] и вернуть альтернативный результат.
