**Kafka Broker** — это сервер в кластере [[Кафка (Apache Kafka)||Kafka]], который обрабатывает [[Сообщение Кафка (Kafka Message)||сообщения]], хранит [[Раздел Топика Кафка (Kafka Topic Partition)||партиции топиков]] и управляет [[Реплика Раздела Кафка (Kafka Partition Replica)||репликацией данных]].


### Основные функции

- Принимает и хранит [[Сообщение Кафка (Kafka Message)||сообщения]] от [[Производитель Кафка (Kafka Producer)||продюсеров]].
- Обслуживает запросы [[Потребитель Кафка (Kafka Consumer)||потребителей]], выдавая им данные.
- Распределяет [[Раздел Топика Кафка (Kafka Topic Partition)||партиции]] и управляет [[Реплика Раздела Кафка (Kafka Partition Replica)||репликами]] для [[Отказоустойчивость (Fault Tolerance)||отказоустойчивости]].
- Взаимодействует с [[Kafka Zookeeper||ZooKeeper]] для координации в кластере.


### Роль в надёжности и [[Масштабирование (Скейлинг, Scaling)||масштабируемости]]

- **Кластеризация** – несколько [[Брокер Кафка (Kafka Broker)||брокеров]] работают вместе, распределяя нагрузку.
- **[[Отказоустойчивость (Fault Tolerance)||Отказоустойчивость]]** – при сбое [[Брокер Кафка (Kafka Broker)||брокера]] его [[Раздел Топика Кафка (Kafka Topic Partition)||партиции]] восстанавливаются на других [[Брокер Кафка (Kafka Broker)||брокерах]].
- **[[Масштабирование (Скейлинг, Scaling)||Горизонтальное масштабирование]]** – можно добавлять новые [[Брокер Кафка (Kafka Broker)||брокеры]] для увеличения производительности.