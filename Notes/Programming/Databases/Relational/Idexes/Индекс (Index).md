
Индекс — это структура данных, которая ускоряет поиск строк в таблице базы данных, позволяя быстрее находить данные по заданным критериям. Индексы используются для того, чтобы уменьшить время поиска при выполнении операций, таких как [[Синтаксис SELECT (FROM, WHERE, GROUP BY, HAVING, ORDER BY)||SELECT]], и могут быть созданы для одного или нескольких столбцов [[Таблица БД (Database Table, DB Table)||таблицы]].

Индексы обычно работают как указатели на строки данных, хранящиеся в таблице, и позволяют быстро определять местоположение этих строк, избегая необходимости линейного сканирования всей таблицы. Индексы могут быть полезны при выполнении операций сортировки, фильтрации и соединений ([[{TODO} Синтаксис JOIN||JOIN]]).

Однако стоит помнить, что индексы занимают дополнительное место в базе данных и могут замедлять операции вставки, обновления и удаления, так как индекс нужно обновлять при изменении данных в таблице.

### Виды индексов


- [[Позиционный индекс (B-дерево)]] – стандартный. Основан на структуре [[B-Дерево (B-Tree)||B-дерева]], обеспечивает сбалансированное хранение данных с минимальной глубиной. Подходит для операций поиска, вставки и удаления с логарифмической сложностью.
- [[Хеш-индекс (Hash Index)]] – использует [[Хэш-таблица (Hash Table)||хеш-таблицы]] для быстрого поиска точных значений, но не подходит для диапазонных запросов. Эффективен для уникальных и часто повторяющихся значений.
- [[Индекс по столбцу (Column-store index)]] – хранит данные в столбцах вместо строк, что ускоряет агрегирующие и аналитические запросы. Используется в [[Аналитическая База Данных||аналитических базах данных]] и [[{TODO} OLAP Система||системах OLAP]].
- [[Полнотекстовый индекс]] – позволяет выполнять быстрый поиск текста по большому объему данных, поддерживает морфологический анализ и ранжирование. Используется для поиска по текстовым полям, например, в системах поиска.
- [[Индекс для множественных столбцов (Composite Index)]] – содержит несколько столбцов в одной структуре индекса, оптимизируя запросы с несколькими условиями фильтрации. Порядок столбцов в индексе влияет на его эффективность.
- [[Индекс с уникальными значениями (Unique Index)]] – гарантирует уникальность значений в индексируемом столбце или комбинации столбцов. Используется для поддержки уникальных ограничений, например, в первичных ключах.
- [[Индекс с пространственными данными (Spatial index)]] – предназначен для обработки географических и многомерных данных. Поддерживает операции с геометрическими объектами, такие как поиск в радиусе или пересечение.
- [[Индекс на основе битовой карты (Bitmap Index)]] – использует битовые карты для представления данных, эффективен для столбцов с небольшим числом уникальных значений. Подходит для запросов в аналитических базах данных с большим объемом данных.
