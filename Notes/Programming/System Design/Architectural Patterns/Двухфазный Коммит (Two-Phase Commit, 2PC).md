**2PC (Two-Phase Commit)** — это протокол [[Распределённая Транзакция (Distributed Transaction)||распределённых транзакций]], который гарантирует, что все участники либо зафиксируют изменения, либо откатят их, поддерживая [[Атомарность (Atomacy)||атомарность]] в распределённой системе.


### Принцип работы

Протокол состоит из двух фаз:

- **Фаза подготовки (Prepare Phase)**
	- Координатор (Transaction Manager) отправляет участникам запрос: «Готовы ли вы зафиксировать транзакцию?»
	- Каждый узел проверяет, может ли он выполнить операцию, и отвечает «Готов» или «Отклоняю».
	- Участники сохраняют данные, но не фиксируют их (`PREPARE STATE`).
- **Фаза фиксации (Commit Phase)**
	- Если все участники ответили «Готов», координатор отправляет команду `COMMIT`, и данные окончательно сохраняются.
	- Если хоть один участник ответил «Отклоняю», координатор отправляет `ROLLBACK`, и все изменения отменяются.


### Проблема, которую решает 2PC

- В распределённых системах данные могут частично сохраниться, если один из участников не успеет обработать транзакцию.
- 2PC гарантирует, что либо все операции выполняются, либо ни одна → таким образом, система остаётся консистентной.


### Где применяется

- Распределённые базы данных
	- MySQL (XA Transactions)
	- PostgreSQL (Two-Phase Commit)
	- Oracle Distributed Transactions
- Транзакции в Java EE / Jakarta EE
	- Java Transaction API (JTA) + Java Transaction Service (JTS)
	- Используется в WildFly, WebLogic, WebSphere
- Брокеры сообщений
	- [[{TODO} Kafka Transactions||Kafka Transactions]]
	- JMS (Java Message Service)
- Банковские переводы, ERP-системы


### Пример [[Двухфазный Коммит (Two-Phase Commit, 2PC)||2PC]] в [[{TODO} SQL (Structured Query Language)||SQL]] (MySQL XA Transactions)

```mysql
XA START 'trx1';
INSERT INTO db1.orders VALUES (1, 'Laptop');
XA END 'trx1';
XA PREPARE 'trx1';

XA START 'trx2';
INSERT INTO db2.analytics VALUES (1, 'Laptop sold');
XA END 'trx2';
XA PREPARE 'trx2';

XA COMMIT 'trx1';
XA COMMIT 'trx2'; -- Если ошибка, выполняем XA ROLLBACK
```

### Пример [[Двухфазный Коммит (Two-Phase Commit, 2PC)||2PC]] в Java (JTA + Atomikos)

```java
UserTransaction utx = new InitialContext().lookup("java:comp/UserTransaction");

try {
    utx.begin();

    connPostgres.prepareStatement("INSERT INTO orders VALUES (1, 'Laptop')").executeUpdate();
    
    connMySQL.prepareStatement("INSERT INTO analytics VALUES (1, 'Laptop sold')").executeUpdate();

    utx.commit(); // Фиксируем обе операции
} catch (Exception e) {
    utx.rollback(); // Откатываем всё
}
```


### Недостатки

- Высокая задержка → блокирует ресурсы до завершения обеих фаз.
- Проблема отказоустойчивости → если координатор падает, участники могут зависнуть в неопределённом состоянии.
- Плохо масштабируется → для [[Микросервис (Microservice)||микросервисов]] чаще используют [[Сага (SAGA)||SAGA]], а не [[Двухфазный Коммит (Two-Phase Commit, 2PC)||2PC]].


### Когда 2PC лучше не использовать?

- В высоконагруженных системах (из-за блокировок и задержек).
- В микросервисной архитектуре (где лучше подходит [[Сага (SAGA)||SAGA]]).