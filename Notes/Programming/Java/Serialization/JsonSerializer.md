**JsonSerializer** используется для [[Сериализация (Serialization)||сериализации объектов]] в [[{TODO} JSON||JSON]]-формат, особенно в библиотеках [[Кафка (Apache Kafka)||Kafka]], [[{TODO} Jackson||Jackson]] и [[Спринг Фреймворк (Spring Framework)||Spring]].


### Основные моменты

- В [[Кафка (Apache Kafka)||Apache Kafka]] `JsonSerializer` (`org.springframework.kafka.support.serializer.JsonSerializer`) превращает [[Объект (Object)||объекты]] в [[{TODO} JSON||JSON]] перед отправкой [[Сообщение Кафка (Kafka Message)||сообщений]].
- В [[{TODO} Jackson||Jackson]] `JsonSerializer<T>` (`com.fasterxml.jackson.databind.JsonSerializer<T>`) позволяет кастомизировать [[{TODO} JSON||JSON]]-[[Сериализация (Serialization)||сериализацию]] [[Объект (Object)||объектов]].
- В [[Спринг Фреймворк (Spring Framework)||Spring]] часто применяется с `KafkaTemplate` или [[{TODO} Redis||Redis]] для удобной работы с [[{TODO} JSON||JSON]]-данными.


### Пример использования в Kafka:

```java
Properties props = new Properties();

props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, JsonSerializer.class.getName());
```

Это указывает [[Производитель Кафка (Kafka Producer)||Kafka-продюсеру]] [[Сериализация (Serialization)||сериализовать]] [[Объект (Object)||объекты]] в [[{TODO} JSON||JSON]] перед отправкой.