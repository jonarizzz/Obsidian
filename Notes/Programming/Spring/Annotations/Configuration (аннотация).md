В [[Спринг Фреймворк (Spring Framework)||Spring Framework]] аннотация `@Configuration` используется для указания, что [[Класс (Class)||класс]] является источником конфигурации для контекста приложения Spring. Это значит, что [[Класс (Class)||класс]] содержит один или несколько [[Бин (Spring Bean)||бинов]], которые могут быть использованы для настройки и создания [[Объект (Object)||объектов]] внутри [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring IoC контейнера]].

Вместо того, чтобы использовать XML-конфигурацию, с `@Configuration` можно создавать конфигурацию с помощью Java. Класс с аннотацией `@Configuration` часто включает методы, помеченные аннотацией [[{TODO} Bean (аннотация)||@Bean]], которые определяют [[Бин (Spring Bean)||бины]] для [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring контейнера]].


### Пример использования:

```java
@Configuration
public class AppConfig {
	
    @Bean
    public MyService myService() {
        return new MyService();
    }
	
    @Bean
    public MyRepository myRepository() {
        return new MyRepository();
    }
}
```

В этом примере `AppConfig` — это конфигурационный [[Класс (Class)||класс]], а методы `myService` и `myRepository` создают и возвращают [[Бин (Spring Bean)||бины]], которые могут быть [[Внедрение Зависимостей (Dependency Injection)||инжектированы]] в другие компоненты Spring.


Также стоит отметить, что аннотация `@Configuration` является специальной меткой для [[Класс (Class)||классов]], предназначенных для конфигурации, и она подразумевает поведение как для обычных [[Бин (Spring Bean)||бинов]] с [[{TODO} Component (аннотация)||@Component]], но также активирует возможность кэширования конфигурации, что улучшает производительность.