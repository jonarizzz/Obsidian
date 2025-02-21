String — это неизменяемый ([[Неизменяемый Объект (Immutable)||immutable]]) объект, представляющий последовательность [[char||символов]]. Он является частью пакета `java.lang`, поэтому его не нужно импортировать.

### Основные особенности

- [[Неизменяемый Объект (Immutable)||Неизменяемость (Immutable)]] – после создания объект String нельзя изменить. Все операции, такие как конкатенация или замена символов, создают новый объект.
- Хранение в пуле строк ([[Пул Литералов (String Pool, Literal Pool)||String Pool]]) – литералы строк автоматически кэшируются в специальном пуле для экономии памяти.
- Реализует интерфейс [[CharSequence (интерфейс)||CharSequence]] – это позволяет работать со строками так же, как с [[StringBuilder||StringBuilder]], [[StringBuffer||StringBuffer]] и [[CharBuffer||CharBuffer]].

### Создание строк

1. Через строковый литерал (рекомендуемый способ):
```java
String str1 = "Hello, Java!";
```

1. Через `new` (создает новый объект в памяти):
```java
String str2 = new String("Hello, Java!");
```

Этот вариант не использует пул строк, что приводит к созданию нового объекта.

### Основные методы

|**Метод**|**Описание**|
|---|---|
|length()|Возвращает длину строки|
|charAt(int index)|Возвращает символ по индексу|
|substring(int start, int end)|Извлекает подстроку|
|indexOf(String s)|Возвращает индекс первого вхождения подстроки|
|contains(CharSequence s)|Проверяет, содержится ли подстрока|
|replace(String old, String new)|Заменяет одну подстроку на другую|
|split(String regex)|Разбивает строку на массив подстрок|
|toLowerCase()|Преобразует в нижний регистр|
|toUpperCase()|Преобразует в верхний регистр|
|trim()|Убирает пробелы в начале и конце|

### Конкатенация (склеивание) строк

1. Через `+` (неэффективно, создает новый объект):
```java
String fullName = "John" + " " + "Doe";
```

2. Через `concat()` (лучше, но также создает новый объект):
```java
String fullName = "John".concat(" Doe");
```

1. Через [[StringBuilder||StringBuilder]] (оптимальный вариант при множественных операциях):
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World!");
System.out.println(sb.toString()); // "Hello World!"
```

### Сравнение строк

Поскольку String — это объект, его сравнение через `==` проверяет ссылки, а не содержимое:
```java
String s1 = "Hello";
String s2 = new String("Hello");

System.out.println(s1 == s2);  // false (разные объекты)
System.out.println(s1.equals(s2));  // true (сравнивает содержимое)
```

Используйте `equals()` для корректного сравнения строк.

### Преобразование типов

Из числа в строку:
```java
int num = 42;
String str = String.valueOf(num); // "42"
```

Из строки в число:
```java
int num = Integer.parseInt("42"); // 42
```
