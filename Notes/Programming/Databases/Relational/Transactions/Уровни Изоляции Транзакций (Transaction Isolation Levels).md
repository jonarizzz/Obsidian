
Уровни изоляции транзакций определяют, как [[Транзакция (Transaction)||транзакции]] взаимодействуют:

- [[Read Uncommitted||Read Uncommitted]]: позволяет читать неподтвержденные данные. Допускает:
	- [[Грязное Чтение (Dirty Read)]]
	- [[Не повторяемые чтения (Non-repeatable Reads)]]
	- [[Фантомные Чтения (Phantom Reads)]]
- [[Read Committed||Read Committed]]: позволяет читать только зафиксированные данные. Допускает:
	- [[Не повторяемые чтения (Non-repeatable Reads)]]
	- [[Фантомные Чтения (Phantom Reads)]]
- [[Repeatable Read||Repeatable Read]]: предотвращает повторяющиеся чтения. Допускает:
	- [[Фантомные Чтения (Phantom Reads)]]
- [[Serializable||Serializable]]: самый строгий уровень, транзакции выполняются последовательно, предотвращает все проблемы, но снижает производительность.