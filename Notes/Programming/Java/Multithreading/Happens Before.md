**Happens Before** — это отношение между операциями, которое гарантирует, что результат одной операции будет виден другой, если между ними установлено это отношение. Оно используется в [[Многопоточное Программирование (Многопоточка, Multithreading)||многопоточной среде]] для предсказуемого поведения памяти и [[Синхронизация Потоков (synchronized)||синхронизации потоков]].

### Основные принципы Happens Before:

- Правило порядка внутри потока (Program Order Rule): В одном [[Поток (Thread)||потоке]] все операции происходят в том порядке, в котором они написаны в коде.
- Правило мониторной блокировки (Monitor Lock Rule): Разблокировка [[Синхронизация Потоков (synchronized)||synchronized-блока]] одним потоком happens before его последующей блокировки другим потоком.
- Правило volatile (Volatile Variable Rule): Запись в переменную, объявленную [[volatile||volatile]], happens before последующего чтения из неё.
- Правило запуска потока (Thread Start Rule): Вызов `Thread.start()` happens before любой код в запущенном [[Поток (Thread)||потоке]].
- Правило завершения потока (Thread Termination Rule): Завершение [[Поток (Thread)||потока]] happens before того, как другой поток обнаружит его завершение с помощью `Thread.join()` или `Thread.isAlive()`.
- Правило прерывания потока (Thread Interruption Rule): Вызов `Thread.interrupt()` happens before обнаружения прерывания с помощью `Thread.isInterrupted()` или [[{TODO} InterruptedException||InterruptedException]].
- Правило завершения статической инициализации (Finalizer Rule): Завершение конструктора объекта happens before начала работы метода `finalize()`.
- Транзитивность: Если `A` happens before `B`, а `B` happens before `C`, то `A` happens before `C`.


### Пример:

```java
class Example {
    private static boolean flag = false;
    private static int value = 0;
	
    public static void main(String[] args) {
        Thread writer = new Thread(() -> {
            value = 42;
            flag = true;
        });
		
        Thread reader = new Thread(() -> {
            if (flag) {
                System.out.println(value); // Может вывести 0, так как нет Happens Before между потоками
            }
        });
		
        writer.start();
        reader.start();
    }
}
```

В этом коде запись `flag = true` может произойти после чтения `flag`, так как нет механизма Happens Before между потоками. Если `flag` сделать [[volatile||volatile]], то `flag = true` гарантированно будет виден `reader`.