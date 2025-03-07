Контейнер Инверсии Управления (IoC Container) — это программный компонент, который управляет созданием [[Объект (Object)||объектов]], их зависимостями и их [[Жизненный Цикл Бина (Bean Life Cycle)||жизненным циклом]]. Он реализует принцип [[Инверсия Контроля (IoC, Inversion of Control)||инверсии управления (IoC, Inversion of Control)]], который означает, что контроль над созданием и внедрением зависимостей передаётся контейнеру, а не осуществляется вручную внутри [[Класс (Class)||классов]].

### Основные функции IoC-контейнера:

- **Создание объектов** – контейнер отвечает за создание экземпляров классов.
- **Управление зависимостями** – автоматически внедряет зависимости в объекты (Dependency Injection).
- **Контроль жизненного цикла объектов** – определяет, когда объекты создаются и уничтожаются.
- **Конфигурируемость** – поддерживает конфигурацию через аннотации, XML или код.


### Пример использования [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring IoC]] с аннотациями

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.stereotype.Component;

// Компонент, который нужно внедрить
@Component
class Engine {
    public void start() {
        System.out.println("Engine started!");
    }
}

// Основной класс с зависимостью
@Component
class Car {
    private final Engine engine;
	
    // Внедрение зависимости через конструктор
    public Car(Engine engine) {
        this.engine = engine;
    }
	
    public void drive() {
        engine.start();
        System.out.println("Car is moving...");
    }
}

// Конфигурация и запуск IoC-контейнера
public class IoCExample {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext("com.example"); // Сканируем пакет
        Car car = context.getBean(Car.class); // Получаем объект из контейнера
        car.drive();
    }
}
```

Здесь [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||контейнер Spring]] автоматически создаёт экземпляры `Engine` и `Car`, внедряет зависимость в `Car` и управляет их [[Жизненный Цикл Бина (Bean Life Cycle)||жизненным циклом]].


### Реализация собственного IoC-контейнера

Чтобы лучше понять принцип работы [[Инверсия Контроля (IoC, Inversion of Control)||IoC]], можно реализовать примитивный контейнер вручную.

```java
import java.lang.reflect.Constructor;
import java.util.HashMap;
import java.util.Map;

// Простой IoC-контейнер
class SimpleIoCContainer {
    private final Map<Class<?>, Object> instances = new HashMap<>();
	
    public <T> void register(Class<T> type) throws Exception {
        Constructor<T> constructor = type.getDeclaredConstructor();
        T instance = constructor.newInstance();
        instances.put(type, instance);
    }
	
    public <T> T resolve(Class<T> type) {
        return type.cast(instances.get(type));
    }
}

// Классы для теста контейнера
class Service {
    public void doSomething() {
        System.out.println("Service is working!");
    }
}

public class CustomIoCExample {
    public static void main(String[] args) throws Exception {
        SimpleIoCContainer container = new SimpleIoCContainer();
        container.register(Service.class); // Регистрируем класс
        Service service = container.resolve(Service.class); // Получаем экземпляр
        service.doSomething();
    }
}
```

Здесь `SimpleIoCContainer` создаёт объект и управляет его получением. Это базовая концепция [[Инверсия Контроля (IoC, Inversion of Control)||IoC]].


IoC-контейнеры, такие как [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring IoC]], позволяют писать более гибкий, тестируемый и поддерживаемый код, избавляя разработчиков от необходимости вручную управлять зависимостями.