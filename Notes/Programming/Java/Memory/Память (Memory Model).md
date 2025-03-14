[[{TODO} Java||Java]] управляет памятью автоматически с помощью [[Виртуальная Машина Java (Java Virtual Machine, JVM)||JVM]] и [[Сборщик Мусора (Garbage Collector, GC)||Garbage Collector]].

### Основные области памяти:

- [[Heap (Область Памяти)||Heap (Куча)]] – хранит объекты, управляется GC.
	- Young Generation (новые объекты).
	- Old Generation (долгоживущие объекты).
	- Metaspace (метаданные классов).
- [[Stack (Область Памяти)||Stack (Стек)]] – хранит локальные переменные и вызовы методов.
- PC Register – хранит текущую команду потока.
- Native Method Stack – используется для JNI-вызовов.

### Garbage Collector (GC):

Удаляет неиспользуемые объекты автоматически. Основные алгоритмы:

- [[Serial GC||Serial GC]] – для малых приложений.
- [[Parallel GC||Parallel GC]] – многопоточный, для быстродействия.
- [[G1 GC||G1 GC]] – баланс между паузами и производительностью.
- [[ZGC||ZGC]], [[Shenandoah GC||Shenandoah]] – минимальные паузы.

### Проблемы с памятью:

- [[Утечка Памяти (Memory Leak)||Memory Leak]] – утечки памяти из-за неочищенных ссылок.
- [[OutOfMemoryError||OutOfMemoryError]] – нехватка памяти в куче.
- [[StackOverflowError||StackOverflowError]] – слишком глубокая рекурсия.

### Оптимизация:

- Очищать ненужные ссылки.
- Использовать [[Слабая Ссылка (WeakReference)||WeakReference]] для кешей.
- Настроить [[Сборщик Мусора (Garbage Collector, GC)||GC]] (`-XX:+UseG1GC`).
- Анализировать память с `VisualVM`, `JConsole`, `JProfiler`.

