Spring Boot Auto Configuration — это мощная особенность [[Spring Boot||Spring Boot]], которая позволяет автоматически настраивать компоненты приложения на основе зависимостей, присутствующих в [[Classpath||classpath]], а также конфигурации, указанной в приложении.


### Основные аспекты Auto Configuration:

#### Автоматическая настройка на основе зависимостей:

Когда приложение запускается, Spring Boot анализирует [[Classpath||classpath]] и автоматически настраивает [[Бин (Spring Bean)||бины]], основываясь на том, что найдено.

#### Механизм работы:

[[Spring Boot||Spring Boot]] использует аннотацию [[{TODO} EnableAutoConfiguration (аннотация)||@EnableAutoConfiguration]] (или ее сокращенный вариант [[{TODO} SpringBootApplication (аннотация)||@SpringBootApplication]], который включает в себя [[{TODO} EnableAutoConfiguration (аннотация)||@EnableAutoConfiguration]]). Эта аннотация активирует автоматическую настройку, а [[Spring Boot||Spring Boot]] сам настраивает компоненты, если в проекте присутствуют необходимые [[{TODO} Библиотека (Library)||библиотеки]] и отсутствуют конфликты.

#### Пример использования:

Простой пример, где [[Spring Boot||Spring Boot]] автоматически настраивает `DataSource` для подключения к базе данных:

```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

Если в вашем проекте есть зависимость, например, `spring-boot-starter-data-jpa`, [[Spring Boot||Spring Boot]] настроит [[JPA (Java Persistence API)||JPA]] репозитории, EntityManagerFactory и DataSource для вас.

  

### Пользовательская настройка:

Если вам нужно изменить поведение автоматической настройки, вы можете использовать свойства в `application.properties` или `application.yml`. Например, чтобы изменить настройки соединения с [[База данных (БД, Database, DB)||базой данных]], вы можете указать следующее:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
```

  

### Как [[Spring Boot||Spring Boot]] выбирает конфигурацию:

Spring Boot использует класс [[Configuration (аннотация)||@Configuration]] с аннотацией [[{TODO} Conditional (аннотация)||@Conditional]], чтобы определить, когда применить конкретную настройку. Это означает, что настройка будет применяться только при определенных условиях, например, если в [[Classpath||classpath]] есть нужные зависимости.


### Отключение автоматической настройки:

Если вам не нужно автоматическое подключение какого-то компонента, можно отключить его с помощью свойства `spring.autoconfigure.exclude`. Например:

```properties
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

Это исключит автоматическую настройку для источника данных.

  

### Как создавать собственные настройки:

Вы можете создавать свои собственные автоконфигурации, пометив классы с аннотацией [[Configuration (аннотация)||@Configuration]] и применяя к ним аннотацию [[{TODO} ConditionalOnClass (аннотация)||@ConditionalOnClass]], [[{TODO} ConditionalOnProperty (аннотация)||@ConditionalOnProperty]] и другие условия, чтобы управлять, когда будет применяться конкретная конфигурация.

  

### Преимущества:

- **Минимизация конфигурации:** Вам не нужно вручную настраивать большинство компонентов — [[Spring Boot||Spring Boot]] позаботится о настройке всего необходимого.
- **Умная настройка:** Система автоматически решает, какие компоненты подключать, исходя из зависимостей и наличия нужных библиотек.
- **Гибкость:** При необходимости можно легко настроить или отключить автоматическую настройку.

