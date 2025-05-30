**SOA (Service-Oriented Architecture)** – это архитектурный подход, при котором приложение строится из крупных сервисов, каждый из которых отвечает за определённую бизнес-функцию. Эти сервисы могут работать независимо и взаимодействовать через общий коммуникационный слой (обычно [[Enterprise Service Bus (ESB)||ESB – Enterprise Service Bus]] или [[API (Application Programming Interface)||API]]).


### Как устроено

Система состоит из нескольких крупных сервисов, которые могут быть разделены по бизнес-логике. Каждый сервис может иметь свою [[База данных (БД, Database, DB)||базу данных]], но чаще они работают с общей [[База данных (БД, Database, DB)||БД]].

Обычно SOA включает:

- **Клиенты** – [[Веб Приложение (Web Application)||веб-приложения]], мобильные приложения, другие системы.
- **Сервисы** – модули, выполняющие бизнес-логику (например, управление заказами, платежи, учет пользователей).
- **[[Enterprise Service Bus (ESB)||ESB (Enterprise Service Bus)]]** – центральный “шлюз” для общения между сервисами.
- **[[База данных (БД, Database, DB)||База данных]]** – может быть общей или раздельной для каждого сервиса.


### Плюсы

- **Повторное использование сервисов** – можно использовать один сервис в разных проектах.
- **Гибкость** – можно заменять или обновлять сервисы без переделки всей системы.
- **Разные технологии** – каждый сервис может быть написан на разном языке программирования.
- **Лучшая масштабируемость, чем у монолита** – можно масштабировать отдельные сервисы.


### Минусы

- **Сложность управления** – нужно продумывать взаимодействие сервисов и управлять их зависимостями.
- **Более низкая производительность** – сервисы взаимодействуют через сеть, что медленнее, чем внутри [[Монолит (Monolith)||монолита]].
- **ESB – точка отказа** – если центральный “шлюз” ([[Enterprise Service Bus (ESB)||ESB]]) перегружен или сломается, вся система может перестать работать.
- **Высокие требования к безопасности** – нужно защищать [[API (Application Programming Interface)||API]] и данные при передаче между сервисами.


### Когда выбирать SOA?

- Если у вас большая компания с разными бизнес-направлениями.
- Если нужно интегрировать старые системы с новыми.
- Если важно повторное использование сервисов в разных продуктах.
- Если бизнес-логика достаточно стабильная и изменения происходят нечасто.


### Когда SOA – плохой выбор?

- Если проект небольшой – сложность SOA будет избыточной.
- Если нет ресурсов для управления инфраструктурой и [[Enterprise Service Bus (ESB)||ESB]].
- Если критична высокая скорость работы – взаимодействие через сеть будет медленнее [[Монолит (Monolith)||монолита]].