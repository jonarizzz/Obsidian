**Строитель (Builder)** – [[Порождающие паттерны (Creational Patterns)||порождающий паттерн]], который разделяет создание сложного [[Объект (Object)||объекта]] на шаги.


### Пример

```java
class Car {
    private String engine, wheels;
	
    public static class Builder {
        private final Car car = new Car();
		
        public Builder setEngine(String engine) {
            car.engine = engine;
            return this;
        }
        
        public Builder setWheels(String wheels) {
            car.wheels = wheels;
            return this;
        }
        
        public Car build() { return car; }
    }
}

Car car = new Car.Builder().setEngine("V8").setWheels("Alloy").build();
```

Пример реализации – [[StringBuilder||StringBuilder]]