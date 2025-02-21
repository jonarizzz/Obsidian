**Observer (Наблюдатель)** — это поведенческий [[{TODO} Паттерны Проектирования||паттерн проектирования]], который используется для реализации механизма подписки. Он позволяет одному [[Объект (Object)||объекту]] (**наблюдаемому**, или **Subject**) уведомлять других [[Объект (Object)||объектов]] (**наблюдателей**, или **Observers**) об изменении своего состояния.

### Классическая реализация в Java

До [[{TODO} Java 9||Java 9]] в стандартной библиотеке были [[Интерфейс (Interface)||интерфейс]] `Observer` и [[Класс (Class)||класс]] `Observable`, но они устарели. Теперь этот паттерн реализуется вручную.

  
### Пример реализации

```java
import java.util.ArrayList;
import java.util.List;

// Интерфейс наблюдателя (Observer)
interface Observer {
    void update(String message);
}

// Класс наблюдаемого объекта (Subject)
class Subject {
    private final List<Observer> observers = new ArrayList<>();
	
    // Добавление наблюдателя
    public void addObserver(Observer observer) {
        observers.add(observer);
    }
	
    // Удаление наблюдателя
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }
	
    // Уведомление всех наблюдателей
    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

// Конкретный наблюдатель
class ConcreteObserver implements Observer {
    private final String name;
	
    public ConcreteObserver(String name) {
        this.name = name;
    }
	
    @Override
    public void update(String message) {
        System.out.println(name + " получил сообщение: " + message);
    }
}

// Тестовый запуск
public class ObserverPatternExample {
    public static void main(String[] args) {
        Subject subject = new Subject();
        
        Observer observer1 = new ConcreteObserver("Наблюдатель 1");
        Observer observer2 = new ConcreteObserver("Наблюдатель 2");
		
        subject.addObserver(observer1);
        subject.addObserver(observer2);
		
        subject.notifyObservers("Обновление данных!");
		
        subject.removeObserver(observer1);
		
        subject.notifyObservers("Еще одно обновление!");
    }
}
```


### Как это работает?

1. `Subject` (наблюдаемый объект) хранит список подписчиков (`observers`) и уведомляет их об изменениях.
2. `Observer` (наблюдатель) реализует метод `update()`, который вызывается при изменении состояния.
3. Класс `ConcreteObserver` представляет конкретного подписчика.
4. В `main()` добавляем наблюдателей и отправляем им сообщения.

  
### Где используется?

- Системы событий (например, GUI, кнопки, события в приложениях).
- [[{TODO} MVC||Модель-представление-контроллер (MVC)]] — `View` подписывается на `Model`.
- Паттерн [[{TODO} Паттерн Издатель-Подписчик (Pub-Sub)||“Издатель-Подписчик” (Pub/Sub)]].