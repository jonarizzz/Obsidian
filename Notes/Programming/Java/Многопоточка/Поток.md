**Поток** — это “легковесный” подпроцесс, который выполняется внутри [[Процесс||процесса]]. Один процесс может иметь несколько потоков.

## Создание потоков

#### 1. Наследование от Thread

Создать новый поток можно, унаследовавшись от класса `Thread` и переопределив его метод `run()`:

``` java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start(); // Запускает поток
    }
}
```
#### 2. Реализация интерфейса Runnable

Интерфейс `Runnable` позволяет внедрить многопоточность в существующий класс:

``` java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable is running");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start();
    }
}
```
#### 3. Использование Callable и Future

Если нужно вернуть результат из потока, используют `Callable` и `Future`:

``` java 
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) throws Exception {
        Callable<Integer> task = () -> {
            return 123;
        };
        
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> future = executor.submit(task);
        
        System.out.println("Result: " + future.get()); // Ожидание результата
        executor.shutdown();
    }
}
```


## Управление потоками

- `start()`: запускает поток.
- `run()`: выполняет код потока (не запускает поток в отдельном потоке).
- `join()`: приостанавливает текущий поток до завершения другого.
- `sleep(milliseconds)`: заставляет поток “уснуть” на определённое время.
- `interrupt()`: прерывает поток.