В Java ключевое слово `transient` используется для указания, что поле [[Класс (Class)||класса]] не должно [[Сериализация (Serialization)||сериализоваться]] при передаче [[Объект (Object)||объекта]] через [[{TODO} Stream (интерфейс)||потоки]] (например, при использовании `ObjectOutputStream`).

### Пример:

```java
import java.io.*;

class User implements Serializable {
    private static final long serialVersionUID = 1L;
    
    String username;
    transient String password; // не будет сохранено в файле
	
    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }
}

public class TransientExample {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        User user = new User("JohnDoe", "secret123");
		
        // Сериализация объекта
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("user.ser"))) {
            oos.writeObject(user);
        }
		
        // Десериализация объекта
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("user.ser"))) {
            User deserializedUser = (User) ois.readObject();
            System.out.println("Username: " + deserializedUser.username);
            System.out.println("Password: " + deserializedUser.password); // null, так как поле transient
        }
    }
}
```


### Когда использовать?

- Для полей, которые не должны сохраняться (например, пароли, временные данные, кеши).
- Для объектов, которые не реализуют [[{TODO} Serializable (интерфейс)||Serializable]].
- Для полей, которые можно вычислить заново после десериализации.

Если нужно управлять [[Сериализация (Serialization)||сериализацией]] вручную (например, задать значение `transient`-полям после загрузки), можно использовать методы `writeObject` и `readObject`:

```java
private void writeObject(ObjectOutputStream oos) throws IOException {
    oos.defaultWriteObject();
    oos.writeObject(encrypt(password)); // Например, шифруем перед сохранением
}

private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
    ois.defaultReadObject();
    this.password = decrypt((String) ois.readObject()); // Расшифровываем после загрузки
}
```

Таким образом, `transient` позволяет исключать ненужные или чувствительные данные из процесса [[Сериализация (Serialization)||сериализации]].