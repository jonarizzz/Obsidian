В [[Spring Boot||Spring Boot]] профили (**Profiles**) используются для управления конфигурацией приложения в разных средах (например, локальная разработка, тестирование, продакшен). С помощью профилей можно загружать разные настройки в зависимости от окружения, без необходимости менять код.


### Как работают профили?

Spring Boot позволяет задавать **активный профиль** через:

1. **Переменные окружения**

```bash
export SPRING_PROFILES_ACTIVE=prod
```

2. **Флаг при запуске приложения**

```bash
java -jar myapp.jar --spring.profiles.active=dev
```

1. **Настройки в `application.properties` или `application.yml`**

```properties
spring.profiles.active=dev
```

  

### Конфигурация профилей

Можно создать отдельные файлы конфигурации для разных профилей:

- `application-dev.properties` (для разработки)
- `application-prod.properties` (для продакшена)

Пример `application-dev.properties`:
```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost/devdb
```

Пример `application-prod.properties`:
```properties
server.port=80
spring.datasource.url=jdbc:mysql://prodserver/proddb
```


### Использование в коде

1. **Аннотация [[{TODO} Profile (аннотация)||@Profile]]**

Можно помечать [[Бин (Spring Bean)||бины]], которые должны загружаться только при активном профиле:

```java
@Service
@Profile("dev")
public class DevService implements MyService {
    // код, который будет работать только в профиле "dev"
}
```

2. **Условная загрузка в конфигурации**

```java
@Configuration
public class AppConfig {
    @Bean
    @Profile("prod")
    public DataSource prodDataSource() {
        return new HikariDataSource(); // Продакшен база
    }
	
    @Bean
    @Profile("dev")
    public DataSource devDataSource() {
        return new H2DataSource(); // Локальная база H2
    }
}
```

  
### Множественные профили

Можно активировать несколько профилей через запятую:

```properties
spring.profiles.active=dev,database
```