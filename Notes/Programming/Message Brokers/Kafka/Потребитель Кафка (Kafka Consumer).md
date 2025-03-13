**Kafka Consumer (потребитель)** — это компонент в [[Кафка (Apache Kafka)||Apache Kafka]], который читает [[Сообщение Кафка (Kafka Message)||сообщения]] из одного или нескольких [[Топик Кафка (Kafka Topic)||топиков]]. Потребители могут работать индивидуально или в [[Группа Потербителей Кафка (Kafka Consumer Group)||группе (Consumer Group)]] для [[Балансировщик Нагрузки (Load Balancer)||балансировки нагрузки]].


### Принцип работы

1. Подключается к [[Брокер Кафка (Kafka Broker)||брокеру Kafka]].
2. Читает [[Сообщение Кафка (Kafka Message)||сообщения]] из указанного [[Топик Кафка (Kafka Topic)||топика]] (или нескольких).
3. Обрабатывает данные ([[Логирование (Logging)||логирует]], сохраняет в [[База данных (БД, Database, DB)||базу данных]] и т. д.).
4. Коммитит [[Смещение Кафка (Kafka Offset)||Offset]] (позицию последнего обработанного [[Сообщение Кафка (Kafka Message)||сообщения]]).


### Ключевые особенности

- Поддержка [[Группа Потербителей Кафка (Kafka Consumer Group)||групп потребителей (Consumer Group)]] — [[Сообщение Кафка (Kafka Message)||сообщения]] распределяются между [[Потребитель Кафка (Kafka Consumer)||потребителями]] в [[Группа Потербителей Кафка (Kafka Consumer Group)||группе]].
- Гарантия доставки — [[Сообщение Кафка (Kafka Message)||сообщения]] не теряются, если правильно управлять [[Смещение Кафка (Kafka Offset)||Offset]].
- Гибкость в обработке [[Сообщение Кафка (Kafka Message)||сообщений]] — можно читать сначала, с последнего [[Смещение Кафка (Kafka Offset)||офсета]] или вручную управлять позицией.
- Автоматическое или ручное управление [[Смещение Кафка (Kafka Offset)||Offset]] — [[{TODO} Consumer (интерфейс)||потребители]] могут сами решать, когда фиксировать обработанные [[Сообщение Кафка (Kafka Message)||сообщения]].


### Пример Kafka Consumer на Java:

```java
Properties props = new Properties();

props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");

props.put(ConsumerConfig.GROUP_ID_CONFIG, "my-group");

props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

consumer.subscribe(Collections.singletonList("my-topic"));

while (true) {

    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    
    for (ConsumerRecord<String, String> record : records) {
        System.out.println("Получено сообщение: " + record.value());
    }
    
    consumer.commitSync(); // Подтверждаем обработку сообщений
}
```