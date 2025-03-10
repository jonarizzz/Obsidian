
**CharBuffer** — это [[Абстрактный Класс (Abstract Class)||абстрактный класс]] в пакете `java.nio`, который представляет собой буфер для хранения символов. Он реализует интерфейс [[CharSequence (интерфейс)||CharSequence]], что означает, что объекты CharBuffer могут использоваться как последовательности [[char||символов]], предоставляя доступ к методам интерфейса [[CharSequence (интерфейс)||CharSequence]].

### Основные особенности:

- CharBuffer является частью библиотеки `NIO (New I/O)` и используется для работы с буферами [[char||символов]], которые могут быть использованы для ввода/вывода (I/O) данных.
- Предоставляет методы для чтения и записи [[char||символов]], а также позволяет манипулировать позицией, лимитом и вместимостью буфера.
- Реализует все методы интерфейса [[CharSequence (интерфейс)||CharSequence]], например:
	- length()
	- charAt(int index)
	- subSequence(int start, int end)
	- toString()

Однако, в отличие от обычных классов, таких как [[String||String]], которые представляют собой [[Неизменяемый Объект (Immutable)||неизменяемые]] последовательности [[char||символов]], CharBuffer может быть изменяемым и работать с буферами данных.


### Пример использования:

```java
import java.nio.CharBuffer;

public class CharBufferExample {
    public static void main(String[] args) {
        CharBuffer buffer = CharBuffer.allocate(10);
        buffer.put("Hello");
		// Выведет 10 (максимальная емкость)
        System.out.println("Length: " + buffer.length());
        // Выведет 'H'
        System.out.println("Char at 0: " + buffer.charAt(0));
        // Выведет "Hel"
        System.out.println("SubSequence (0, 3): " + buffer.subSequence(0, 3));  
        // Переводим буфер в режим чтения
        buffer.flip();
        
        while (buffer.hasRemaining()) {
	        // Выведет "Hello"
            System.out.print(buffer.get());  
        }
    }
}
```