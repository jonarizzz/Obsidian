**Шаблонный Метод (Template Method)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который определяет алгоритм, позволяя подклассам переопределять отдельные шаги без изменения структуры.


### Пример

```java
abstract class Template {

    public void execute() {
        step1();
        step2();
    }
    
    protected abstract void step1();
    protected abstract void step2();
}

class ConcreteClass extends Template {
    protected void step1() { System.out.println("Step 1 executed"); }
    protected void step2() { System.out.println("Step 2 executed"); }
}

Template template = new ConcreteClass();
template.execute();
```