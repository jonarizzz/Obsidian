**COUNT** — это агрегатная функция в базах данных, которая используется для подсчета количества строк в [[Таблица БД (Database Table, DB Table)||таблице]] или выборке. Она часто применяется в SQL-запросах для получения информации о количестве записей, удовлетворяющих определенным условиям.

### Основной синтаксис:

```sql
SELECT COUNT(*) FROM table_name;
```


### Примеры использования:

1. Подсчитать все строки в таблице:
```sql
SELECT COUNT(*) FROM employees;
```
  
2. Подсчитать строки с условием:
```sql
SELECT COUNT(*) FROM employees WHERE department = 'HR';
```

3. Подсчитать уникальные значения:
```sql
SELECT COUNT(DISTINCT department) FROM employees;
```

4. Подсчитать значения в конкретном столбце (исключая `NULL`):
```sql
SELECT COUNT(salary) FROM employees;
```


### Примечания:

- `COUNT(*)` подсчитывает все строки, включая те, где значения столбцов равны `NULL`.
- `COUNT(column_name)` подсчитывает только строки, где значение в указанном столбце не `NULL`.
