**DHCP** — это сетевой протокол, который автоматически назначает устройствам [[IP Адрес (Internet Protocol Address, IP Address)||IP-адреса]] и другие параметры сети ([[Шлюз (Default Gateway)||шлюз]], [[DNS (Domain Name System)||DNS]], [[Маска Подсети (Subnet Mask)||маску подсети]]).


### Как работает

1. Устройство отправляет запрос DHCP Discover.
2. DHCP-сервер предлагает [[IP Адрес (Internet Protocol Address, IP Address)||IP-адрес]] (DHCP Offer).
3. Устройство принимает предложение (DHCP Request).
4. Сервер подтверждает назначение (DHCP Acknowledgment).


### Что выдает DHCP

- [[IP Адрес (Internet Protocol Address, IP Address)||IP-адрес]] устройства.
- [[Шлюз (Default Gateway)||Шлюз]] по умолчанию.
- [[DNS (Domain Name System)||DNS-серверы]].
- [[Маска Подсети (Subnet Mask)||Маску подсети]].
- Время аренды [[IP Адрес (Internet Protocol Address, IP Address)||IP]].


### Плюсы

- Автоматическое управление [[IP Адрес (Internet Protocol Address, IP Address)||IP-адресами]].
- Исключает конфликты [[IP Адрес (Internet Protocol Address, IP Address)||адресов]].
- Упрощает администрирование сети.


### Минусы

- Возможность атак (например, DHCP Spoofing).
- Зависимость от DHCP-сервера (если он недоступен, устройства не получают [[IP Адрес (Internet Protocol Address, IP Address)||IP]]).