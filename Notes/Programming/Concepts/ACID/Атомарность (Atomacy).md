**Атомарность (Atomicity)** — это принцип, который гарантирует, что [[Транзакция (Transaction)||транзакция]] либо выполняется полностью, либо не выполняется вовсе.

Основная идея – нет промежуточных состояний — если что-то пошло не так, все изменения [[Откат Транзакции (Rollback)||откатываются]].


### Как это работает в базе данных

- Если [[Транзакция (Transaction)||транзакция]] включает несколько операций (`INSERT`, `UPDATE`, `DELETE`), и одна из них провалилась — все изменения [[Откат Транзакции (Rollback)||отменяются]] (`ROLLBACK`).
- Если все операции успешно выполнены — [[Транзакция (Transaction)||транзакция]] [[{TODO} Подтверждение Транзакции (Фиксирование Транзакции, Commit Transaction)||подтверждается]] (`COMMIT`).


### Пример в [[{TODO} SQL (Structured Query Language)||SQL]]

```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT; -- Подтверждаем изменения (оба запроса выполнены успешно)
```

Если произойдёт сбой между двумя `UPDATE`, то система [[Откат Транзакции (Rollback)||откатит изменения]], и деньги не исчезнут:

```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- В этот момент произошёл сбой! Операция перевода не завершена
ROLLBACK; -- Отмена всех изменений, чтобы данные остались целыми
```