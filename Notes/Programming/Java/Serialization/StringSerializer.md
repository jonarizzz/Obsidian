**StringSerializer** обычно используется для [[Сериализация (Serialization)||сериализации]] строк в байтовый массив, особенно в контексте фреймворков работы с данными, например, [[Кафка (Apache Kafka)||Kafka]] или [[{TODO} Redis||Redis]].


### Основные моменты

- В [[Кафка (Apache Kafka)||Apache Kafka]] [[StringSerializer||StringSerializer]] (`org.apache.kafka.common.serialization.StringSerializer`) кодирует [[String||строку]] в [[Массив (Array)||массив]] [[byte||byte]] с использованием UTF-8.
- В [[Спринг Фреймворк (Spring Framework)||Spring]] [[{TODO} Redis||Redis]] `StringRedisSerializer` помогает преобразовывать [[String||строки]] в [[Массив (Array)||массивы]] [[byte||byte]] и обратно.
- Можно легко реализовать свой [[StringSerializer||StringSerializer]], если требуется кастомное поведение, например, с другим кодировщиком.


### Пример использования в [[Кафка (Apache Kafka)||Kafka]]:

```java
Properties props = new Properties();

props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
```

Это указывает [[Производитель Кафка (Kafka Producer)||продюсеру Kafka]] сериализовать [[Ключ Сообщения Кафка (Kafka Message Key)||ключи]] и значения как [[String||строки]].