**Stop-the-World (STW)** — это термин, описывающий ситуацию, когда все [[Поток (Thread)||потоки]] в [[{TODO} Java||Java-программе]] останавливаются для выполнения операций [[Сборщик Мусора (Garbage Collector, GC)||сборщика мусора (GC)]]. Во время [[Stop-The-World (STW)||STW]] происходит очистка [[Память (Memory Model)||памяти]], реорганизация объектов или другие действия, которые требуют эксклюзивного доступа к памяти.


### Ключевые моменты

- **Причина остановки:** Все [[Поток (Thread)||потоки]] останавливаются, чтобы [[Сборщик Мусора (Garbage Collector, GC)||сборщик мусора]] мог очистить неиспользуемые [[Объект (Object)||объекты]] и освободить [[Память (Memory Model)||память]].
- **Типы пауз:**
	- **Minor GC:** Быстрые паузы для очистки молодого поколения.
	- **Full GC:** Длительные паузы для очистки всей [[Heap (Область Памяти)||кучи]].
- **Влияние на производительность:** [[Stop-The-World (STW)||STW]] может вызвать задержки в приложении, особенно при длительных паузах.
- **Минимизация влияния:** Современные сборщики мусора, такие как [[G1 GC||G1 GC]], [[ZGC||ZGC]] и [[Shenandoah GC||Shenandoah GC]], стараются уменьшить продолжительность [[Stop-The-World (STW)||STW-пауз]], улучшая производительность.
- **Присутствует в:**
	- [[Serial GC||Serial GC]]
	- [[Parallel GC||Parallel GC]]
