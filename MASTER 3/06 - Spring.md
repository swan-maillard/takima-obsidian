---
cover: "[[spring.png]]"
---
# 💠Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: true # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
---

# **💠  Core Spring Concepts**  

## **1. What is Spring?**  

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

## **2. Why Use Spring?**  

1. **Modularity & Flexibility**  
   - Use only the modules you need (Core, MVC, Security, Data, etc.).  
   - Integrates seamlessly with other frameworks (Hibernate, Kafka, Quartz).  

2. **Productivity Boost**  
   - Reduces boilerplate code (e.g., JDBC, JPA).  
   - Spring Boot’s auto-configuration speeds up development.  

3. **Testability**  
   - DI makes unit testing easier (mock dependencies).  
   - `@SpringBootTest` simplifies integration testing.  

## **3. IoC & DI in Spring**  

### **Inversion of Control (IoC)**  
- **Framework-managed** object lifecycle (creation, wiring, destruction)  
- **Developer declares** beans (`@Component`, `@Bean`), **Spring Container** handles the rest  
- **Flip of control**: Framework calls your code (vs. you calling libraries)  

### **Dependency Injection (DI)**  
- **Dependencies provided externally** => No need to instantiate anymore
- **Primary types**:  
  - **Constructor injection** (✅ Preferred: immutable, testable)  
  - Setter injection  
  - Field injection (❌ Avoid: harder to test)  

### **Why It Matters**  
- **Loose coupling**: Classes depend on abstractions (interfaces), not concrete implementations  
- **Easy testing**: Mock dependencies via constructor args  
- **Modular design**: Swap implementations without code changes (e.g., `@Profile`)  
- **Cleaner code**: No `new` keyword littered everywhere  

### **Example**  
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

## **4. Bean Scopes**  
| Scope         | Description |  
|--------------|------------|  
| `singleton` (Default) | One instance per container. |  
| `prototype` | New instance per request. |  
| `request` | One per HTTP request (web). |  
| `session` | One per user session (web). |  

## **5. Configuration Styles**  
| Method          | Example |  
|----------------|---------|  
| **XML** | `<bean id="service" class="com.example.Service"/>` |  
| **Annotations** | `@Component`, `@Service`, `@Repository` |  
| **Java Config** | `@Configuration` + `@Bean` methods |  

---

---

# **💠 Spring Core**

Spring Core is the **central module** of the Spring Framework, providing the essential infrastructure for **dependency injection (DI)** and **Inversion of Control (IoC)**. At its heart is the **IoC Container**, which manages the lifecycle of Java objects (beans) and wires dependencies automatically.  

## 1. **Key Components**  
- **BeanFactory**: Basic container interface for bean instantiation and wiring.  
- **ApplicationContext**: Advanced container (extends `BeanFactory`) with additional features like:  
  - Internationalization (`MessageSource`)  
  - Event publication (`ApplicationEventPublisher`)  
  - Resource loading (`ResourceLoader`)  
- **Bean Scopes**: Controls bean lifecycle (`singleton`, `prototype`, request, session).  

## **2. Why It Matters**  
- **Decouples components** through DI (no hardcoded dependencies)  
- **Centralizes configuration** (XML, annotations, or Java config)  
- **Enables testability** via mockable dependencies  
- **Provides consistent API** to access resources and environment  

---
# **💠 Spring Boot**  

## **1. Auto-Configuration Magic**
- **Conditional Bean Loading**:  
  - Uses `@Conditional` variants (e.g., `@ConditionalOnClass`, `@ConditionalOnProperty`)  
  - Example: Auto-configures `DataSource` only if `spring.datasource.url` is set  
- **Custom Auto-Configuration**:  
  - Create `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`  
  - Use `@AutoConfiguration` + `@Conditional` for custom rules  

## **2. Starter Packs

Spring Boot uses **starter dependencies** to simplify configuration and speed up project setup. These **opinionated dependency bundles** automatically bring in everything needed for a particular use case, reducing the need for manual setup or XML-based configuration.

Here are some essential Spring Boot starters you’ll use across most projects:

| Starter                                                 | Purpose                                                                               |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **spring-boot-starter-web**                             | For building RESTful web applications using Spring MVC and embedded Tomcat.           |
| **spring-boot-starter-data-jpa**                        | Simplifies database access using Spring Data and Hibernate.                           |
| **spring-boot-starter-security**                        | Adds basic security setup with Spring Security (e.g., login form, password encoding). |
| **spring-boot-starter-test**                            | Includes JUnit, Mockito, Spring Test, and AssertJ for unit/integration testing.       |
| **spring-boot-starter-validation**                      | Adds support for bean validation (Hibernate Validator is the default).                |
| **spring-boot-starter-actuator**                        | Provides production-ready monitoring endpoints (health, metrics, env).                |

## **3. Embedded Servers**

**Tomcat** is brought by the **spring-boot-starter-web**.

| Server   | Default Port | Key Feature                 | Best For             |
| -------- | ------------ | --------------------------- | -------------------- |
| Tomcat   | 8080         | Servlet 5.0 (Jakarta EE 9+) | Traditional web apps |
| Jetty    | 8080         | Lightweight, async support  | Reactive/High-load   |
| Undertow | 8080         | Non-blocking, low memory    | Microservices        |

## **4. Actuator Endpoints**

| Endpoint   | Description                        | Security Consideration |     |
| ---------- | ---------------------------------- | ---------------------- | --- |
| `/health`  | App status (DB, disk space)        | Often exposed publicly |     |
| `/metrics` | JVM, HTTP stats (Prometheus-ready) | Restrict to admins     |     |
| `/env`     | All configuration properties       | Highly sensitive       |     |
| `/beans`   | List all Spring beans              | Debugging only         |     |


---

# **💠 Spring MVC & REST**  

## **1. Core Architecture**

### **Front Controller Pattern:**
- `DispatcherServlet` (Central controller)
  - Handles all HTTP requests
  - Delegates to controllers via `HandlerMapping`
  - Processes results via `ViewResolver`

### **Request Lifecycle:**
1. Request → DispatcherServlet
2. HandlerMapping selects controller
3. Controller processes request
4. Returns ModelAndView
5. ViewResolver renders response

## **2. Key Components**

| Component | Purpose | Annotation/Interface |
|-----------|---------|----------------------|
| Controller | Business logic | `@Controller`, `@RestController` |
| HandlerMapping | Route requests | `@RequestMapping` |
| ViewResolver | Renders views | `InternalResourceViewResolver` |
| Model | Carries data | `Model`, `ModelMap` |
| MessageConverter | Serialization | `HttpMessageConverter` |

## **3. REST Implementation**

### **Essential Annotations:**
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

### **Exception Handling:**
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

### **Validation:**
```java
@PostMapping("/users")
public User createUser(@Valid @RequestBody UserDto userDto) {
    // Automatically validates based on UserDto annotations
}
```

## **6. Performance Optimization**

1. **Caching:**
   ```java
   @GetMapping("/users/{id}")
   @Cacheable("users")
   public User getUser(@PathVariable Long id) {
       // Implementation
   }
   ```

2. **Pagination:**
   ```java
   @GetMapping("/users")
   public Page<User> getUsers(Pageable pageable) {
       return userService.findAll(pageable);
   }
   ```
   Request: `GET /users?page=0&size=20&sort=name,asc`

---

# **💠 Spring AOP (Aspect-Oriented Programming)**  

Spring AOP enables **modularization of cross-cutting concerns**—functionality that spans multiple layers of an application (e.g., logging, security, transactions). Unlike OOP, which organizes code into hierarchies, AOP **"weaves"** additional behavior into existing code **without modifying the original classes**.  

## 1. **Key Concepts**  
- **Aspect**: A module encapsulating cross-cutting logic (e.g., `LoggingAspect`).  
- **Advice**: The action taken by an aspect (e.g., `@Before`, `@After`, `@Around`).  
- **Pointcut**: A predicate defining where advice should be applied (e.g., `execution(* com.example.service.*.*(..))`).  
- **Join Point**: A specific point in execution (e.g., method invocation).  

## **2. Aspect**
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

## **3. Advice**
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

## **4. Pointcut**
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

## **5. Join Point**
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