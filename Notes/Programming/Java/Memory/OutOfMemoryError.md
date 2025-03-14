OutOfMemoryError в Java — это [[{TODO} Error||ошибка]], возникающая, когда [[Виртуальная Машина Java (Java Virtual Machine, JVM)||JVM]] не может выделить больше памяти для выполнения программы. Она наследуется от [[{TODO} VirtualMachineError||VirtualMachineError]] и сигнализирует о критической нехватке ресурсов.


### Основные причины возникновения OutOfMemoryError

- **Heap space (куча переполнена)**
	- Происходит, когда в [[Heap (Область Памяти)||куче]] заканчивается память, а [[Сборщик Мусора (Garbage Collector, GC)||сборщик мусора]] не может освободить достаточно пространства.
	- Ошибка: `java.lang.OutOfMemoryError: Java heap space`
	- Причины:
		- Утечки памяти (неиспользуемые, но не освобождённые [[Объект (Object)||объекты]]).
		- Создание слишком большого количества [[Объект (Object)||объектов]].
		- Обработка больших файлов или данных без [[Многопоточное Программирование (Многопоточка, Multithreading)||потоковой]] обработки.

- **Metaspace (Java 8+) / PermGen (до Java 7 включительно)**
	- Происходит, когда метаданные [[Класс (Class)||классов]] заполняют Metaspace (или PermGen в старых версиях).
	- Ошибка: `java.lang.OutOfMemoryError: Metaspace`
	- Причины:
		- Динамическая загрузка [[Класс (Class)||классов]] без их выгрузки (например, при использовании [[{TODO} ClassLoader||ClassLoader]]).
		- Слишком много сгенерированных динамически [[Класс (Class)||классов]] (в фреймворках типа [[{TODO} Hibernate||Hibernate]], [[Спринг Фреймворк (Spring Framework)||Spring]]).

- **GC overhead limit exceeded**
	- [[Виртуальная Машина Java (Java Virtual Machine, JVM)||JVM]] тратит слишком много времени на [[Сборщик Мусора (Garbage Collector, GC)||сборку мусора]], но освобождает мало памяти.
	- Ошибка: `java.lang.OutOfMemoryError: GC overhead limit exceeded`
	- Обычно связано с утечками памяти или недостаточным выделением памяти для [[Виртуальная Машина Java (Java Virtual Machine, JVM)||JVM]].

- **Direct buffer memory**
	- Недостаточно памяти для выделения `ByteBuffer` вне [[Heap (Область Памяти)||кучи]].
	- Ошибка: `java.lang.OutOfMemoryError: Direct buffer memory`
	- Причины:
		- Использование `ByteBuffer.allocateDirect()` без освобождения.

- **Unable to create new native thread**
	- JVM не может создать новый [[Поток (Thread)||поток]] из-за нехватки системных ресурсов.
	- Ошибка: `java.lang.OutOfMemoryError: Unable to create new native thread`
	- Причины:
		- Достигнут лимит потоков ОС.
		- Утечка [[Поток (Thread)||потоков]] (например, не завершаются [[ExecutorService||ExecutorService]]).


### Способы решения

- **Увеличение памяти**
	- Для кучи: `java -Xmx2G -Xms512M MyApp`
	- Для Metaspace: `java -XX:MaxMetaspaceSize=256M`
- **Профилирование и анализ утечек**: использовать `VisualVM`, `YourKit`, `Eclipse MAT` или `jcmd`
- **Использование потоковой обработки (streaming)**: например, для больших файлов вместо загрузки всего в память:
```java
try (BufferedReader reader = new BufferedReader(new FileReader("bigfile.txt"))) {
    reader.lines().forEach(System.out::println);
}
```
- **Ручное управление ByteBuffer**: освобождение прямой памяти:
```java
((DirectBuffer) byteBuffer).cleaner().clean();
```
- **Ограничение количества [[Поток (Thread)||потоков]]**: например, в ExecutorService:
```java
ExecutorService executor = Executors.newFixedThreadPool(10);
```
