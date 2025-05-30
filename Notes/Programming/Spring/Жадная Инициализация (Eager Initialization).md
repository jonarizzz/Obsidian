Жадная инициализация (Eager Initialization) в [[Спринг Фреймворк (Spring Framework)||Spring]] — это стратегия, при которой [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring-контейнер]] создаёт и инициализирует [[Бин (Spring Bean)||бины]] сразу после старта приложения, а не откладывает их создание до момента первого использования (в отличие от [[Ленивая Инициализация (Lazy Initialization)||ленивой инициализации, Lazy Initialization]]).

### Как работает жадная инициализация?**

- По умолчанию все [[{TODO} Singleton (область видимости)||singleton-бины]] в Spring создаются при старте контейнера.
- Это позволяет выявить возможные ошибки при запуске приложения, так как все зависимости и конфигурации проверяются заранее.
- Используется в большинстве случаев, когда приложение требует готовности всех сервисов сразу после загрузки.

### Как настроить жадную инициализацию?

Жадная инициализация включена по умолчанию для [[Бин (Spring Bean)||бинов]] со [[{TODO} Singleton (область видимости)||scope = “singleton”]], но если явно включена [[Ленивая Инициализация (Lazy Initialization)||ленивая инициализация]] на уровне всего контекста (`spring.main.lazy-initialization=true`), то можно переопределить её для конкретного [[Бин (Spring Bean)||бина]].


### Пример явного указания жадной инициализации:

```java
import org.springframework.stereotype.Service;

@Service
public class MyEagerService {
    public MyEagerService() {
        System.out.println("MyEagerService создан!");
    }
}
```

Этот [[Бин (Spring Bean)||бин]] создаётся сразу после запуска приложения, так как [[{TODO} Service (аннотация)||@Service]] по умолчанию использует [[{TODO} Singleton (область видимости)||singleton-область видимости]].


### Как переопределить поведение?

Если приложение настроено на [[Ленивая Инициализация (Lazy Initialization)||ленивую инициализацию]] ([[{TODO} Lazy (аннотация)||@Lazy]] на уровне конфигурации или в аннотациях), можно отменить её для конкретного [[Бин (Spring Bean)||бина]]:

```java
import org.springframework.context.annotation.Lazy;
import org.springframework.stereotype.Service;

@Service
@Lazy(false)  // Гарантирует жадную инициализацию
public class MyEagerService {
    public MyEagerService() {
        System.out.println("MyEagerService создан!");
    }
}
```

### Когда использовать?

- Когда нужно, чтобы [[Бин (Spring Bean)||бины]] были готовы сразу после старта (например, подключение к [[База данных (БД, Database, DB)||БД]], загрузка [[Кэш (Cache)||кэша]]).
- Для проверки конфигурации и зависимостей на этапе запуска (быстрая проверка ошибок).

Не рекомендуется для тяжеловесных [[Бин (Spring Bean)||бинов]], которые могут замедлить запуск приложения.