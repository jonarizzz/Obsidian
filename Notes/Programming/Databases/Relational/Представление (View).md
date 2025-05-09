
**Представление (view) в базе данных** — это виртуальная таблица, которая формируется на основе результата выполнения SQL-запроса. Она не хранит данные самостоятельно, а предоставляет доступ к данным, которые извлекаются из одной или нескольких таблиц (или других представлений) в момент выполнения запроса.

### Основные характеристики представлений:

- **Виртуальность**: Представления не хранят данные. Они “живут” только как результат выполнения запроса.
- **Упрощение работы**: Представления позволяют скрыть сложность SQL-запросов, предоставляя пользователю упрощённый доступ к данным.
- **Безопасность**: Представления могут использоваться для ограничения доступа к определённым столбцам или строкам в таблице, предоставляя только нужные данные.
- **Обновляемость**: Некоторые представления поддерживают операции вставки, обновления и удаления данных, если они построены на базе одной таблицы и удовлетворяют определённым условиям.

  

### Пример использования представления:

**Создание представления:**

```sql
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE status = 'active';
```

В этом случае active_users — это представление, которое отображает только активных пользователей из таблицы users.


**Использование представления:**

```sql
SELECT * FROM active_users;
```

Этот запрос вернёт все строки из виртуальной таблицы active_users, а данные будут извлечены в реальном времени из таблицы users.

### Преимущества представлений:

- Упрощают сложные запросы.
- Повышают читаемость и повторное использование кода.
- Повышают уровень безопасности, скрывая определённые данные.
- Позволяют создать абстракцию поверх таблиц.

### Ограничения:

- Производительность может быть ниже, так как данные извлекаются при каждом запросе.
- Некоторые представления нельзя обновлять (например, если используются агрегатные функции, подзапросы и т.д.).
- Не все базы данных поддерживают материализованные представления (физическое сохранение данных).