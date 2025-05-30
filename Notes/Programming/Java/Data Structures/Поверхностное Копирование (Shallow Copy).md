**Поверхностное копирование (Shallow Copy)** в Java означает создание копии объекта, при которой копируются только [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылки]] на объекты, находящиеся в полях оригинального объекта, а не сами объекты. Это означает, что если оригинальный объект содержит [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылки]] на другие объекты (например, [[Массив (Array)||массивы]] или другие объекты), то в копии будут только [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылки]] на эти объекты, а не их полные копии.

В результате, изменения в вложенных объектах ([[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылках]]) в копии будут отражаться и в оригинале, так как оба объекта будут указывать на те же самые вложенные объекты.

### Пример поверхностного копирования:

```java
import java.util.Arrays;

class ShallowCopyExample {
    public static void main(String[] args) {
        int[] original = {1, 2, 3};
        ShallowCopyExample obj = new ShallowCopyExample();
        obj.shallowCopy(original);
    }
	
    public void shallowCopy(int[] original) {
        int[] shallowCopy = original; // Это поверхностное копирование
        shallowCopy[0] = 99; // Изменяем элемент в копии
		
        // Оригинальный массив также изменяется, потому что обе переменные указывают на один и тот же массив
        System.out.println("Оригинальный массив: " + Arrays.toString(original)); // Выведет: [99, 2, 3]
        System.out.println("Копия массива: " + Arrays.toString(shallowCopy));    // Выведет: [99, 2, 3]
    }
}
```

Здесь `shallowCopy` — это поверхностная копия массива, и изменения в одном [[Массив (Array)||массиве]] повлияют на другой, потому что обе переменные [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||указывают]] на один и тот же [[Массив (Array)||массив]].

Если вам нужно создать [[Глубокое Копирование (Deep Copy)||глубокую копию]], при которой копируются не только [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылки]], но и все вложенные объекты, это потребует дополнительных усилий и обходных путей.