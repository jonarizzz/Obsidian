Жизненный цикл [[Бин (Spring Bean)||бина]] в [[Спринг Фреймворк (Spring Framework)||Spring Framework]] — это процесс, через который проходит [[Бин (Spring Bean)||объект-Bean]] от момента создания до уничтожения. Он включает в себя несколько этапов, и Spring предоставляет механизмы для управления этим процессом.

### Основные этапы:

1. Создание объекта – [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||Spring]] создаёт экземпляр [[Бин (Spring Bean)||бина]] (если используется [[Область Видимости Бина (Bean Scope, Скоуп)||Singleton]], то он создаётся сразу при запуске [[Контекст Приложения (Application Context)||контекста]]).
2. Заполнение зависимостей – [[Контейнер Инверсии Контроля в Спринг (Spring IoC Container)||контейнер]] [[Внедрение Зависимостей (Dependency Injection)||внедряет зависимости]] (через **конструктор** или **сеттеры**).
3. Вызов [[{TODO} PostConstruct (аннотация)||@PostConstruct]] или `InitializingBean -> afterPropertiesSet()`
	1. Если [[Бин (Spring Bean)||бин]] реализует [[{TODO} InitializingBean||InitializingBean]], то вызывается метод `afterPropertiesSet()`.
	2. Или если используется аннотация [[{TODO} PostConstruct (аннотация)||@PostConstruct]], вызывается помеченный метод.
4. Вызов метода `init` (если указан в `initMethod` в конфигурации): если в XML-конфигурации или в `@Bean(initMethod = "customInit")` указан метод инициализации, он вызывается.
5. Готовность к использованию – на этом этапе [[Бин (Spring Bean)||бин]] полностью готов к работе.
6. Завершение работы приложения – когда [[Контекст Приложения (Application Context)||контекст Spring]] закрывается, вызываются методы для завершения работы [[Бин (Spring Bean)||бина]].
7. Вызов [[{TODO} PreDestroy (аннотация)||@PreDestroy]] или `DisposableBean -> destroy()`
	1. Если используется [[{TODO} PreDestroy (аннотация)||@PreDestroy]], вызывается этот метод.
	2. Если [[Бин (Spring Bean)||бин]] реализует [[{TODO} DisposableBean||DisposableBean]], вызывается метод `destroy()`.
8. Вызов метода destroy (если указан в `destroyMethod`): если в конфигурации задан `destroyMethod`, вызывается этот метод.


### Как управлять жизненным циклом?


✅ Использование аннотаций:

```java
@Component
public class MyBean {
    
    @PostConstruct
    public void init() {
        System.out.println("Бин инициализирован!");
    }
	
    @PreDestroy
    public void destroy() {
        System.out.println("Бин будет уничтожен!");
    }
}
```

✅ Использование интерфейсов InitializingBean и DisposableBean:

```java
@Component
public class MyBean implements InitializingBean, DisposableBean {
    
    @Override
    public void afterPropertiesSet() {
        System.out.println("Метод afterPropertiesSet() вызван!");
    }
	
    @Override
    public void destroy() {
        System.out.println("Метод destroy() вызван!");
    }
}
```

✅ Указание initMethod и destroyMethod:

```java
@Bean(initMethod = "customInit", destroyMethod = "customDestroy")
public MyBean myBean() {
    return new MyBean();
}
```

```java
public class MyBean {
    public void customInit() {
        System.out.println("Инициализация через initMethod!");
    }
	
    public void customDestroy() {
        System.out.println("Уничтожение через destroyMethod!");
    }
}
```
