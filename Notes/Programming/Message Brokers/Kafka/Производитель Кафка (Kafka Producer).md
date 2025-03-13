**Kafka Producer** — это клиент, который отправляет сообщения в [[Кафка (Apache Kafka)||Kafka]], публикуя их в определённые [[Топик Кафка (Kafka Topic)||топики]].


### Как работает

- Определяет [[Топик Кафка (Kafka Topic)||топик]] и [[Раздел Топика Кафка (Kafka Topic Partition)||партицию]], куда будет отправлено [[Сообщение Кафка (Kafka Message)||сообщение]].
- Формирует [[Сообщение Кафка (Kafka Message)||сообщение]], включая [[Ключ Сообщения Кафка (Kafka Message Key)||ключ (key)]], значение (value) и метаданные.
- Выбирает [[Раздел Топика Кафка (Kafka Topic Partition)||партицию]] (по [[Ключ Сообщения Кафка (Kafka Message Key)||ключу]] или случайно, если [[Ключ Сообщения Кафка (Kafka Message Key)||ключ]] отсутствует).
- Отправляет [[Сообщение Кафка (Kafka Message)||сообщение]] [[Брокер Кафка (Kafka Broker)||брокеру]], который сохраняет его и [[Реплика Раздела Кафка (Kafka Partition Replica)||реплицирует]].


### Основные конфигурации в [[{TODO} Java||Java]]:

- Настройки доставки [[Сообщение Кафка (Kafka Message)||сообщений]]:
	- `acks=0/1/all` — уровень подтверждений (`0` — не ждать, `1` — от лидера, `all` — от всех [[ISR (In-Sync Replicas)||реплик]]).
	- `retries` — количество попыток повторной отправки при сбоях.
	- `linger.ms` — задержка перед отправкой (для объединения [[Сообщение Кафка (Kafka Message)||сообщений]] в батчи).
	- `batch.size` — размер батча [[Сообщение Кафка (Kafka Message)||сообщений]].
- Надёжность и порядок:
	- `enable.idempotence=true` — предотвращение дубликатов ([[Типы доставки в Кафка (Kafka Delivery Types)||exactly-once]]).
	- `max.in.flight.requests.per.connection` — ограничение параллельных отправок (ставим `1` для строгого порядка).
- Производительность:
	- `compression.type=none/gzip/snappy/lz4/zstd` — сжатие [[Сообщение Кафка (Kafka Message)||сообщений]].
	- `buffer.memory` — размер буфера [[Сообщение Кафка (Kafka Message)||сообщений]] в [[Производитель Кафка (Kafka Producer)||продюсере]].
- Распределение [[Сообщение Кафка (Kafka Message)||сообщений]]:
	- `key.serializer / value.serializer` — [[Сериализация (Serialization)||сериализаторы]] для [[Ключ Сообщения Кафка (Kafka Message Key)||ключей]] и значений [[Сообщение Кафка (Kafka Message)||сообщений]].
	- `partitioner.class` — кастомная логика распределения по [[Раздел Топика Кафка (Kafka Topic Partition)||разделам]].


### Пример на [[{TODO} Java||Java]]

```java
import org.apache.kafka.clients.producer.*;
import java.util.Properties;

public class SimpleKafkaProducer {
    public static void main(String[] args) {
        // Настройки продюсера
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092"); // Адрес брокера Kafka
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("acks", "all"); // Гарантия доставки
		
        // Создаём продюсер
        KafkaProducer<String, String> producer = new KafkaProducer<>(props);
		
        // Отправляем сообщение в топик "test-topic"
        String topic = "test-topic";
        ProducerRecord<String, String> record = new ProducerRecord<>(topic, "key1", "Hello, Kafka!");
		
        // Асинхронная отправка с обработкой результата
        producer.send(record, (metadata, exception) -> {
            if (exception == null) {
                System.out.println("Сообщение отправлено в " 
	                + metadata.topic() + " (partition: " 
	                + metadata.partition() + ", offset: " 
	                + metadata.offset() + ")");
            } else {
                exception.printStackTrace();
            }
        });
		
        // Закрываем продюсер
        producer.close();
    }
}
```