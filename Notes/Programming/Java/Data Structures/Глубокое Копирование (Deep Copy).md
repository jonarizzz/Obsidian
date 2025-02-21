Глубокое копирование в Java — это процесс создания нового объекта, который является полным независимым копированием исходного объекта, включая все объекты, на которые тот [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылается]]. Это противоположно [[Поверхностное Копирование (Shallow Copy)||поверхностному копированию]], где создаётся новый объект, но ссылки на вложенные объекты остаются такими же, как у исходного.

Для глубокого копирования необходимо создать новые экземпляры всех вложенных объектов, а не просто копировать [[Ссылочный Тип Данных (Сильная Ссылка, Strong Reference, Link)||ссылки]] на них.

### Пример:

```java
class Person {
    String name;
    Address address;
	
    Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }
	
    // Метод для глубокого копирования
    public Person deepCopy() {
        // Создание нового экземпляра Person с новым адресом (копия, а не ссылка)
        return new Person(this.name, new Address(this.address.city, this.address.zipCode));
    }
}

class Address {
    String city;
    String zipCode;
	
    Address(String city, String zipCode) {
        this.city = city;
        this.zipCode = zipCode;
    }
}

public class Main {
    public static void main(String[] args) {
        Address address = new Address("New York", "10001");
        Person person1 = new Person("John", address);
		
        // Глубокое копирование
        Person person2 = person1.deepCopy();
		
        // Изменим адрес у person2
        person2.address.city = "Los Angeles";
		
        // Выведем адреса для проверки
        System.out.println(person1.address.city);  // Выведет: New York
        System.out.println(person2.address.city);  // Выведет: Los Angeles
    }
}
```

В этом примере `deepCopy()` создает новый объект `Person`, а также новый объект `Address`, что позволяет независимым образом изменять данные в копии, не затрагивая оригинал.