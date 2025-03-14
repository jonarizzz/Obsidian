
**Фантомная ссылка (Phantom Reference)** – это одна из [[Типы Ссылок (Reference Types)||видов ссылок в Java]], определенная в пакете `java.lang.ref`. Она используется для более точного контроля за [[Сборщик Мусора (Garbage Collector, GC)||сборкой мусора (GC)]], особенно когда требуется выполнить финализацию объекта перед его удалением из памяти.

### Ключевые особенности:

- **Объект недоступен напрямую** – в отличие от [[Мягкая Ссылка (SoftReference)||SoftReference]] и [[Слабая Ссылка (WeakReference)||WeakReference]], метод `.get()` у `PhantomReference` всегда возвращает `null`.
- **Сигнализирует о готовности объекта к удалению** – фантомные ссылки полезны для отслеживания, когда [[Объект (Object)||объект]] уже собран [[Сборщик Мусора (Garbage Collector, GC)||сборщиком мусора]].
- **Используется с ReferenceQueue** – фантомная ссылка должна быть связана с [[{TODO} ReferenceQueue||ReferenceQueue]], в которую она помещается, когда [[Объект (Object)||объект]] становится недостижимым.
- **Позволяет управлять очисткой ресурсов** – например, освобождать ресурсы (файлы, сокеты, нативную память) перед удалением объекта.


### Пример использования:

```java
import java.lang.ref.*;

class PhantomReferenceExample {
    public static void main(String[] args) throws InterruptedException {
        Object obj = new Object();
        ReferenceQueue<Object> referenceQueue = new ReferenceQueue<>();
        PhantomReference<Object> phantomRef = new PhantomReference<>(obj, referenceQueue);
		
        System.out.println("Before GC: " + phantomRef.get()); // Всегда null
		
        // Удаляем сильную ссылку
        obj = null;
		
        // Запускаем GC
        System.gc();
        Thread.sleep(100); // Ждем завершения GC
		
        // Проверяем очередь
        Reference<?> refFromQueue = referenceQueue.poll();
        if (refFromQueue != null) {
            System.out.println("Phantom reference was enqueued!");
        } else {
            System.out.println("Phantom reference is not yet enqueued.");
        }
    }
}
```


### Когда использовать?

- **Очистка ресурсов перед удалением [[Объект (Object)||объекта]]** – если [[Объект (Object)||объект]] работает с нативной памятью или файлами, фантомные ссылки помогут убедиться, что ресурсы освобождены.
- **Отложенная финализация** – `PhantomReference` считается более надежным, чем `finalize()`, который может вызывать проблемы с управлением памятью.
- **Отслеживание объектов перед их удалением [[Сборщик Мусора (Garbage Collector, GC)||GC]]** – если нужно точно узнать, когда объект становится недостижимым.
