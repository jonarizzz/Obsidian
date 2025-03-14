**SoftReference в Java** — это один из [[Типы Ссылок (Reference Types)||типов ссылок]] из пакета `java.lang.ref`, который используется для реализации [[{TODO} Кэширование в Java||кэширования]] и управления памятью. [[Объект (Object)||Объекты]], на которые ссылается SoftReference, удаляются только при нехватке памяти, но не сразу после потери [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||сильной ссылки]].

### Основные особенности:

- **“Мягкие” ссылки** – объект остается в памяти, пока у [[Виртуальная Машина Java (Java Virtual Machine, JVM)||JVM]] достаточно свободной памяти.
- **Удаляются перед выбрасыванием [[OutOfMemoryError||OutOfMemoryError]]**, но не сразу после потери всех [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||сильных ссылок]].
- **Используется в [[{TODO} Кэширование в Java||кэшах]]** – помогает [[{TODO} Кэширование в Java||кэшировать]] данные, которые не критичны, но могут быть полезны.

### Пример использования:

```java
import java.lang.ref.SoftReference;

public class SoftReferenceExample {
    public static void main(String[] args) {
        // Создаем объект и сильную ссылку
        String strongReference = new String("Hello, SoftReference!");
		
        // Создаем "мягкую" ссылку
        SoftReference<String> softRef = new SoftReference<>(strongReference);
		
        // Убираем сильную ссылку
        strongReference = null;
		
        // Объект все еще доступен через мягкую ссылку
        System.out.println("До GC: " + softRef.get());
		
        // Вызываем сборщик мусора (не гарантирует очистку)
        System.gc();
		
        // Проверяем, остался ли объект в памяти
        System.out.println("После GC: " + softRef.get());
    }
}
```

### Важные моменты:

- `softRef.get()` возвращает [[Объект (Object)||объект]], если он еще не удален.
- [[Сборщик Мусора (Garbage Collector, GC)||System.gc()]] не обязательно очищает `SoftReference` – это зависит от наличия свободной памяти.
- Если памяти мало, [[Сборщик Мусора (Garbage Collector, GC)||GC]] очистит мягкие ссылки, но перед этим попытается освободить обычные ([[Слабая Ссылка (WeakReference)||WeakReference]] удаляются сразу).

### Где используется?

- **[[{TODO} Кэширование в Java||Кэширование]] изображений, данных, результатов вычислений** (например, в [[{TODO} SoftReferenceMap||SoftReferenceMap]]).
- **JVM кэш для классов**.
- **Реализация кэшей в библиотеках (Google Guava Cache)**.