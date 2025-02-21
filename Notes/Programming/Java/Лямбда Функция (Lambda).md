Лямбда-функция (или **lambda-выражение**) в Java (начиная с [[{TODO} Java 8||Java 8]]) — это компактный способ записи [[Анонимный Класс (Anonymous Class)||анонимного класса]], реализующего [[Функциональный Интерфейс (Functional Interface)||функциональный интерфейс]]. Лямбда-выражения позволяют писать более короткий и читаемый код, особенно при работе с [[Функциональный Интерфейс (Functional Interface)||функциональными интерфейсами]], такими как [[{TODO} Comparator (интерфейс)||Comparator]], [[{TODO} Runnable (интерфейс)||Runnable]], [[{TODO} Consumer (интерфейс)||Consumer]] и другие.


### Синтаксис

```java
(параметры) -> { тело_функции }
```

Если тело состоит из одного выражения, {} можно опустить:
```java
(параметры) -> выражение
```

Если параметр один, скобки () тоже можно опустить:
```java
param -> выражение
```


### Примеры использования


#### Лямбда вместо анонимного класса

Рассмотрим пример с `Comparator<String>`, который сортирует [[String||строки]] по длине.

**Без лямбды (обычный [[Анонимный Класс (Anonymous Class)||анонимный класс]])**
```java
Comparator<String> comparator = new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return Integer.compare(s1.length(), s2.length());
    }
};
```

**С использованием лямбды**
```java
Comparator<String> comparator = (s1, s2) -> Integer.compare(s1.length(), s2.length());
```


#### Лямбда в потоке (Stream API)

Фильтрация [[ArrayList||списка]] [[String||строк]], оставляя только те, которые длиннее 3 символов:

```java
List<String> words = Arrays.asList("Java", "Lambda", "Code", "Hi");
words.stream()
     .filter(word -> word.length() > 3)
     .forEach(System.out::println);
```


#### Использование в Runnable

**Обычный способ**

```java
Thread t = new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Выполняется поток");
    }
});
t.start();
```

**С лямбдой**

```java
Thread t = new Thread(() -> System.out.println("Выполняется поток"));
t.start();
```


### Функциональные интерфейсы

Лямбды можно использовать только с [[Функциональный Интерфейс (Functional Interface)||функциональными интерфейсами]] — это интерфейсы, у которых есть только один абстрактный метод.

Примеры таких интерфейсов в `java.util.function`:

- `Consumer<T>` — принимает значение, ничего не возвращает (`void accept(T t)`)
- `Supplier<T>` — ничего не принимает, возвращает значение (`T get()`)
- `Function<T, R>` — принимает значение и возвращает результат (`R apply(T t)`)
- `Predicate<T>` — принимает значение и возвращает [[boolean||boolean]] (`boolean test(T t)`)