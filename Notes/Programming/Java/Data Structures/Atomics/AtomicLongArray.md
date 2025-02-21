AtomicLongArray аналогичен [[AtomicIntegerArray||AtomicIntegerArray]], но работает с массивами длинных чисел ([[Массив (Array)||"long[]"]]). Он предоставляет [[Атомарность (Atomacy)||атомарные]] операции для изменения значений в массиве без необходимости [[Синхронизация Потоков (synchronized)||синхронизации]].

### Операции:

- get(int index): Получает элемент массива по индексу.
- set(int index, long newValue): Устанавливает значение элемента массива по индексу.
- getAndSet(int index, long newValue): Получает текущий элемент массива и устанавливает новое значение.
- compareAndSet(int index, long expectedValue, long newValue): Пытается заменить элемент массива на новое значение, если текущий элемент равен ожидаемому.
- incrementAndGet(int index): Увеличивает элемент массива на 1 и возвращает результат.
- addAndGet(int index, long delta): Добавляет delta к элементу массива и возвращает результат.