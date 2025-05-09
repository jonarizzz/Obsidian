**ZGC (Z Garbage Collector)** — это современный [[Сборщик Мусора (Garbage Collector, GC)||сборщик мусора]] в Java, предназначенный для работы с очень низкими паузами (не превышающими 1–2 мс) независимо от размера [[Heap (Область Памяти)||кучи]] (даже терабайты памяти). Может потреблять больше CPU, чем другие [[Сборщик Мусора (Garbage Collector, GC)||GC]].

  
### Основные особенности:

- **Низкие паузы GC** – основное преимущество ZGC. Он работает в основном в фоновом режиме и избегает длинных стопов мира ([[Stop-The-World (STW)||Stop-the-world]]).
- **Масштабируемость** – поддерживает [[Heap (Область Памяти)||кучи]] от мегабайт до терабайт.
- **Не требует ручной настройки** – по умолчанию работает оптимально.
- **Компактизация памяти** – дефрагментирует [[Heap (Область Памяти)||кучу]] без длительных пауз.
- **Использует механизм “colored pointers”** – метки в указателях помогают отслеживать состояние [[Объект (Object)||объектов]].

  
### Как включить?

ZGC доступен начиная с [[{TODO} Java 11||JDK 11]] как экспериментальный, а с [[{TODO} Java 15||JDK 15]] – в продакшн-версии. Чтобы его включить, передайте [[Виртуальная Машина Java (Java Virtual Machine, JVM)||JVM]] флаг:

```
java -XX:+UseZGC -jar your_app.jar
```

Можно также задать размер [[Heap (Область Памяти)||кучи]]:

```
java -XX:+UseZGC -Xmx16g -jar your_app.jar
```


### Когда использовать?

- Если вам нужны минимальные задержки в GC (например, для low-latency сервисов).
- Если ваше приложение работает с очень большими объемами данных (более 16 ГБ RAM).
- Если у вас Java 11+ и современный процессор.


### Когда НЕ использовать?

- Если у вас небольшая [[Heap (Область Памяти)||куча]] (<1ГБ) и ZGC просто не даст значительных преимуществ.
- Если ваше приложение активно использует `-XX:+UseStringDeduplication`, т.к. ZGC пока его не поддерживает.


### Принцип работы:
  

ZGC использует **конкурентный алгоритм**, который выполняет большинство операций без остановки всех потоков ([[Stop-The-World (STW)||stop-the-world]]). Главная идея – разделить [[Сборщик Мусора (Garbage Collector, GC)||сборку мусора]] на несколько фаз, выполняемых в фоновом режиме, так чтобы паузы были минимальными.


### Фазы выполнения:

1. **“Colored Pointers” (Цветные указатели)** – ZGC использует 64-битные указатели с дополнительными 4 битами, которые помогают отслеживать состояние [[Объект (Object)||объектов]] без модификации самой памяти. Благодаря этому ZGC избегает длинных блокировок и может двигать [[Объект (Object)||объекты]] в памяти без остановки мира. Каждый [[Объект (Object)||объект]] в [[Heap (Область Памяти)||куче]] может быть в одном из трех состояний:
	1. **Белый** (White) – [[Объект (Object)||объект]] доступен и не обработан [[Сборщик Мусора (Garbage Collector, GC)||сборщиком мусора]].
	2. **Серый** (Gray) – [[Объект (Object)||объект]] в процессе обработки (перемещается или проверяется).
	3. **Черный** (Black) – [[Объект (Object)||объект]] обработан и безопасен.
2. **Concurrent Compacting GC (Конкурентная компактизация)** – обычные GC (например, [[G1 GC||G1]]) сталкиваются с проблемой [[Фрагментация Памяти (Memory Fragmentation)||фрагментации памяти]], поэтому периодически выполняют стоп-длину компактизации. ZGC решает это за счёт асинхронного перемещения [[Объект (Object)||объектов]] во время работы программы. Когда ZGC перемещает объект:
	1. Он непосредственно обновляет указатели на него с помощью “цветных указателей”.
	2. Это делает процесс безопасным и без остановки всех [[Поток (Thread)||потоков]].
3. Concurrent Phases (Конкурентные фазы работы)
	1. **Mark Start (начало маркировки)** – очень короткая пауза (1-2 мс), в которой ZGC отмечает корневые [[Объект (Object)||объекты]].
	2. **Concurrent Marking (конкурентная маркировка)** – выполняется в фоне, определяя “живые” [[Объект (Object)||объекты]].
	3. **Concurrent Relocation (конкурентное перемещение)** – [[Объект (Object)||объекты]] перемещаются в новые области без остановки приложения.
	4. **Relocation Phase (финальное перемещение)** – очень короткая пауза (1-2 мс) для завершения процесса.