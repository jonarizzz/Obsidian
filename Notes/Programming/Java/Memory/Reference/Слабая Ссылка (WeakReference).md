
`WeakReference<T>` — это специальный [[Класс (Class)||класс]] из пакета `java.lang.ref`, который позволяет удерживать [[Объект (Object)||объект]] слабо, то есть не препятствует его [[Сборщик Мусора (Garbage Collector)||сборке мусора (GC)]].

### Как работает?

- Если на объект больше нет [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||сильных ссылок]], но есть слабая ссылка (`WeakReference`), [[Сборщик Мусора (Garbage Collector)||сборщик мусора]] может его удалить при следующем проходе.
- `WeakReference` полезен для [[{TODO} Кэширование в Java||кэширования]] [[Объект (Object)||объектов]], которые можно безопасно пересоздать.

### Пример использования

```java
import java.lang.ref.WeakReference;

public class WeakReferenceExample {
    public static void main(String[] args) {
        Object strongObj = new Object();  // Сильная ссылка
        WeakReference<Object> weakRef = new WeakReference<>(strongObj);
		
        System.out.println("Before GC: " + weakRef.get()); // Доступен
		
        strongObj = null;  // Убираем сильную ссылку
        System.gc();        // Запрашиваем GC
		
        System.out.println("After GC: " + weakRef.get()); // Скорее всего, null
    }
}
```

`weakRef.get()` возвращает `null`, если объект был удален [[Сборщик Мусора (Garbage Collector)||сборщиком мусора]].


### Когда использовать?

- **Кэширование**: если объект можно заново создать или загрузить.
- **Хранение [[Listeners||слушателей]]/[[Паттерн Наблюдатель (Observer)||наблюдателей]]**: чтобы избежать утечек памяти.
- **Слабые ключи в [[{TODO} WeakHashMap||WeakHashMap]]**: автоматически удаляет [[Объект (Object)||объекты]] при [[Сборщик Мусора (Garbage Collector)||сборке мусора]].
