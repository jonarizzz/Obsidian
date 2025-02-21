SELECT — это одна из ключевых команд в языке SQL (Structured Query Language), которая используется для выборки данных из [[Реляционные Базы Данных (Relational Database)||базы данных]]. Она позволяет извлекать данные из одной или нескольких таблиц в зависимости от указанных условий.

### Общий синтаксис

``` sql
SELECT [столбцы] 
FROM [таблица] 
[WHERE условие] 
[GROUP BY столбец] 
[HAVING условие] 
[ORDER BY столбец];
```


### Основные компоненты:

1. **SELECT** — указывает, какие столбцы нужно извлечь. Можно использовать * для выборки всех столбцов.
```sql
SELECT * FROM users; -- Выбрать все столбцы из таблицы "users"
SELECT id, name FROM users; -- Выбрать только id и name
```

2. **FROM** — указывает таблицу, из которой будут извлечены данные.
```sql
SELECT name FROM employees; -- Извлечь столбец "name" из таблицы "employees"
```

3. **WHERE** — добавляет фильтрацию данных (условия выборки).
```sql
SELECT * FROM orders WHERE status = 'completed'; -- Выбрать завершенные заказы
```

4. **GROUP** BY — группирует строки, которые имеют одинаковые значения в указанном столбце, часто используется с агрегатными функциями (SUM, AVG, COUNT, и т.д.).
```sql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department; -- Подсчитать сотрудников по отделам
```

5. **HAVING** — фильтрует результаты после группировки.
```sql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department 
HAVING COUNT(*) > 10; -- Выбрать отделы, где больше 10 сотрудников
```

6. **ORDER BY** — сортирует результаты по указанным столбцам.
``` sql
SELECT name, salary 
FROM employees 
ORDER BY salary DESC; -- Отсортировать сотрудников по зарплате (по убыванию)
```

### Примеры:

7. Выбрать всех пользователей:
```sql
SELECT * FROM users;
```

8. Выбрать только имена и даты регистрации пользователей:
```sql
SELECT name, registration_date FROM users;
```

9. Найти всех пользователей старше 30 лет:
```sql
SELECT * FROM users WHERE age > 30;
```

10. Подсчитать количество заказов по статусам:
```sql
SELECT status, COUNT(*) FROM orders GROUP BY status;
```

11. Отсортировать список пользователей по имени:
```sql
SELECT * FROM users ORDER BY name ASC;
```