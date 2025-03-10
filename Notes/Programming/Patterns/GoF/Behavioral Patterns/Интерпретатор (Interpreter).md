**Интерпретатор (Interpreter)** – [[Поведенческие паттерны (Behavioral Patterns)||поведенческий паттерн]], который определяет грамматику, а затем интерпретирует её для выполнения. Этот паттерн используется для реализации языков программирования или форматов данных.


### Пример

```java
interface Expression {
    boolean interpret(String context);
}

class TerminalExpression implements Expression {
    private final String data;
    
    public TerminalExpression(String data) { 
	    this.data = data; 
	}
	
    public boolean interpret(String context) { 
	    return context.contains(data); 
	}
}

class OrExpression implements Expression {
    private final Expression expr1;
    private final Expression expr2;
    
    public OrExpression(Expression expr1, Expression expr2) { 
	    this.expr1 = expr1; this.expr2 = expr2; 
	}
	
    public boolean interpret(String context) { 
	    return expr1.interpret(context) || expr2.interpret(context); 
	}
}

class InterpreterDemo {
    public static void main(String[] args) {
        Expression isMale = new TerminalExpression("Male");
        Expression isMarried = new TerminalExpression("Married");
        Expression isMarriedMale = new OrExpression(isMale, isMarried);
		
        System.out.println("Is Male or Married? " + isMarriedMale.interpret("Male"));
        System.out.println("Is Male or Married? " + isMarriedMale.interpret("Single"));
    }
}
```