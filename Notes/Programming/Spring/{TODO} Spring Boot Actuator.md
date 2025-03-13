**Spring Boot Actuator** — это встроенный модуль [[Spring Boot||Spring Boot]], который предоставляет готовые инструменты для [[Мониторинг (Monitoring)||мониторинга]], аудита и управления приложением в продакшене.

### Основные возможности Actuator:

- **Готовые эндпоинты** для получения информации о приложении, таких как:
	- /actuator/health — состояние приложения (живо или нет).
	- /actuator/info — пользовательская информация (можно добавить данные о версии, среде и т. д.).
	- /actuator/metrics — метрики системы (CPU, память, HTTP-запросы и др.).
	- /actuator/env — переменные окружения.
	- /actuator/loggers — уровень логирования и его динамическое изменение.
	- /actuator/mappings — список всех контроллеров и их URL.
	- /actuator/beans — список всех бинов в Spring-контексте.
- **Гибкая настройка**: Можно включать и отключать нужные эндпоинты через application.properties или application.yml.
- **Интеграция с [[Мониторинг (Monitoring)||мониторингом]]**: Поддержка Prometheus, Micrometer, Zipkin и других инструментов для сбора метрик и трассировки запросов.
- **Безопасность**: Доступ к эндпоинтам можно ограничить с помощью Spring Security.


### Как подключить Actuator?

В pom.xml (если используешь [[{TODO} Maven||Maven]]) добавь зависимость:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Для Gradle:

```
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-actuator'
}
```

Настройка в application.yml:

```
management:
  endpoints:
    web:
      exposure:
        include: health, info, metrics  # Включаем доступные эндпоинты
  endpoint:
    health:
      show-details: always  # Показывать подробности о состоянии приложения
  info:
    app:
      name: "MyApp"
      version: "1.0.0"
```

После запуска приложения эндпоинты будут доступны по адресу:

http://localhost:8080/actuator/health, http://localhost:8080/actuator/info и т. д.

  
Пример использования:

• Проверить, что приложение работает:

```
curl http://localhost:8080/actuator/health
```

Ответ:

```
{ "status": "UP" }
```


• Посмотреть загруженность CPU, памяти, активные потоки:

```
curl http://localhost:8080/actuator/metrics
```