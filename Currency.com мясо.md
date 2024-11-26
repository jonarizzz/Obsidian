
Привет, прошёл скрининг сегодня. Норм поболтали. Есть команда в которой не оч нужен опыт банковский, походу туда пихать будут.

На собесе был квиз из 6 тех вопросов по джаве и базам.

Complexity for searching an element in a balanced binary tree

Having this code:  
``` java
@RestController  
public class IncrementController {  
    private <<**A**>> int i;  
  
    @GetMapping("/increment")  
    public <<**B**>> void increment() {  
        System.out.print(i++);  
    }  
}  
```
  
what combination of modifiers A and B is going to guarantee "i" is equal to the exact number of endpoint invocations? (multiple options possible)  
A=volatile B=synchronized
A=volatile B=<<nothing>>
A=<<nothing>> B=synchronized
A=<<nothing>> B=<<nothing>>

What is the default scope of a Spring bean?  
Session
Singleton
Request
Prototype

You have Postgres table _users_. Which index will make the execution time of this query the fastest: 
select age, name, balance from users where name = 'John' and balance > 1000
? 

CREATE INDEX users_idx ON users (age, name, balance)
CREATE INDEX users_idx ON users (name, balance, age)
CREATE INDEX users_idx ON users (balance)
CREATE INDEX users_idx ON users (name);


Which protocol would be most suitable for live video streaming or online gaming?  
TCP
HTTP 1.1
UDP
WebSocket

What data structure is used to store information in the PostgreSQL indexes by default?  
B-Tree
LSM-Tree
Hash Table
Graph


Она мне скинула что повторить перед собесом, сижу вот охуеваю)
* sorting algorithms
* trees and hash functions
* logging system design
* analysis of a logical problem
* garbage collectors
* write quicksort code/pseudocode

Aliaksandr Karnilovich and Siarhei Akhramenka

Здаров, да эти челы и пришли. 

Дали задачку на то что будешь делать если медленный запрос стал. Дошли до того что предположим что проблема в базе

Спрашивали про sql, индексы, как работают, какие бывают

Как лучше построить составной индекс, какие вообще проблемы решают индексы, почему нельзя создать индекс на все колонки.

Спрашивали про уровни изоляции.

Была задачка как работать с пейментами если нельзы использовать Serealizable, но нужно поддерживать консистентность. Ответ: использовать оптимистик локи

Потом говорили про многопоточку: 

Если прийдут два потока смогут ли они у этого класса вызвать каждый свой метод?

Ответ - нет, тк будет синхронизация на уровне класса, нужно писать синхронизационный блок

``` java
	void synchronized increment() {
	   i++;
	}
```

``` java
	void synchronized increment2() {
	   j++;
	}
```

Поговорили как работает изнутри AtomicInteger

Ещё что-то про локи спрашивали.



Ну и потом завершили всё разговором про кафку. Чо куда каво, сколько партиций может быть. Обеспечение порядка чтения. Какие типы ASC есть. Про батч чтение поговорили

Надеюсь будет полезно для будущих ребят. Они юзали какой-то заготовленный список вопросов)

Могу ещё про лайвкодинг написать

Задачка чисто на джаве, мавен проект. Он пошарил на своём компе в идее и скинул ссылку. Задача написать библиотеку. Есть условная книжка и условный юзер, нужно иметь возможность забекать книжку в библиотеке. Нужно иметь возможность поставить чувака в очередь если книжка забукана. Нужно иметь возможность вернуть книжку. 

Чел писал красиво, через DDD, правильно оформлял репозитории. Потом обсуждали, добавил потокобезопасности, поставил read-write lock (на чтение и на запись), его устроило. Вместо красивости нужно чисто функционал ебашить. Чела смутило то что он не спросил насколько расписывать репозитории и прч. 

Артём вернулся, и мы обсудили твое
собеседование. Рад сообщить, что ты
произвёл положительное впечатление, и
собеседование с Артемом (а также
предыдущие собеседования с Сергеем и
Александром) пройдено. Хотя команда
выявила некоторые пробелы в твоих знаниях
Java Core и Kafka, мы считаем, что при
правильной поддержке ты мог бы добиться
больших успехов у нас!
Чтобы держать вас в курсе событий, прямо
сейчас я связываюсь с нашими менеджерами
по инжинирингу, чтобы узнать, какая из
команд может вам подойти (учитывая, что
некоторые команды не смогут предоставить
достаточно возможностей для роста в
области основных Java и Kafka/потребуют
более сильных навыков, в то время как
другие команды могут оказаться более
подходящими).
На данный момент наиболее вероятным
вариантом является наша команда MarTech, к
концу недели у меня должны появиться
новости от них и некоторых других команд.
Еще раз приношу извинения за задержку
обратной связи с Артемом, надеюсь, что
смогу ответить вам быстрее со следующими
обновлениями (или даже просто дать вам
знать, что мы помним о вас, я определенно
помню, я все еще держу за вас кулачки :))