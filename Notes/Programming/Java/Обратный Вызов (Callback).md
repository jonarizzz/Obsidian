**Callback (обратный вызов)** — это механизм, при котором один [[Объект (Object)||объект]] передает другому [[Объект (Object)||объекту]] [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылку]] на метод, который будет вызван позже, когда наступит определённое событие или завершится выполнение операции.
  
### Реализации:

1. Через [[Интерфейс (Interface)||интерфейс]] (наиболее распространенный способ)
2. С использованием [[Лямбда Функция (Lambda)||лямбда-выражений]] и [[Функциональный Интерфейс (Functional Interface)||функциональных интерфейсов]] (начиная с [[{TODO} Java 8||Java 8]])
3. Через [[Анонимный Класс (Anonymous Class)||анонимные классы]]


### Реализация через [[Интерфейс (Interface)||интерфейс]] (Классический способ)

Это стандартный способ, который использует [[Интерфейс (Interface)||интерфейс]] для передачи метода обратного вызова.

```java
// 1. Определяем интерфейс callback
interface Callback {
    void onComplete(String result);
}

// 2. Класс, выполняющий какую-то задачу и вызывающий callback
class Worker {
    void doWork(Callback callback) {
        System.out.println("Выполняется работа...");
        // Имитация долгой операции
        try { 
	        Thread.sleep(1000); 
		} catch (InterruptedException e) { 
			e.printStackTrace(); 
		}
        // Вызываем callback после завершения работы
        callback.onComplete("Работа завершена!");
    }
}

// 3. Основной класс с реализацией callback
public class Main {
    public static void main(String[] args) {
        Worker worker = new Worker();
        worker.doWork(new Callback() { // Передаем реализацию callback
            @Override
            public void onComplete(String result) {
                System.out.println("Callback получен: " + result);
            }
        });
    }
}
```

Вывод:

```
Выполняется работа...
Callback получен: Работа завершена!
```


### Использование [[Лямбда Функция (Lambda)||лямбд]] (начиная с [[{TODO} Java 8||Java 8]])

[[Лямбда Функция (Lambda)||Лямбда-выражения]] позволяют записать код короче и удобнее.

```java
@FunctionalInterface
interface Callback {
    void onComplete(String result);
}

class Worker {
    void doWork(Callback callback) {
        System.out.println("Выполняется работа...");
        try { 
	        Thread.sleep(1000); 
		} catch (InterruptedException e) { 
			e.printStackTrace(); 
		}
        callback.onComplete("Работа завершена!");
    }
}

public class Main {
    public static void main(String[] args) {
        Worker worker = new Worker();
        
        // Передаем лямбда-функцию вместо создания анонимного класса
        worker.doWork(result -> System.out.println("Callback получен: " + result));
    }
}
```

Вывод:

```
Выполняется работа...
Callback получен: Работа завершена!
```


### Использование [[Анонимный Класс (Anonymous Class)||анонимных классов]]

[[Анонимный Класс (Anonymous Class)||Анонимные классы]] могут заменить отдельный класс-обработчик.

```java
class Worker {
    void doWork(Callback callback) {
        System.out.println("Выполняется работа...");
        try { 
	        Thread.sleep(1000); 
		} catch (InterruptedException e) { 
			e.printStackTrace(); 
		}
        callback.onComplete("Готово!");
    }
}

public class Main {
    public static void main(String[] args) {
        Worker worker = new Worker();
        worker.doWork(new Callback() {
            @Override
            public void onComplete(String result) {
                System.out.println("Анонимный класс: " + result);
            }
        });
    }
}
```


### Где используются `callbacks`:

- [[Многопоточное Программирование (Многопоточка, Multithreading)||Асинхронное]] выполнение задач (например, [[CompletableFuture||CompletableFuture]] в [[{TODO} Java 8||Java 8]])
- Обработка событий в GUI (например, ActionListener в Swing)
- Реализация паттерна [[Паттерн Наблюдатель (Observer)||Observer]]
- Обработка [[{TODO} Http||HTTP-запросов]] (например, в Retrofit для Android)

  
### Что выбрать?

- Если нужно поддерживать старые версии Java (<8) → Используйте интерфейсы или анонимные классы.
- Если работаете с [[{TODO} Java 8||Java 8+]] → Используйте [[Лямбда Функция (Lambda)||лямбды]] и [[Функциональный Интерфейс (Functional Interface)||функциональные интерфейсы]].