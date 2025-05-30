Read Uncommitted — это [[Уровни Изоляции Транзакций (Transaction Isolation Levels)||уровень изоляции транзакций]] в [[База данных (БД, Database, DB)||базе данных]], который позволяет транзакциям читать данные, которые еще не были зафиксированы (не коммитированы). Это означает, что транзакции могут читать “грязные” данные, которые могут быть изменены или отменены другими транзакциями до того, как они будут окончательно подтверждены.

### Преимущества:

- Производительность: Этот уровень изоляции минимизирует блокировки, что может повысить производительность, особенно в сценариях с высокими требованиями к скорости выполнения операций и когда точность данных не критична.
- Меньше задержек: Поскольку не происходит блокировки чтения, это снижает время ожидания для других транзакций, которые могут пытаться получить доступ к тем же данным.

### Недостатки:

- [[Грязное Чтение (Dirty Read)||Грязные чтения (dirty reads)]]: Основный риск заключается в том, что транзакции могут прочитать данные, которые были изменены другими транзакциями, но не зафиксированы. Эти данные могут быть позже отменены, что приводит к несоответствиям и ошибкам.
- Неконсистентные данные: Поскольку транзакции могут видеть промежуточные состояния данных, это может привести к логическим ошибкам и несоответствиям в обработке данных.

### Пример:

Предположим, одна транзакция обновляет сумму на счете, но еще не зафиксировала изменения. В это время другая транзакция может прочитать эту сумму и использовать старое значение, несмотря на то, что в первой транзакции оно еще не было подтверждено.

Этот уровень изоляции обычно используется, когда важно минимизировать блокировки и время ожидания, и когда небольшие проблемы с точностью данных можно игнорировать.