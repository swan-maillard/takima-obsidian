---
cover: "[[spring.png]]"
---
## **1. Core Spring Concepts**  

### **What is Spring?**  

**Spring** is a powerful, open-source **Java framework** designed to simplify enterprise application development. It provides a comprehensive programming and configuration model for building **scalable, modular, and maintainable** applications. Spring’s core features include:  

- **Inversion of Control (IoC)** – Manages object creation and dependencies automatically.  
- **Dependency Injection (DI)** – Promotes loose coupling by injecting dependencies rather than hardcoding them.  

**Modules:**
- **Spring Core**
- **Aspect-Oriented Programming (AOP)** – Separates cross-cutting concerns (logging, security, transactions).  
- **Spring MVC** – A robust web framework for RESTful and traditional web apps.  
- **Spring Boot** – Simplifies setup with auto-configuration, embedded servers, and production-ready features.  
- **Spring Data** – Streamlines database access (JPA, MongoDB, Redis).  
- **Spring Security** – Handles authentication, authorization, and security threats.  

### **Why Use Spring?**  

1. **Modularity & Flexibility**  
   - Use only the modules you need (Core, MVC, Security, Data, etc.).  
   - Integrates seamlessly with other frameworks (Hibernate, Kafka, Quartz).  

2. **Productivity Boost**  
   - Reduces boilerplate code (e.g., JDBC, JPA).  
   - Spring Boot’s auto-configuration speeds up development.  

3. **Testability**  
   - DI makes unit testing easier (mock dependencies).  
   - `@SpringBootTest` simplifies integration testing.  

### **IoC & DI in Spring**  

#### **Inversion of Control (IoC)**  
- **Framework-managed** object lifecycle (creation, wiring, destruction)  
- **Developer declares** beans (`@Component`, `@Bean`), **Spring Container** handles the rest  
- **Flip of control**: Framework calls your code (vs. you calling libraries)  

#### **Dependency Injection (DI)**  
- **Dependencies provided externally** => No need to instantiate anymore
- **Primary types**:  
  - **Constructor injection** (✅ Preferred: immutable, testable)  
  - Setter injection  
  - Field injection (❌ Avoid: harder to test)  

#### **Why It Matters**  
- **Loose coupling**: Classes depend on abstractions (interfaces), not concrete implementations  
- **Easy testing**: Mock dependencies via constructor args  
- **Modular design**: Swap implementations without code changes (e.g., `@Profile`)  
- **Cleaner code**: No `new` keyword littered everywhere  

#### **Example**  
```java
// Without Spring ❌  
class ServiceA {  
    private ServiceB b = new ServiceB();  // Tight coupling  
}  

// With Spring DI ✅  
@Service  
class ServiceA {  
    private final ServiceB b;  
    public ServiceA(ServiceB b) {  // Injected  
        this.b = b;  
    }  
}  
```

### **Bean Scopes**  
| Scope         | Description |  
|--------------|------------|  
| `singleton` (Default) | One instance per container. |  
| `prototype` | New instance per request. |  
| `request` | One per HTTP request (web). |  
| `session` | One per user session (web). |  

### **Configuration Styles**  
| Method          | Example |  
|----------------|---------|  
| **XML** | `<bean id="service" class="com.example.Service"/>` |  
| **Annotations** | `@Component`, `@Service`, `@Repository` |  
| **Java Config** | `@Configuration` + `@Bean` methods |  

---
### **2. Spring Core**

Spring Core is the **central module** of the Spring Framework, providing the essential infrastructure for **dependency injection (DI)** and **Inversion of Control (IoC)**. At its heart is the **IoC Container**, which manages the lifecycle of Java objects (beans) and wires dependencies automatically.  

#### **Key Components**  
- **BeanFactory**: Basic container interface for bean instantiation and wiring.  
- **ApplicationContext**: Advanced container (extends `BeanFactory`) with additional features like:  
  - Internationalization (`MessageSource`)  
  - Event publication (`ApplicationEventPublisher`)  
  - Resource loading (`ResourceLoader`)  
- **Bean Scopes**: Controls bean lifecycle (`singleton`, `prototype`, request, session).  

#### **Why It Matters**  
- **Decouples components** through DI (no hardcoded dependencies)  
- **Centralizes configuration** (XML, annotations, or Java config)  
- **Enables testability** via mockable dependencies  
- **Provides consistent API** to access resources and environment  

---
## **3. Spring Boot**  

### **Core Features & Architecture**

#### **1. Auto-Configuration Magic**
- **Conditional Bean Loading**:  
  - Uses `@Conditional` variants (e.g., `@ConditionalOnClass`, `@ConditionalOnProperty`)  
  - Example: Auto-configures `DataSource` only if `spring.datasource.url` is set  
- **Custom Auto-Configuration**:  
  - Create `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`  
  - Use `@AutoConfiguration` + `@Conditional` for custom rules  

#### **2. Starter Packs
- **Starter Dependencies**:  
  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-jpa</artifactId>
  </dependency>
  ```
  - Brings in Hibernate, Spring Data JPA, JDBC, and connection pool automatically  

#### **3. Embedded Servers**

**Tomcat** is brought by the **spring-boot-starter-web**.

| Server   | Default Port | Key Feature                 | Best For             |
| -------- | ------------ | --------------------------- | -------------------- |
| Tomcat   | 8080         | Servlet 5.0 (Jakarta EE 9+) | Traditional web apps |
| Jetty    | 8080         | Lightweight, async support  | Reactive/High-load   |
| Undertow | 8080         | Non-blocking, low memory    | Microservices        |

#### **4. Actuator Endpoints**

| Endpoint   | Description                        | Security Consideration |     |
| ---------- | ---------------------------------- | ---------------------- | --- |
| `/health`  | App status (DB, disk space)        | Often exposed publicly |     |
| `/metrics` | JVM, HTTP stats (Prometheus-ready) | Restrict to admins     |     |
| `/env`     | All configuration properties       | Highly sensitive       |     |
| `/beans`   | List all Spring beans              | Debugging only         |     |


---

## **4. Spring MVC & REST**  

#### **1. Core Architecture**

**Front Controller Pattern:**
- `DispatcherServlet` (Central controller)
  - Handles all HTTP requests
  - Delegates to controllers via `HandlerMapping`
  - Processes results via `ViewResolver`

**Request Lifecycle:**
1. Request → DispatcherServlet
2. HandlerMapping selects controller
3. Controller processes request
4. Returns ModelAndView
5. ViewResolver renders response

#### **2. Key Components**

| Component | Purpose | Annotation/Interface |
|-----------|---------|----------------------|
| Controller | Business logic | `@Controller`, `@RestController` |
| HandlerMapping | Route requests | `@RequestMapping` |
| ViewResolver | Renders views | `InternalResourceViewResolver` |
| Model | Carries data | `Model`, `ModelMap` |
| MessageConverter | Serialization | `HttpMessageConverter` |

#### **3. REST Implementation**

**Essential Annotations:**
```java
@RestController
@RequestMapping("/api/v1")
public class UserController {

    @GetMapping("/users/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        // Implementation
    }

    @PostMapping("/users")
    public User createUser(@Valid @RequestBody UserDto userDto) {
        // Implementation
    }

    @PutMapping("/users/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody UserDto userDto) {
        // Implementation
    }

    @DeleteMapping("/users/{id}")
    public void deleteUser(@PathVariable Long id) {
        // Implementation
    }
}
```

**Exception Handling:**
- Global exception handler:
  ```java
  @ControllerAdvice
  public class GlobalExceptionHandler {
      
      @ExceptionHandler(ResourceNotFoundException.class)
      public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
          return ResponseEntity.status(HttpStatus.NOT_FOUND)
                  .body(new ErrorResponse(ex.getMessage()));
      }
  }
  ```

**Validation:**
```java
@PostMapping("/users")
public User createUser(@Valid @RequestBody UserDto userDto) {
    // Automatically validates based on UserDto annotations
}
```

#### **6. Performance Optimization**

1. **Caching:**
   ```java
   @GetMapping("/users/{id}")
   @Cacheable("users")
   public User getUser(@PathVariable Long id) {
       // Implementation
   }
   ```

2. **Async Processing:**
   ```java
   @GetMapping("/users")
   public CompletableFuture<List<User>> getAllUsers() {
       return CompletableFuture.supplyAsync(userService::findAll);
   }
   ```
	
3. **Pagination:**
   ```java
   @GetMapping("/users")
   public Page<User> getUsers(Pageable pageable) {
       return userService.findAll(pageable);
   }
   ```
   Request: `GET /users?page=0&size=20&sort=name,asc`


---

## **5. Spring Data JPA**  

### **Key Interfaces**  
- `CrudRepository` → Basic CRUD ops.  
- `JpaRepository` → JPA-specific methods (`flush()`, `saveAndFlush()`).  

### **Annotations**  
| Annotation                 | Purpose                   |
| -------------------------- | ------------------------- |
| `@Entity`                  | Marks a JPA entity class. |
| `@Table`                   | Customizes table name.    |
| `@Id`                      | Primary key.              |
| `@GeneratedValue`          | Auto-incremented ID.      |
| `@OneToMany`, `@ManyToOne` | Entity relationships.     |

---

## **6. Spring AOP (Aspect-Oriented Programming)**  

Spring AOP enables **modularization of cross-cutting concerns**—functionality that spans multiple layers of an application (e.g., logging, security, transactions). Unlike OOP, which organizes code into hierarchies, AOP **"weaves"** additional behavior into existing code **without modifying the original classes**.  

#### **Key Concepts**  
- **Aspect**: A module encapsulating cross-cutting logic (e.g., `LoggingAspect`).  
- **Advice**: The action taken by an aspect (e.g., `@Before`, `@After`, `@Around`).  
- **Pointcut**: A predicate defining where advice should be applied (e.g., `execution(* com.example.service.*.*(..))`).  
- **Join Point**: A specific point in execution (e.g., method invocation).  

#### **1. Aspect**
An aspect is a modular unit that encapsulates cross-cutting concerns. It's implemented as a regular Java class annotated with `@Aspect`. Aspects contain:
- Advice (the what)
- Pointcuts (the where)
- Introductions (adding new behavior to classes)

Example:
```java
@Aspect
@Component
public class TransactionAspect {
    // Contains advice and pointcut definitions
}
```

Key Characteristics:
- Reusable across application
- Configurable through Spring
- Can be ordered using `@Order` annotation

#### **2. Advice**
Advice defines both:
- The action to be taken
- When that action should execute

Spring supports five advice types:

| Advice Type     | Annotation        | Execution Timing                   |
| --------------- | ----------------- | ---------------------------------- |
| Before          | `@Before`         | Just before method execution       |
| After Returning | `@AfterReturning` | After successful method completion |
| After Throwing  | `@AfterThrowing`  | When method throws exception       |
| After (Finally) | `@After`          | After method (always executes)     |
| Around          | `@Around`         | Wraps entire method invocation     |

#### **3. Pointcut**
Pointcuts define where advice should be applied using expressions. Spring supports two approaches:

**A. Execution Designators**
```java
@Pointcut("execution(public * com.example.service.*.*(..))")
public void servicePublicMethods() {}

@Pointcut("within(@org.springframework.stereotype.Service *)")
public void serviceClassMethods() {}
```

**B. Combination Operators**
```java
@Pointcut("servicePublicMethods() && serviceClassMethods()")
public void combinedPointcut() {}
```

Common Pointcut Expressions:
- `execution([modifiers] return-type [declaring-type].method-name(params))`
- `within(package.or.class)`
- `@annotation(annotation-type)`
- `bean(bean-name-or-pattern)`

#### **4. Join Point**
A join point represents a specific point in program execution where advice can be applied. In Spring AOP, join points are always method executions.

Join Point Metadata Access:
```java
@Before("serviceMethods()")
public void logMethodDetails(JoinPoint jp) {
    // Get method signature
    String methodName = jp.getSignature().getName();
    
    // Get method arguments
    Object[] args = jp.getArgs();
    
    // Get target object
    Object target = jp.getTarget();
    
    // Get proxy object
    Object proxy = jp.getThis();
}
```

Key Differences:
- **Aspect**: The module containing the cross-cutting logic
- **Advice**: The action and its timing
- **Pointcut**: The predicate that matches join points
- **Join Point**: The specific execution point being intercepted

#### **Why Use AOP?**  
- **Separation of Concerns**: Keeps business logic clean (e.g., no logging code in services).  
- **Reusability**: Share aspects across multiple classes.  
- **Declarative Control**: Apply behaviors via annotations (e.g., `@Transactional`).  

#### **Practical Considerations**
1. **Proxy Limitations**: Spring AOP uses JDK dynamic proxies (for interfaces) or CGLIB (for classes)
2. **Performance Impact**: Each advised method adds slight overhead
3. **Best Practices**:
   - Keep aspect logic lightweight
   - Use specific pointcuts for better performance
   - Avoid advising too many methods
   - Consider compile-time weaving (AspectJ) for complex needs

---

## **7. Spring Security**  

### **Key Features**  
✔ **Authentication** (Form, JWT, OAuth2).  
✔ **Authorization** (`@PreAuthorize`, `@Secured`).  
✔ **CSRF Protection** (enabled by default).  

---

## **8. Common Interview Questions**  

### **Q1: What is the difference between `@Controller` and `@RestController`?**  
- `@Controller` → Returns **view names** (MVC).  
- `@RestController` → Returns **data** (REST API, = `@Controller` + `@ResponseBody`).  

### **Q2: How does Spring Boot Auto-Configuration work?**  
- Scans classpath for dependencies (e.g., `spring-boot-starter-data-jpa` → auto-configures `DataSource`).  
- Defined in `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`.  

### **Q3: Explain `@Transactional`**  
- Ensures **ACID** properties for DB operations.  
- **Propagation**: `REQUIRED` (default), `REQUIRES_NEW`.  
- **Isolation**: `READ_COMMITTED` (default).  

### **Q4: What is the difference between `@Component`, `@Service`, `@Repository`?**  
- All are stereotypes (mark classes as Spring beans).  
- `@Repository` → Adds **exception translation** (SQL → `DataAccessException`).  
- `@Service` → Business logic layer (semantic difference).  

---

## **9. Best Practices**  
✅ **Use constructor injection** (immutable, testable).  
✅ **Externalize configs** (`application.yml`, env vars).  
✅ **Follow layered/feature-based packaging**.  
✅ **Monitor with Actuator + Prometheus**.  
❌ **Avoid circular dependencies**.  