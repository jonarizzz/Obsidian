Внедрение зависимостей (Dependency Injection, DI) — это принцип проектирования программного обеспечения, который помогает уменьшить связанность между компонентами системы. Вместо того чтобы создавать [[Объект (Object)||объекты]] внутри [[Класс (Class)||класса]] или компонента, зависимости ([[Объект (Object)||объекты]], от которых зависит [[Класс (Class)||класс]]) передаются ему извне. Это способствует улучшению тестируемости, гибкости и расширяемости системы.

### Преимущества внедрения зависимостей:

- **Уменьшение связанности**: классы становятся независимыми от реализации своих зависимостей.
- **Упрощение тестирования**: проще подменить зависимости на мок-объекты при тестировании.
- **Упрощение модификации**: легко заменить одну зависимость на другую без изменения логики класса.

  
### Примеры:

#### Пример 1: Внедрение  через конструктор

```java
// Интерфейс репозитория
public interface UserRepository {
    User findById(int id);
}

// Реализация репозитория
public class UserRepositoryImpl implements UserRepository {
    @Override
    public User findById(int id) {
        // Реализация поиска пользователя по id
        return new User(id, "John Doe");
    }
}

// Сервис, который зависит от UserRepository
public class UserService {
    private UserRepository userRepository;
	
    // Внедрение зависимости через конструктор
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
	
    public User getUser(int id) {
        return userRepository.findById(id);
    }
}

// Главный класс для демонстрации
public class Main {
    public static void main(String[] args) {
        // Создаем зависимость
        UserRepository userRepository = new UserRepositoryImpl();
        
        // Внедряем зависимость в UserService через конструктор
        UserService userService = new UserService(userRepository);
        
        // Используем сервис
        User user = userService.getUser(1);
        System.out.println(user.getName());
    }
}
```

#### Пример 2: Внедрение зависимостей через сеттеры

```java
// Интерфейс репозитория
public interface UserRepository {
    User findById(int id);
}

// Реализация репозитория
public class UserRepositoryImpl implements UserRepository {
    @Override
    public User findById(int id) {
        // Реализация поиска пользователя по id
        return new User(id, "John Doe");
    }
}

// Сервис, который зависит от UserRepository
public class UserService {
    private UserRepository userRepository;
	
    // Внедрение зависимости через сеттер
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
	
    public User getUser(int id) {
        return userRepository.findById(id);
    }
}

// Главный класс для демонстрации
public class Main {
    public static void main(String[] args) {
        // Создаем зависимость
        UserRepository userRepository = new UserRepositoryImpl();
        
        // Создаем сервис
        UserService userService = new UserService();
        
        // Внедряем зависимость через сеттер
        userService.setUserRepository(userRepository);
        
        // Используем сервис
        User user = userService.getUser(1);
        System.out.println(user.getName());
    }
}
```

#### Пример 3: Внедрение зависимостей с использованием [[Спринг Фреймворк (Spring Framework)||Spring]] (с фреймворком)

Если используется Spring Framework, внедрение зависимостей может быть автоматизировано с помощью аннотаций:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

public interface UserRepository {
    User findById(int id);
}

@Component
public class UserRepositoryImpl implements UserRepository {
    @Override
    public User findById(int id) {
        return new User(id, "John Doe");
    }
}

@Component
public class UserService {
    private UserRepository userRepository;
	
    // Внедрение зависимости через аннотацию @Autowired
    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
	
    public User getUser(int id) {
        return userRepository.findById(id);
    }
}

// Главный класс с использованием Spring
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        // Создание контекста Spring
        ApplicationContext context = new AnnotationConfigApplicationContext("com.example");
        
        // Получаем UserService из контекста
        UserService userService = context.getBean(UserService.class);
        
        // Используем сервис
        User user = userService.getUser(1);
        System.out.println(user.getName());
    }
}
```

В этом примере Spring автоматически внедряет зависимости с использованием аннотации [[{TODO} Autowired (аннотация)||@Autowired]], и компоненты помечены как [[{TODO} Component (аннотация)||@Component]] для управления зависимостями в [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||контейнере Spring]].