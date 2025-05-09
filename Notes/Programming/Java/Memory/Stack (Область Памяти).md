
**Стек** — это часть оперативной памяти, которая используется для хранения **вызовов методов**, **локальных переменных** и **адресов возврата**. Он организован по принципу [[Стек (Stack)||LIFO (Last In, First Out)]], то есть последний добавленный элемент извлекается первым.


### Основные особенности стека в Java

- Разделение на фреймы (Stack Frames)
	- Каждый вызов метода создает новый **кадр стека (Stack Frame)**.
	- Когда метод завершает выполнение, его фрейм удаляется, и управление передается предыдущему методу.
- Хранение данных
	- Локальные переменные [[Примитивные Типы Данных (Primitives)||примитивных типов]].
	- [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||Ссылки на объекты]] (но сами [[Объект (Object)||объекты]] хранятся в [[Heap (Область Памяти)||куче]]).
	- Адрес возврата после завершения метода.
- Автоматическое управление памятью – Java автоматически очищает стек: при выходе из метода его фрейм уничтожается.
- Размер стека ограничен
	- У каждого [[Поток (Thread)||потока]] свой стек, и его размер можно задать через параметр `-Xss` (например, `-Xss512k` для `512 KB`).
	- Если стек переполняется из-за глубоких рекурсий или бесконечных вызовов методов, возникает [[StackOverflowError||StackOverflowError]].


### Пример работы стека

```java
public class StackExample {
    public static void main(String[] args) {
        methodA();
    }
	
    static void methodA() {
        int a = 10;  // Локальная переменная в стеке
        methodB();
    }
	
    static void methodB() {
        int b = 20;  // Новая переменная в новом фрейме стека
        methodC();
    }
	
    static void methodC() {
        int c = 30;  // Опять новая переменная в новом фрейме
    }
}
```

Как это выглядит в стеке:

```
[Frame methodC] → c = 30  // Текущий кадр
[Frame methodB] → b = 20
[Frame methodA] → a = 10
[Frame main] 
```

После выхода из `methodC()`, его фрейм удаляется, затем удаляется `methodB()`, и так далее, пока стек не очистится.


### Стек и многопоточное программирование

- У каждого [[Поток (Thread)||потока]] свой отдельный стек.
- Это значит, что локальные переменные одного [[Поток (Thread)||потока]] не видны в другом [[Поток (Thread)||потоке]].
- [[Объект (Object)||Объекты]], на которые указывают [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылки]] в стеке, могут находиться в [[Heap (Область Памяти)||куче]] и быть общими для всех потоков.