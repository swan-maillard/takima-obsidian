---
cover: "[[spring.png]]"
---
# Java Persistence: ORM & JPA Fundamentals

## 🏗️ Core Concepts
**ORM (Object-Relational Mapping)**
- Technique converting data between OOP systems and relational databases
- Benefits:
  - No manual SQL writing
  - Database-agnostic code
  - Object-oriented data manipulation

**JPA (Java Persistence API)**
- Standard Java specification for ORM (JSR 338)
- Current version: **JPA 3.1** (Jakarta EE 9+)
- Implementations:
  - Hibernate (most popular)
  - EclipseLink
  - OpenJPA

Hibernate arrived **before** JPA

---

## 🧩 Key JPA Components

**Entities**
```java
@Entity
public class Product {
    @Id @GeneratedValue
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    // Getters/setters
}```


**Annotations Cheatsheet**

| Annotation | Purpose |
|------------|---------|
| `@Entity` | Marks class as persistent |
| `@Table` | Customizes table mapping |
| `@Id` | Marks primary key |
| `@GeneratedValue` | Configures ID generation |
| `@Column` | Field-to-column mapping |
| `@OneToMany`/`@ManyToOne` | Relationship mappings |


Let me expand on both the Entity Manager/Persistence Context and the N+1 problem in detail:

---

## 🔄 **Entity Manager & Persistence Context - Deep Dive**

### **Core Concept**
The `EntityManager` is your gateway to JPA operations, and the **Persistence Context** is its memory where it tracks entity states.

```java
EntityManager em = emf.createEntityManager(); // Creates a persistence context
```

**EntityManager** = JPA
**Session** = Hibernate's implementation

Better to use **EntityManager** to be implementation agnostic

### **Entity Lifecycle States**
1. **New (Transient)** 
   - Object created but not associated with persistence context
   ```java
   Product p = new Product(); // Transient state
   ```

2. **Managed (Persistent)**
   - Object attached to persistence context (tracked for changes)
   ```java
   em.persist(p); // Now managed
   p.setPrice(100); // Change automatically tracked!
   ```

3. **Detached**
   - Object was managed but lost connection (after `close()` or `clear()`)
   - Useful to give back the connection if there is a big computation to be done and you don't want to "take in hostage" the connection
   ```java
   em.detach(p); // OR em.close();
   p.setPrice(200); // Change NOT tracked
   ```

4. **Removed**
   - Scheduled for deletion from database
   ```java
   em.remove(p); // Will be deleted on flush
   ```

Data is persisted when **FLUSH** (often done automatically)

### **Critical Behaviors**
- **Automatic Dirty Checking**: Managed entities auto-detect changes
- **Flush Modes**: When SQL executes (`AUTO`, `COMMIT`, `ALWAYS`(not very performant),  manual `flush()`)
- **1st Level Cache**: Persistence context acts as a transaction-scoped cache

The app has a **pool of connection** (eg. HIKARI) => By default **10 connections**

---
## Transactional

### **Core Transaction Concepts**
Transactions ensure ACID (Atomicity, Consistency, Isolation, Durability) operations:
A => Atomic (all or nothing)
C => Coherent (stay in coherent state, linked to atomic)
I => Isolation ()
D => Durability (in time)


```java
@Transactional
public void placeOrder(Order order) {
    // All operations succeed or fail together
    orderRepository.save(order);
    inventoryService.reduceStock(order.getItems());
    paymentService.process(order.getPayment());
}
```

### **Transaction Boundaries**
1. **Container-Managed** (Spring/JEE)
   - Declared via `@Transactional`
   - Automatically handled by framework

2. **User-Managed**
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

### **Isolation Levels**
| Level | Behavior |
|-------|----------|
| `READ_UNCOMMITTED` | Dirty reads allowed |
| `READ_COMMITTED` (Default) | Prevents dirty reads |
| `REPEATABLE_READ` | Prevents non-repeatable reads |
| `SERIALIZABLE` | Full isolation (slowest) |

Configure in Spring:
```java
@Transactional(isolation = Isolation.REPEATABLE_READ)
```

### **Common Pitfalls**
1. **Self-Invocation** (calling `@Transactional` methods within same class)
2. **Long Transactions** holding database connections
3. **Wrong Propagation** causing unexpected rollbacks
4. **Open Persistence Context** with lazy loading after transaction ends
5. **Open-in-view** => By default true, keeps transaction context open

---

## Proxies

#### **1. Proxy-Based Transaction Management**
- **JDK Dynamic Proxy**: Used when beans implement interfaces (default for Spring AOP)
- **CGLIB Proxy**: Used when beans don't implement interfaces (requires `proxyTargetClass=true`)

```java
@Service
public class OrderService {
    @Transactional
    public void placeOrder(Order order) {
        // Business logic
    }
}
```

#### **2. How It Works Internally**
1. **Proxy Creation**: Spring wraps the `OrderService` in a proxy.
2. **Method Interception**: When `placeOrder()` is called, the proxy:
   - **Starts a transaction** (if needed)
   - **Delegates to the real method**
   - **Commits on success** or **rolls back on exception**
3. **AOP Advice**: The proxy applies `@Transactional` behavior via **around advice**.

#### **3. Key Implications**
- **Self-Invocation Bypasses Proxy**  
  → Calling `@Transactional` methods **internally** (without proxy) skips transaction management:
  ```java
  public void process() {
      this.placeOrder(order); // ❌ No transaction (self-invocation)
  }
  ```
  **Fix**: Inject proxy or use `AopContext.currentProxy()`.

- **Proxy vs. Real Object**  
  → `this` refers to the real instance, not the proxy.

- **Visibility Matters**  
  → `private` methods **cannot** be transactional (AOP can't proxy them).

#### **5. Performance Considerations**
- Proxy creation happens at startup (minimal runtime overhead).
- Use `@Transactional` at **class level** for all public methods if needed.
- Prefer **interface-based proxies** (JDK) for better compatibility.

---

### 🤝 Relationships
**Association Types**
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

**Cascade Types**
- `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`, `ALL`

---

## 🚨 **The N+1 Problem

### **What Happens?**
When fetching entities with relationships, JPA may generate:
- **1 query** for the parent entity
- **N additional queries** (one per child) if relationships are lazy-loaded

### **Example Scenario**
```java
@Entity
public class Order {
    @OneToMany(mappedBy = "order", fetch = FetchType.LAZY)
    private List<OrderItem> items;
}

// Later...
List<Order> orders = em.createQuery("SELECT o FROM Order o").getResultList();

for (Order o : orders) {
    o.getItems().size(); // Triggers N additional queries!
}
```

### **Why It's Bad**
- 100 Orders → 101 queries (1 + 100)
- Severe performance penalty

### **Solutions**

1. **JOIN FETCH (JPQL)**
   ```java
   SELECT o FROM Order o JOIN FETCH o.items
   ```
   - Single query with join

2. **EntityGraph**
   ```java
   @EntityGraph(attributePaths = {"items"})
   List<Order> findAll();
   ```

3. **DTO Projections**
   ```java
   SELECT new com.dto.OrderDTO(o.id, o.date, i.name) 
   FROM Order o JOIN o.items i
   ```
   - Avoids entity loading entirely

### LAZY common issues
=> LAZY INIT EXCEPTIONS

---

### ⚙️ Querying
**JPQL (Java Persistence Query Language)**
```java
TypedQuery<Product> q = em.createQuery(
    "SELECT p FROM Product p WHERE p.price > :minPrice", 
    Product.class
);
q.setParameter("minPrice", 500.0);
```

**Criteria API (Type-safe queries)**
```java
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<Product> cq = cb.createQuery(Product.class);
Root<Product> product = cq.from(Product.class);
cq.where(cb.gt(product.get("price"), 500.0));
```


---

### 🚀 Advanced Topics
**Caching**
- First-level (Persistence Context)
- Second-level (Shared cache)
- Query cache

**Performance Tips**
- Use `@BatchSize` for N+1 problems
- Prefer `JOIN FETCH` for eager loading
- Consider DTO projections

**Spring Data JPA**
```java
public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByPriceGreaterThan(double price);
}```

---

### 📝 Best Practices
1. Always manage transactions
2. Avoid entity serialization (use DTOs)
3. Monitor generated SQL
4. Use lazy loading judiciously
5. Keep bidirectional relationships synchronized