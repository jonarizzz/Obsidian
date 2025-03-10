**Инкапсуляция (Encapsulation)** — это принцип, который ограничивает доступ к данным [[Объект (Object)||объекта]] и позволяет управлять их изменением только через определённые методы. Защищает данные от неконтролируемого изменения и позволяет управлять их изменением только через безопасные методы.

Основная идея – защищать внутреннее состояние [[Объект (Object)||объекта]], предоставляя доступ только через публичные методы (геттеры и сеттеры).

Реализуется через [[Модификаторы Доступа (Access Modifiers)||модификаторы доступа]] (`private`, `protected`, `public`) в сочетании с методами для управления данными.


### Пример

```java
class BankAccount {
    private double balance; // Приватное поле - нельзя изменить напрямую
	
    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }
	
    public double getBalance() { // Геттер - только для чтения
        return balance;
    }
	
    public void deposit(double amount) { // Контролируемый доступ
        if (amount > 0) {
            balance += amount;
        }
    }
	
    public void withdraw(double amount) { // Контролируемый доступ
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount(1000);
        account.deposit(500);
        account.withdraw(200);
        System.out.println("Баланс: " + account.getBalance()); // Баланс: 1300
    }
}
```