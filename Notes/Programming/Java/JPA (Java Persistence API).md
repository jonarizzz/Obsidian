JPA (Java Persistence API) — это спецификация для управления [[Объектно-Реляционное Отображение (Object-Relational Mapping, ORM)||объектно-реляционным отображением (ORM)]] в Java-приложениях. Она определяет стандартизированный способ взаимодействия с [[Реляционные Базы Данных (Relational Database)||реляционными базами данных]] через [[ООП – Объектно-Ориентированное Программирование (OOP, Object Oriented Programming)||объектно-ориентированные]] модели.


### Основные особенности JPA:

- Является спецификацией, а не конкретной реализацией. Популярные реализации:
	- [[{TODO} Hibernate||Hibernate]] (самая распространенная)
	- EclipseLink
	- OpenJPA
- Использует аннотации для определения сущностей и их связей:
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
	
    @Column(nullable = false)
    private String name;
}
```
- Позволяет управлять жизненным циклом объектов, выполняя [[CRUD (Create, Read, Update, Delete)||CRUD-операции]]:
```java
EntityManager em = entityManagerFactory.createEntityManager();
em.getTransaction().begin();
em.persist(new User("Yauheni"));
em.getTransaction().commit();
em.close();
```
- Поддерживает связи между сущностями ([[{TODO} OneToOne (аннотация)||@OneToOne]], [[{TODO} OneToMany (аннотация)||@OneToMany]], [[{TODO} ManyToOne (аннотация)||@ManyToOne]], [[{TODO} ManyToMany (аннотация)||@ManyToMany]]).
- Позволяет использовать [[{TODO} JPQL||JPQL (Java Persistence Query Language)]] — аналог [[{TODO} SQL (Structured Query Language)||SQL]], но работающий с [[Объект (Object)||объектами]], а не с [[Таблица БД (Database Table, DB Table)||таблицами]].
```java
List<User> users = em.createQuery("SELECT u FROM User u WHERE u.name = :name", User.class)
	 .setParameter("name", "Yauheni")
	 .getResultList();
```

  

### Когда использовать JPA?

- Если нужно работать с [[База данных (БД, Database, DB)||базами данных]] в [[ООП – Объектно-Ориентированное Программирование (OOP, Object Oriented Programming)||объектно-ориентированном]] стиле.
- Когда важна переносимость кода между разными [[База данных (БД, Database, DB)||базами данных]] ([[{TODO} SQL (Structured Query Language)||SQL]]-синтаксис у БД может отличаться, а JPA абстрагирует это).
- В больших проектах, где нужно управлять сложными связями между [[Объект (Object)||объектами]].