UNIQUE KEY (или ограничение уникальности) — это механизм, который обеспечивает уникальность значений в одном или нескольких столбцах [[Таблица БД (Database Table, DB Table)||таблицы]]. Это значит, что значения в указанных столбцах (или их комбинации) не могут повторяться.

### Основные особенности UNIQUE KEY

- Обеспечение уникальности – если на столбец или группу столбцов установлено ограничение UNIQUE, система проверяет, чтобы каждое значение (или их комбинация) встречалось только один раз.
- Разница с [[Первичный Ключ (Primary Key)||первичным ключом (PRIMARY KEY)]]:
	- У таблицы может быть только один [[Первичный Ключ (Primary Key)||PRIMARY KEY]], но несколько UNIQUE KEY.
	- [[Первичный Ключ (Primary Key)||PRIMARY KEY]] автоматически подразумевает уникальность и не допускает `NULL` значений.
	- В отличие от этого, UNIQUE KEY позволяет иметь одно или несколько `NULL` значений (в зависимости от базы данных).
- Индексация – при добавлении UNIQUE KEY для столбца или столбцов создаётся уникальный [[Индекс (Index)||индекс]], который ускоряет операции поиска и проверки уникальности.
- Комбинация нескольких столбцов – уникальность может применяться к комбинации двух или более столбцов.

### Как добавить UNIQUE KEY

При создании таблицы:
``` sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    username VARCHAR(50),
    UNIQUE (username)
);
```

В уже существующую таблицу:
``` sql
ALTER TABLE users ADD UNIQUE (email);
```

Для комбинации столбцов:
``` sql
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    UNIQUE (customer_id, product_id)
);
```


### Удаление UNIQUE

Чтобы удалить UNIQUE KEY, нужно знать его имя (оно создаётся автоматически или задаётся вручную). Узнать имя [[Индекс (Index)||индекса]] можно с помощью команды:
``` sql
SHOW INDEX FROM table_name;
```

Удаление выполняется так:
``` sql
ALTER TABLE table_name DROP INDEX unique_index_name;
```

### Практическое применение

Уникальные ключи используют для предотвращения дублирования данных, например, в таблицах:
- Пользователей (email, username).
- Продуктов (артикул, SKU).
- Календарей (уникальные события).

### Ограничения и особенности

- `NULL` значения:
	- В `MySQL` можно иметь несколько `NULL` значений в столбце с `UNIQUE KEY`.
	- В `PostgreSQL` и `Oracle` только одно `NULL` значение разрешено (в большинстве случаев).
- Производительность – уникальные индексы могут замедлять вставку данных, поскольку система должна проверять уникальность для каждой новой записи.