**Apache Flink** – это фреймворк для обработки потоков данных в реальном времени (и пакетной обработки). Позволяет анализировать, фильтровать, агрегировать и обрабатывать данные с высокой пропускной способностью и низкой задержкой.


### Как работает

Flink использует DataStream API (для потоковой обработки) и DataSet API (для пакетной обработки).
- **JobManager** – координирует задачи.
- **TaskManager** – исполняет задачи.
- **State Backend** – сохраняет промежуточные состояния (RocksDB, HDFS, S3).


### Пример кода (подсчет слов в потоке)

```java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

DataStream<String> text = env.socketTextStream("localhost", 9999);

text.flatMap(new Tokenizer())
    .keyBy(value -> value.f0)
    .sum(1)
    .print();

env.execute("WordCount");
```

- Читает данные из [[Сокет (Socket)||сокета]]
- Токенизирует строки
- Группирует и суммирует повторяющиеся слова
- Выводит результат


### Когда использовать

- Сложные потоковые вычисления (например, машинное обучение, графовые алгоритмы)
- Обработка событий с низкой задержкой
- Гибридная обработка (батч + стрим)
- [[{TODO} SQL (Structured Query Language)||SQL-запросы]] к потокам (Flink SQL)