
**Spring Security** — это мощный и гибкий фреймворк [[Аутентификация (Authentication)||аутентификации]] и [[Авторизация (Authorization)||авторизации]] для приложений на основе [[Спринг Фреймворк (Spring Framework)||Spring]]. Он обеспечивает защиту [[{TODO} Веб Приложение (Web Application)||веб-приложений]] и [[REST (Representational State Transfer)||REST API]], поддерживает различные механизмы [[Аутентификация (Authentication)||аутентификации]], а также интеграцию с различными системами безопасности.

### Основные возможности Spring Security:

- [[Аутентификация (Authentication)||Аутентификация (Authentication)]]
	- Проверка личности пользователя (логин/пароль, [[OAuth 2.0||OAuth2]], [[{TODO} JWT||JWT]], [[{TODO} SAML (Security Assertion Markup Language)||SAML]] и др.)
	- Поддержка встроенных и кастомных провайдеров аутентификации (например, [[База данных (БД, Database, DB)||база данных]], [[{TODO} LDAP||LDAP]])
	- Запоминание пользователя (Remember Me)
- [[Авторизация (Authorization)||Авторизация (Authorization)]]
	- Контроль доступа к ресурсам (на уровне [[URL (Uniform Resource Locator)||URL]], методов контроллеров, бизнес-логики)
	- Гибкое разграничение прав (роль ROLE_ADMIN, ROLE_USER и т. д.)
	- Матричные политики доступа (Spring Security Expressions)
- Защита от атак
	- [[{TODO} CSRF (межсайтовая подделка запроса)||CSRF (межсайтовая подделка запроса)]]
	- [[{TODO} XSS (межсайтовый скриптинг)||XSS (межсайтовый скриптинг)]]
	- [[{TODO} Clickjacking (атаки с подменой интерфейса)||Clickjacking (атаки с подменой интерфейса)]]
	- Защита от атак повторного использования токенов
- Интеграция с протоколами безопасности
	- [[OAuth 2.0||OAuth 2.0]] и [[{TODO} OpenID Connect (OIDC)||OpenID Connect (OIDC)]]
	- [[{TODO} JWT||JWT (JSON Web Token)]]
	- [[{TODO} SAML (Security Assertion Markup Language)||SAML (Security Assertion Markup Language)]]
	- [[{TODO} Kerberos||Kerberos]], [[{TODO} LDAP||LDAP]]
- Гибкая настройка и расширяемость
	- Настройка безопасности с помощью Java-конфигурации или XML
	- Возможность кастомизации [[Аутентификация (Authentication)||аутентификации]], [[Авторизация (Authorization)||авторизации]] и политики безопасности
	- Интеграция с [[Spring Boot||Spring Boot]] ([[Автоконфигурация (Spring Boot Auto Configuration)||автоконфигурация]])


### Пример базовой конфигурации:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .requestMatchers("/user/**").hasRole("USER")
                .anyRequest().authenticated()
            )
            .formLogin(withDefaults())  // Форма входа
            .logout(withDefaults());    // Выход из системы
        return http.build();
    }
}
```

Этот код:
- Запрещает доступ к /admin/**, если у пользователя нет роли ADMIN
- Разрешает доступ к /user/** только пользователям с ролью USER
- Включает стандартную форму аутентификации
- Добавляет выход из системы