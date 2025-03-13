**Kafka Consumer Group** — это группа [[Потребитель Кафка (Kafka Consumer)||потребителей]], работающих вместе для чтения [[Сообщение Кафка (Kafka Message)||сообщений]] из одного или нескольких [[Топик Кафка (Kafka Topic)||топиков]] параллельно.


### Принцип работы

- Каждый [[Потребитель Кафка (Kafka Consumer)||потребитель]] в группе получает часть [[Раздел Топика Кафка (Kafka Topic Partition)||партиций]] из [[Топик Кафка (Kafka Topic)||топика]].
- [[Кафка (Apache Kafka)||Kafka]] гарантирует, что каждую [[Раздел Топика Кафка (Kafka Topic Partition)||партицию]] читает только один [[Потребитель Кафка (Kafka Consumer)||потребитель]] в группе.
- Если один [[Потребитель Кафка (Kafka Consumer)||потребитель]] выходит из строя, его [[Раздел Топика Кафка (Kafka Topic Partition)||партиции]] перераспределяются между оставшимися [[Потребитель Кафка (Kafka Consumer)||потребителями]].


### Для чего используются

- [[Масштабирование (Скейлинг, Scaling)||Горизонтальное масштабирование]] – позволяет обрабатывать больше [[Сообщение Кафка (Kafka Message)||сообщений]] быстрее.
- [[Балансировщик Нагрузки (Load Balancer)||Балансировка нагрузки]] – [[Сообщение Кафка (Kafka Message)||сообщения]] распределяются между [[Потребитель Кафка (Kafka Consumer)||потребителями]].
- [[Отказоустойчивость (Fault Tolerance)||Отказоустойчивость]] – при сбое одного [[Потребитель Кафка (Kafka Consumer)||потребителя]] его нагрузку берут другие.


### Как работает [[Балансировщик Нагрузки (Load Balancer)||балансировка]] в Consumer Group

- Если `количество потребителей ≤ количество партиций`: каждый [[Потребитель Кафка (Kafka Consumer)||потребитель]] читает минимум одну [[Раздел Топика Кафка (Kafka Topic Partition)||партицию]].
- Если `количество потребителей > количество партиций`: некоторые [[Потребитель Кафка (Kafka Consumer)||потребители]] остаются без нагрузки.


### Пример Kafka Consumer Group в [[{TODO} Java||Java]]

```java
Properties props = new Properties();

props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");

props.put(ConsumerConfig.GROUP_ID_CONFIG, "my-consumer-group"); // Одна группа для нескольких потребителей

props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

consumer.subscribe(Collections.singletonList("my-topic")); // Подписка на топик

while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    
    for (ConsumerRecord<String, String> record : records) {
        System.out.println("Consumer " + record.value());
    }
    
    consumer.commitSync(); // Фиксируем офсеты
}
```