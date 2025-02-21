В Java ключевое слово `static` используется для обозначения членов [[Класс (Class)||класса]] (переменных, методов, блоков и вложенных классов), которые принадлежат самому классу, а не конкретному экземпляру.


### Где можно использовать static?


##### Статические переменные (поля класса)

Они принадлежат [[Класс (Class)||классу]] и разделяются всеми его экземплярами.

```java
class Example {
    static int counter = 0;
}

public class Main {
    public static void main(String[] args) {
        Example.counter++;  // Можно обращаться через имя класса
        System.out.println(Example.counter); // 1
    }
}
```

  

##### Статические методы

Они могут вызываться без создания [[Объект (Object)||экземпляра класса]], но не могут напрямую использовать нестатические переменные или методы.

```java
class Utils {
    static int square(int x) {
        return x * x;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(Utils.square(5)); // 25
    }
}
```

  

##### Статические блоки инициализации

Используются для выполнения кода при загрузке [[Класс (Class)||класса]].

```java
class Example {
    static int value;
	
    static {
        value = 42;
        System.out.println("Статический блок инициализации выполнен");
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(Example.value); // 42
    }
}
```

  

##### Статические вложенные классы

В отличие от обычных [[Вложенный Класс (Inner Class)||вложенных классов]], статический [[Класс (Class)||класс]] не привязан к экземпляру внешнего [[Класс (Class)||класса]].

```java
class Outer {
    static class Nested {
        void hello() {
            System.out.println("Привет из статического вложенного класса!");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer.Nested obj = new Outer.Nested();
        obj.hello();
    }
}
```

  
### Когда использовать static?

- Если значение переменной относится ко всему [[Класс (Class)||классу]], а не к конкретному [[Объект (Object)||объекту]].
- Если метод не использует нестатические члены [[Класс (Class)||класса]].
- Для создания утилитарных методов (например, `Math.sqrt()`).
- Для [[Вложенный Класс (Inner Class)||внутренних классов]], которым не нужен доступ к полям внешнего класса.
