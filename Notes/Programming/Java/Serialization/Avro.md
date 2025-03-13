**AvroSerializer** используется для [[Сериализация (Serialization)||сериализации объектов]] в бинарный Avro-формат, часто применяемый в [[Кафка (Apache Kafka)||Kafka]] и больших данных.


### Основные моменты

- В [[Кафка (Apache Kafka)||Apache Kafka]] `KafkaAvroSerializer` (`io.confluent.kafka.serializers.KafkaAvroSerializer`) кодирует данные в Avro с использованием схемы из [[{TODO} Schema Registry||Schema Registry]].
- В Apache Avro можно использовать `SpecificDatumWriter` или `GenericDatumWriter` для сериализации вручную.
- Требуется Avro-схема (`.avsc`) для определения структуры данных.


### Пример использования в [[Кафка (Apache Kafka)||Kafka]]:

```java
Properties props = new Properties();

props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, KafkaAvroSerializer.class.getName());

props.put(AbstractKafkaSchemaSerDeConfig.SCHEMA_REGISTRY_URL_CONFIG, "http://localhost:8081");
```

Это указывает [[Производитель Кафка (Kafka Producer)||Kafka-продюсеру]] [[Сериализация (Serialization)||сериализовать объекты]] в [[Avro||Avro]] с использованием схемы из [[{TODO} Schema Registry||Schema Registry]].