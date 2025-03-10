**Итератор (Iterator)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который предоставляет способ последовательного доступа ко всем элементам [[Collection (интерфейс)||коллекции]] без раскрытия её структуры.


### Пример

```java
import java.util.*;

class IteratorPattern {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("A", "B", "C");
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) System.out.println(iterator.next());
    }
}
```