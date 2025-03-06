  
## 🎓 Context
During this milestone, we were asked the following objectives:

+ Implement **Flyway** to **Spring Boot** for handling database migrations.
+ Using **Hibernate** to bind our **Models** to the database **Entities**.
	+ Understand different **Id generation policies***.
+ Use the **EntityManager** in our **DAOs** to query the database with **JPQL** statements.
	+ Make use of **Transactional** and **Read-only Transactional** in our implementations.
+ Serve **API endpoints** to access and manipulate the data.
+ Use **Embeddable** models and **Enumerated** to nicely handle our entities fields.
	+ Create **Converters** when need of mapping an Enum and an entity field.
+ Handle **relationships** between entities, with **ManyToMany**, **ManyToOne**, **OneToMany** and **OneToOne** relations.
+ Implement **Inheritance** between entities and choose pertinent Strategy (for instance I chose **JOINED Strategy**).
+ Add **Entity Validation** with annotations.
+ Understand **Lazy** and **Eager** fetching strategies and how to avoid the **N+1 problem**. Basically, default at **Lazy Fetch** and perform **JOIN FETCH** whenever necessary.
+ Write more complete **tests** for each services.

## 📝 Progress
I have produced the following bonuses:
- Implement **PrePersist** and **PreUpdate** on Carts to automatically update last time of update.
- Added **L2 Caching** with **Hazelcast** and understanding the different **Caching Strategies**.

## 🤔 Difficulties
It went mostly well, but I sometimes struggle handling **Lazy Fetching**, I often didn't recognize a problem before running tests.
The **Caching** part was also a lot of struggles, I couldn't manage to make it work : even though Hazelcast was running and the caching enabled, Hibernate kept sending requests to the db. I tried logged in Hibernate, in Postgres, by enabling the statistics, but impossible to understand the problem. Hazelcast was performing "PUT" operations in the L2 cache, but never performed "HIT" operation to retrieve the cached data. Very mysterious.

