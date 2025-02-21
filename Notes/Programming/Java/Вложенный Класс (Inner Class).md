Во вложенных классах (Inner Class) в Java один класс определяется внутри другого. Вложенные классы могут использоваться для логической организации кода и обеспечения удобного доступа к полям и методам внешнего [[Класс (Class)||класса]].  

### Статический вложенный класс (Static Nested Class)

Этот класс объявляется с модификатором static и не имеет доступа к нестатическим полям и методам внешнего класса.

```java
class Outer {
    static class StaticNested {
        void display() {
            System.out.println("Это статический вложенный класс");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer.StaticNested nested = new Outer.StaticNested();
        nested.display();
    }
}
```

### Нестатический (обычный) вложенный класс (Non-static Inner Class)

Этот класс связан с экземпляром внешнего класса и может обращаться к его полям и методам, включая private.

```java
class Outer {
    private String message = "Привет из внешнего класса!";
	
    class Inner {
        void display() {
            System.out.println(message);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.display();
    }
}
```

### Локальный класс (Local Inner Class)

Определяется внутри метода и доступен только в этом методе.

```java
class Outer {
    void outerMethod() {
        class LocalInner {
            void display() {
                System.out.println("Это локальный вложенный класс");
            }
        }
        LocalInner localInner = new LocalInner();
        localInner.display();
    }
}

public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.outerMethod();
    }
}
```

### [[Анонимный Класс (Anonymous Class)||Анонимный класс (Anonymous Inner Class)]]

Это класс без имени, который создается на лету, часто для реализации [[Интерфейс (Interface)||интерфейсов]] или наследования.

```java
abstract class Greeting {
    abstract void sayHello();
}

public class Main {
    public static void main(String[] args) {
        Greeting greeting = new Greeting() {  // Анонимный класс
            void sayHello() {
                System.out.println("Привет из анонимного класса!");
            }
        };
        greeting.sayHello();
    }
}
```


### Когда использовать?

- Если вложенный класс логически связан с внешним и не используется отдельно.
- Чтобы инкапсулировать детали реализации, скрывая вложенный класс от других частей программы.
- Для создания компактного кода с [[Анонимный Класс (Anonymous Class)||анонимными классами]], например, при использовании обработчиков событий.