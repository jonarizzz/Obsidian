
**Компоновщик (Composite)** – [[Структурные паттерны (Structural Patterns)||структурный паттерн]], который позволяет работать с деревьями [[Объект (Object)||объектов]], где отдельные элементы и группы элементов обрабатываются одинаково.

### Пример

```java
import java.util.*;

interface Component {
    void operation();
}

class Leaf implements Component {
    public void operation() { 
	    System.out.println("Leaf operation"); 
	}
}

class Composite implements Component {
    private final List<Component> children = new ArrayList<>();

    public void add(Component component) { 
	    children.add(component); 
	}
	
    public void operation() {
        System.out.println("Composite operation");
        for (Component child : children) child.operation();
    }
}

Composite root = new Composite();
Leaf leaf1 = new Leaf();
Leaf leaf2 = new Leaf();
root.add(leaf1);
root.add(leaf2);
root.operation();
```