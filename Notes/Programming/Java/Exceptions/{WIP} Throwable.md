**Throwable** — это базовый класс для всех исключений и ошибок. 

### Иерархия:

- [[Исключение (Exception)||Exception]] – представляет проверяемые исключения (checked exceptions), которые нужно обрабатывать с помощью [[{TODO} Try-Catch-Finally||try-catch]] или объявлять в `throws`.
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
- [[{TODO} Error||Error]] – представляет критические ошибки, возникающие в среде выполнения, которые обычно нельзя обработать.
	- ThreadDeath
	- VirtualMachineError
		- UnknownError
		- StackOverflowError
		- OutOfMemoryError


### Методы:

- `getMessage()` – получает сообщение об ошибке.
- `getCause()` – получает причину исключения.
- `printStackTrace()` – выводит стек вызовов.

  
Используется в [[{TODO} Try-Catch-Finally||механизме обработки исключений (try-catch-finally)]] и для проброса ошибок (throw / throws).