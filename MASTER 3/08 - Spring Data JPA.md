---
cover: "[[spring_jpa.png]]"
---
# 💠Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
---

# 💠 Core Concepts

## 1. **ORM (Object-Relational Mapping)**
- **ORM** are tools that map Java objects to database tables. It lets you use Java code to persist, retrieve, and manipulate data without writing raw SQL.
- Benefits:
	- Cleaner, object-oriented data access
	- Database-agnostic (switch DBs with minimal change)
	- Avoids repetitive JDBC boilerplate

## 2. **JPA (Java Persistence API)**
- **JPA** is the **standard specification** for ORM in Java.
- It defines **annotations and interfaces** for entity mapping, persistence contexts, transactions, and queries.
- Latest version: **JPA 3.x**
- Implementations are **Hibernate** (Red Hat), **EclipseLink**, **OpenJPA** (Apache)

## **3. Hibernate (JPA Implementation)**
- Hibernate is the **most widely used** implementation of JPA.
- It existed **before JPA** and influenced its creation.
- Hibernate adds extra features like caching, advanced query capabilities, and more flexible mappings.
- Latest version: **Hibernate 6.x** (default in Spring Boot 3.x)
- Requires **jakarta.persistence** packages

---

# 💠 JPA Annotations

| Annotation | Purpose |
|------------|---------|
| `@Entity` | Marks class as persistent |
| `@Table` | Customizes table mapping |
| `@Id` | Marks primary key |
| `@GeneratedValue` | Configures ID generation |
| `@Column` | Field-to-column mapping |
| `@OneToMany`/`@ManyToOne` | Relationship mappings |


---

# **💠 Persistence Context**

## 1. Entity Manager
The `EntityManager` is the **central interface** in JPA for performing **CRUD operations** on database entities.
- It **manages the lifecycle** of entities.
- Each `EntityManager` is associated with a **Persistence Context**—an in-memory cache that tracks entity state and identity within a transaction.
```java
EntityManager em = emf.createEntityManager(); // New persistence context
```
> **EntityManager** => Standard JPA  
> **Session** => Hibernate’s implementation (extends EntityManager)
> => Use `EntityManager` for **portability across JPA providers**.

Applications typically use a **connection pool** (e.g., **HikariCP**, default in Spring Boot).
- Default: ~10 connections
- Each persistence context borrows a connection **only when needed** (on flush/commit).

## 2. **Entity Lifecycle States**
JPA entities move through **four lifecycle states**:

1. **New (Transient)**
	- Object created but not associated with persistence context

2. **Managed (Persistent)**
	- Tracked by the persistence context
	- Changes are automatically synchronized with the DB (on flush)

3. **Detached**
	- Was managed, but now outside the persistence context (e.g., after `em.close()` or `em.clear()`).
	- Changes won’t be saved unless re-attached.
	- Useful when doing long computations and don’t want to hold a DB connection.

4. **Removed**
	- Marked for deletion; will be deleted on `flush()` or `commit()`.

## 3. **Critical Behaviors**
- **1st-Level Cache**: All managed entities are cached in the persistence context during a transaction.
- **Automatic Dirty Checking**: Tracks changes to managed entities and syncs them on flush.
- **Flush**: Sends SQL changes to DB.
    - Triggered manually or automatically (e.g., before query execution or on commit)
- **Flush Modes**: 
	- When SQL executes (`AUTO`, `COMMIT`, `ALWAYS`(not very performant),  manual `flush()`)


---
# 💠 Transactional

## 1. What is a Transaction
A **transaction** is a unit of work that groups multiple database operations into one atomic action, ensuring **data integrity** through **ACID** properties:

- **A – Atomicity**: All or nothing; partial updates are not allowed.
- **C – Consistency**: DB remains in a valid state before & after.
- **I – Isolation**: Transactions are isolated from one another.
- **D – Durability**: Committed changes are permanent—even after crashes.

## 2. Managing Transactions
1. **Declarative (Container-Managed)** 
   - Declared via `@Transactional` 
   - Spring handles start, commit, rollback

2. **Programmatic (Manual Control)**
   - Manual begin/commit/rollback
   ```java
   EntityTransaction tx = em.getTransaction();
   try {
       tx.begin();
       // JPA operations
       tx.commit();
   } catch (Exception e) {
       tx.rollback();
   }
   ```

### 3. **Common Pitfalls**
1. **Self-Invocation** : Calling `@Transactional` methods from the same class bypasses proxy, so no transaction is started.
2. **Long Transactions**: Holding DB connection too long = performance issues.
3. **LazyInitializationException**: Accessing lazy fields after transaction closes.
4. **Open Session in View**: Keeps persistence context open during view rendering (can lead to lazy load + performance problems). Default: `true` in Spring Boot, but we prefer putting it at `false`.

---

# 💠 Proxies

## 1. **What is a Proxy?**
A **proxy** is a **wrapper object** that stands in for the real bean. Instead of calling the actual bean directly, Spring calls the proxy, which can add extra behavior **before or after** the real method executes.
## 2. **How Proxies Work
1. Spring creates a proxy wrapping your bean.
2. Method calls go to the proxy first.
3. Proxy can run **additional logic** (e.g., start transaction, check security).
4. Proxy calls the **actual bean method**.
5. Proxy executes any **post-processing** (commit, logging, etc.).

This pattern is used by **Spring AOP** for all kinds of aspects, including `@Transactional`.

## 3. **Limitations of Proxies**

- **Self-invocation bypass**: Calls from within the same class don’t go through the proxy, so advice (like transactions) is skipped.
- Proxies only intercept **public method calls** by default.

---

# 💠 Relationships

```java
// 1:1 => FETCH
@OneToOne
private UserProfile profile;

// 1:N (Parent side) => LAZY 
@OneToMany(mappedBy = "order")
private List<OrderItem> items;

// N:1 (Child side) => FETCH
@ManyToOne 
private Order order;

// N:M => LAZY
@ManyToMany
private List<Category> categories;
```

There are 2 **fetch types**:
- **LAZY (default for `@OneToMany` and `@ManyToMany`)**:  
    Related entities are **not loaded** immediately. Instead, they're fetched **only when accessed** (via proxy). This improves performance by avoiding unnecessary data loads.  

- **EAGER (default for `@OneToOne` and `@ManyToOne`)**:  
    Related entity is **fetched immediately** with the parent, using a **JOIN** query. This can lead to **performance issues** if not carefully managed.  

---

# 💠 **The N+1 Problem

## 1. **What Is It?**

In JPA, when fetching a parent entity with a **lazy-loaded** collection (e.g., `@OneToMany`), it causes:
- **1 query** for the parent(s)
- **N queries** for each child collection (1 per parent)

Example: Fetching 100 students from 1 university → **1 + 100 = 101 queries**

It makes many small queries which **scales badly** because slow.


## 3. **Solutions**

1.  **`JOIN FETCH` (JPQL)**
	Forces eager loading in a single query
```java
SELECT o FROM Order o JOIN FETCH o.items
```

2. **`@EntityGraph`**
	Declarative way to specify eager relationships:
```java
@EntityGraph(attributePaths = {"items"})
List<Order> findAll();
```

3. **Projections**
	Fetch only needed fields directly into a Projection:
```java
SELECT new com.dto.OrderProjection(o.id, o.date, i.name) 
FROM Order o JOIN o.items i
```
