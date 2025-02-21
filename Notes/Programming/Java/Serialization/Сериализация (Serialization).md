**Сериализация** в Java — это процесс преобразования [[Объект (Object)||объекта]] в поток байтов для его последующего сохранения в [[{TODO} Файл (File)||файл]], передачи по сети или хранения в памяти. Обратный процесс называется **десериализацией** — восстановлением объекта из потока байтов.

### Как работает сериализация?

1. [[Объект (Object)||Объект]] преобразуется в поток байтов.
2. Этот поток может быть записан в [[{TODO} Файл (File)||файл]], отправлен по сети или сохранен в памяти.
3. Позже этот поток байтов можно прочитать и воссоздать оригинальный [[Объект (Object)||объект]].

  
### Как сериализовать объект?

Чтобы объект можно было сериализовать, его класс должен реализовывать [[{TODO} Serializable (интерфейс)||интерфейс java.io.Serializable]]. Этот [[Интерфейс (Interface)||интерфейс]] не содержит методов, он просто помечает класс как поддерживающий сериализацию.

### Пример:

```java
import java.io.*;

class Person implements Serializable {  // Класс должен реализовать Serializable
    private static final long serialVersionUID = 1L; // Рекомендуется добавлять serialVersionUID
    String name;
    int age;
	
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        Person person = new Person("Alice", 30);
		
        // Сериализация
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            out.writeObject(person);
            System.out.println("Объект сериализован");
        } catch (IOException e) {
            e.printStackTrace();
        }
		
        // Десериализация
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person deserializedPerson = (Person) in.readObject();
            System.out.println("Объект десериализован: " + deserializedPerson.name + ", " + deserializedPerson.age);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```


### Важные моменты:

- Поля [[transient||transient]] не сериализуются.
- [[static||static]] поля не сериализуются, так как они принадлежат [[Класс (Class)||классу]], а не [[Объект (Object)||объекту]].
- `serialVersionUID` используется для контроля совместимости версий класса.

  
### Где используется?

- Передача [[Объект (Object)||объектов]] по сети (например, RMI).
- Сохранение состояния объектов в [[{TODO} Файл (File)||файлах]] или [[База данных (Database)||базах данных]].
- [[{TODO} Кэширование в Java||Кэширование объектов]].

  

В современных приложениях вместо стандартной сериализации часто используют **JSON** (например, через Jackson) или **protobuf** (Google Protocol Buffers), так как они более эффективны и безопасны.