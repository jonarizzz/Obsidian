ApplicationContext в Spring — это центральный интерфейс [[Контейнер Инверсии Контроля (Inversion of Control Container, IoC Container)||контейнера инверсии управления (IoC)]], который управляет [[Жизненный Цикл Бина (Bean Life Cycle)||жизненным циклом бинов]] и предоставляет расширенные возможности, такие как:

- Конфигурация [[Бин (Spring Bean)||бинов]] — создаёт и управляет зависимостями объектов ([[Бин (Spring Bean)||beans]]).
- Автоматическое связывание ([[Внедрение Зависимостей (Dependency Injection)||Dependency Injection, DI]]) — внедряет зависимости между [[Бин (Spring Bean)||бинами]].
- Механизм событий — позволяет [[Бин (Spring Bean)||бинам]] обмениваться сообщениями через [[{TODO} ApplicationEvent||ApplicationEvent]].
- Интернационализация (I18n) — поддержка локализации через MessageSource.
- Поддержка свойств (Environment & PropertySources) — позволяет загружать свойства из внешних файлов.


### Основные реализации ApplicationContext:

- `ClassPathXmlApplicationContext` — загружает конфигурацию из XML-файла в [[Classpath||classpath]].
- `FileSystemXmlApplicationContext` — загружает XML-конфигурацию из файловой системы.
- `AnnotationConfigApplicationContext` — используется для конфигурации через аннотации ([[Configuration (аннотация)||@Configuration]], [[{TODO} ComponentScan (аннотация)||@ComponentScan]]).
- `WebApplicationContext` — специализированный контекст для веб-приложений.


В приложении обычно используется **один контекст**, но в сложных веб-приложениях может быть **несколько** (корневой + для веб-слоя). В [[Spring Boot||Spring Boot]] создаётся `AnnotationConfigServletWebServerApplicationContext`.