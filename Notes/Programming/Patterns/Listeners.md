**Listeners** (слушатели) — это [[Объект (Object)||объекты]], которые реагируют на определенные события в программе. Они являются частью паттерна [[Наблюдатель (Observer)||Наблюдатель (Observer)]] и широко используются в GUI (например, в Swing), веб-приложениях (ServletContextListener) и других областях.

### Основные характеристики Listeners:

- Подписка на события — слушатель регистрируется у источника событий (например, кнопки).
- Обработка событий — когда событие происходит, вызывается метод слушателя.
- Интерфейсы — слушатели обычно реализуют определённые интерфейсы.


### Пример: слушатель для кнопки в Swing

В этом примере кнопка `JButton` регистрирует `ActionListener`, который реагирует на нажатие.

```java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class ButtonExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Example");
        JButton button = new JButton("Click me!");
		
        // Добавляем слушателя событий
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("Button clicked!");
            }
        });
		
        frame.add(button);
        frame.setSize(200, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
```

Когда пользователь нажимает кнопку, срабатывает `actionPerformed()`, и в консоль выводится "`Button clicked!`".


### Другие примеры Listeners:

- **MouseListener** — реагирует на действия мыши.
- **KeyListener** — реагирует на нажатие клавиш.
- **WindowListener** — следит за событиями окна (открытие, закрытие).
- **ServletContextListener** — слушает события жизненного цикла веб-приложения.


[[Наблюдатель (Observer)||Observer]] реагирует на изменение состояния объекта, а `Listener` — на конкретное событие (например, клик, нажатие клавиши).