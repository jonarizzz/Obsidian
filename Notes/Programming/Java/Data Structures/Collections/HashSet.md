HashSet — это [[Collection (интерфейс)||коллекция]] в языке программирования Java, которая реализует [[{TODO} Set (интерфейс)||интерфейс Set]]. Она хранит уникальные элементы и не допускает дублирования. Элементы в HashSet не упорядочены, то есть не имеют фиксированного порядка, в котором они были добавлены.

### Основные особенности:

- **Уникальность элементов**: Все элементы уникальны, и при попытке добавить элемент, который уже существует в наборе, он не будет добавлен.
- **Быстрая работа**: Внутри использует [[Хэш-таблица (Hash Table)||хеш-таблицу]], что обеспечивает очень быструю операцию поиска (в среднем $O(1)$).
- **Неупорядоченность**: Порядок элементов не сохраняется и не может быть предсказан, поскольку они распределяются по [[Хэш-таблица (Hash Table)||хеш-таблице]] на основе их [[Хэширование (Хэш-функция, Hash Function, Hashing)||хеш-кодов]].
- **Не допускает null (не всегда)**: Хотя HashSet поддерживает `null` элементы, в случае если `null` пытаются добавить несколько раз, он будет считаться одним и тем же элементом.

### Пример использования:

```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();
		
        // Добавляем элементы
        set.add("Apple");
        set.add("Banana");
        set.add("Orange");
        set.add("Apple"); // Этот элемент не будет добавлен
		
        // Печатаем элементы
        System.out.println(set); // [Apple, Banana, Orange]
    }
}
```

В этом примере добавление элемента `"Apple"` второй раз не повлияет на результат, поскольку элементы в HashSet должны быть уникальными.

### Основные методы:

- `add(E e)`: добавляет элемент, если его нет в наборе.
- `remove(Object o)`: удаляет элемент.
- `contains(Object o)`: проверяет, содержится ли элемент.
- `size()`: возвращает количество элементов в наборе.
- `clear()`: удаляет все элементы из набора.