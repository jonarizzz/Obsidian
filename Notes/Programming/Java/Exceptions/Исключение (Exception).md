
**Исключение (Exception)** — это [[Объект (Object)||объект]], который сигнализирует об ошибке или нестандартной ситуации во время выполнения программы.


### Иерархия:

- [[{TODO} RuntimeException||RuntimeException]] – непроверяемые исключения. Возникают во время выполнения программы. 
	- NoSuchElementException
	- IndexOutOfBoundsException
	- ArithmeticException
	- ClassCastException
	- NullPointerException
	- IlligalArgumentException
- SQLException
- IOException
	- EOFException
	- FileNotFoundException
- ReflectiveOperationException
	- NoSuchFieldException
	- IlligalAccessException
	- ClassNotFoundException
	- NoSuchMethodException

### Обработка: Используется [[{TODO} Try-Catch-Finally||try-catch-finally]]:

```java
try {
    int result = 10 / 0; // Ошибка деления на ноль
} catch (ArithmeticException e) {
    System.out.println("Ошибка: " + e.getMessage());
} finally {
    System.out.println("Этот блок выполняется всегда.");
}
```


### Создание собственного исключения:

```java
class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}
```


### Принудительный выброс исключения:

```java
throw new IllegalArgumentException("Некорректный аргумент");
```

  

  

Исключения помогают улучшить надежность кода и корректно обрабатывать ошибки. 🚀