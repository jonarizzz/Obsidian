В Spring Bean — это [[Объект (Object)||объект]], который управляется [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||контейнером Spring IoC (Inversion of Control)]]. По сути, это компонент приложения, который [[Спринг Фреймворк (Spring Framework)||Spring]] создает, настраивает и управляет его [[Жизненный Цикл Бина (Bean Life Cycle)||жизненным циклом]]. Имеет [[Область Видимости Бина (Bean Scope, Скоуп)||область видимости (скоуп)]]

### Основные характеристики Spring Bean:

- **Создается [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||контейнером Spring]]** – [[Объект (Object)||объекты]] (бины) создаются и управляются в соответствии с конфигурацией (Java-код, XML или аннотации).
- **Имеет определенный [[Жизненный Цикл Бина (Bean Life Cycle)||жизненный цикл]]** – от создания до уничтожения, [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring]] управляет его состоянием.
- **По умолчанию является [[Область Видимости Бина (Bean Scope, Скоуп)||синглтоном]]** – один бин создается на весь [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||контейнер]] (но можно изменить это поведение (изменить [[Область Видимости Бина (Bean Scope, Скоуп)||скоуп]])).
- **Связывается с другими бинами ([[Внедрение Зависимостей (Dependency Injection)||Dependency Injection]])** – [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring]] внедряет зависимости автоматически.


### Как объявить Bean?

Есть несколько способов:

#### 1. Аннотация [[{TODO} Component (аннотация)||@Component]] (или ее производные)

[[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring]] автоматически создаст бин, если [[Класс (Class)||класс]] помечен аннотацией:

```java
@Component
public class MyBean {
    public void doSomething() {
        System.out.println("Hello from MyBean!");
    }
}
```

Дополнительно нужно включить [[{TODO} ComponentScan (аннотация)||сканирование компонентов]]:

```java
@Configuration
@ComponentScan("com.example")
public class AppConfig {
}
```


#### 2. Аннотация [[{TODO} Bean (аннотация)||@Bean]] в [[Configuration (аннотация)||конфигурационном классе]]

```java
@Configuration
public class AppConfig {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

#### 3. Определение в XML (старый способ)

```xml
<bean id="myBean" class="com.example.MyBean"/>
```