[[Кафка (Apache Kafka)||Kafka]] поддерживает три основных модели доставки [[Сообщение Кафка (Kafka Message)||сообщений]]:

- **At-most-once** (не более одного раза)
	- [[Сообщение Кафка (Kafka Message)||Сообщение]] может потеряться, но никогда не будет дублироваться.
	- Происходит, если [[Потребитель Кафка (Kafka Consumer)||потребитель]] обрабатывает [[Сообщение Кафка (Kafka Message)||сообщение]], но не успевает подтвердить (commit) [[Смещение Кафка (Kafka Offset)||смещение]].
	- Подходит для некритичных данных (например, [[Мониторинг (Monitoring)||мониторинг]] без строгих требований к полноте).
- **At-least-once** (как минимум один раз, но возможно дублирование)
	- [[Сообщение Кафка (Kafka Message)||Сообщение]] будет доставлено минимум один раз, но в случае сбоя может быть обработано повторно.
	- Достигается за счёт повторного чтения [[Сообщение Кафка (Kafka Message)||сообщений]], если [[Потребитель Кафка (Kafka Consumer)||потребитель]] не успел подтвердить обработку.
	- Это самая распространённая модель, так как она балансирует между надежностью и сложностью.
- **Exactly-once** (ровно один раз, без потерь и дубликатов)
	- Гарантирует, что каждое [[Сообщение Кафка (Kafka Message)||сообщение]] будет обработано строго один раз.
	- Требует [[Транзакция Кафка (Kafka Transaction)||транзакционной]] обработки и поддержки [[Идемпотентность (Idempotency)||idempotent]]-[[Производитель Кафка (Kafka Producer)||производителей]].
	- Используется в критических системах (например, финансовые [[Транзакция (Transaction)||транзакции]]).


### Как обеспечиваются гарантии доставки

- Репликация данных ([[ISR (In-Sync Replicas)||ISR — In-Sync Replicas]]) защищает от потерь при сбоях.
- [[Идемпотентность (Idempotency)||Idempotent]]-[[Производитель Кафка (Kafka Producer)||продюсеры]] предотвращают дублирование [[Сообщение Кафка (Kafka Message)||сообщений]].
- [[Транзакция Кафка (Kafka Transaction)||Транзакционные топики]] позволяют гарантировать **exactly-once** обработку.
- Коммиты [[Смещение Кафка (Kafka Offset)||смещений]] (offset commit) контролируют, какие [[Сообщение Кафка (Kafka Message)||сообщения]] уже обработаны.

