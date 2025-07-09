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

## 1. Versions
- Latest is **Spring Framework 6.x**
- Released with **Spring Boot 3.x**

## 2. What is Spring?  
**Spring** is an open-source **Java framework** used for easily building **applications**. It promotes clean architecture with **loose coupling**, **modularity**, and **testability**.

- **Inversion of Control (IoC)** – The container controls object creation and lifecycle instead of the application code.
- **Dependency Injection (DI)** – Objects receive their dependencies from the container, not by creating them internally. This supports **loose coupling** and easier testing.

**Modules:**
- **Spring Core** - Provides fundamental features like IoC and DI.
- **Spring AOP (Aspect-Oriented Programming)** – Enables modular handling of behaviors that affect multiple classes.
- **Spring MVC** – Web framework based on Model-View-Controller design.
- **Spring Boot** – Auto-configures Spring applications to reduce boilerplate setup.
- **Spring Data** – Simplifies data access for relational and NoSQL databases.
- **Spring Security** – Manages authentication and authorization.  

## 3. IoC & DI in Spring  

#### **Inversion of Control (IoC)**  
- The **IoC container** manages the **lifecycle of objects (beans)** — including creation, wiring, and destruction.
- Developers define beans using annotations like `@Component`, `@Service`, or `@Bean`.
- The framework **injects dependencies** and controls execution flow — a reversal from traditional programming where you create and manage objects manually.
- In short: **Your code is called by the framework**, not the other way around.
#### **Dependency Injection (DI)**  
- **Dependencies are passed in by the container**, not created inside the class.
- Eliminates manual instantiation (`new`) and tight coupling.

#### **Why It Matters**  
- **Loose Coupling**
    - Classes depend on **interfaces or abstractions**, not concrete implementations.
- **Testability**
    - Easily inject **mock dependencies** in unit tests via constructor arguments.
- **Flexibility**
    - Swap implementations using features like `@Profile` or configuration changes — no code rewrites.
- **Cleaner, Maintainable Code**
    - Code is focused on **business logic**, not wiring objects or managing lifecycle manually.  

---

# **💠 Spring Core**

**Spring Core** is the foundational module of the Spring Framework. It provides the essential infrastructure for **Dependency Injection (DI)** and **Inversion of Control (IoC)**. 

The centerpiece is the **IoC Container**, which manages the lifecycle of objects (called **beans**) and automatically wires their dependencies.

## 1. **Key Components**  

- **BeanFactory**  
    The basic container interface responsible for **instantiating**, **configuring**, and **managing beans**.  
- **ApplicationContext**  
    An extension of `BeanFactory` that adds more enterprise-level features.
	Typically used in real-world applications.
- **Bean Scopes**  
	Define the lifecycle and visibility of beans in the container.

## 2. **Bean Scopes**  

| Scope                            | Description                 |
| -------------------------------- | --------------------------- |
| `singleton` (Default)            | One instance per container. |
| `prototype`                      | New instance per request.   |
| `request` *(only for SpringMVC)* | One per HTTP request (web). |
| `session` *(only for SpringMVC)* | One per user session (web). |


---
# **💠 Spring Boot**  

**Spring Boot** is an opinionated framework built on top of Spring that **simplifies application setup and development** by providing auto-configuration. It allows developers to create production-ready Spring applications with minimal configuration and no XML.

It build a **fat jar** (uber-jar): a single JAR file that contains:
- The application code
- All required dependencies
- An embedded server (e.g., Tomcat) if it's a web app
It doesn't contain the **JVM**.

It's latest version is **Spring Boot 3.x** which works with **Spring Framework 6.x**.

## 1. @SpringBootApplication

**`@SpringBootApplication`** is used to bootstrap the Spring Boot application. It annotates the **main class** of the project.
It enables auto-configuration and component scanning in the package and sub-packages.

It is a **combination** of the following annotations:

-  **`@Configuration`**
	- Marks a class as a **source of bean definitions** for the application context.    
	- Used to define beans via `@Bean` methods.
	
-  **`@EnableAutoConfiguration`**
	- Enables Spring Boot’s **auto-configuration** mechanism.
	- Automatically configures beans based on classpath, other beans, and property settings.

- **`@ComponentScan`**
	- Tells Spring where to look for **components**, **services**, **repositories**, and **controllers** to register as beans.
	- Automatically scans the package of the annotated class and sub-packages.

## 2. Starter Packs
**Starters** are curated sets of Maven/Gradle dependencies that provide a **ready-to-use setup** for common features (e.g., web, JPA, security).

They abstract away complex dependency management, making project setup fast and standardized.

| Starter                            | Purpose                                                                                   |
| ---------------------------------- | ----------------------------------------------------------------------------------------- |
| **spring-boot-starter-web**        | For building RESTful web applications using **Spring MVC** and embedded **Tomcat**.       |
| **spring-boot-starter-data-jpa**   | Simplifies database access using **Spring Data** and **Hibernate**.                       |
| **spring-boot-starter-security**   | Adds basic security setup with **Spring Security** (e.g., login form, password encoding). |
| **spring-boot-starter-test**       | Includes **JUnit, Mockito, Spring Test, and AssertJ** for unit/integration testing.       |
| **spring-boot-starter-validation** | Adds support for bean validation (**Hibernate Validator** is the default).                |
| **spring-boot-starter-actuator**   | Provides production-ready monitoring endpoints (**health**, **metrics**, **env**).        |

## 3. Parent POM
- Spring Boot provides a **parent POM** (`spring-boot-starter-parent`) that manages **dependency versions**, plugin configurations, and defaults.
- Using the parent POM avoids version conflicts and simplifies Maven configuration.
- It also includes settings for building executable jars and other best practices.

---

# **💠 Spring MVC & REST**  

## 1. Web Services
**Web Services** allow applications to communicate with each other over a network using standard protocols like **HTTP**.
They expose functionality or data to other systems through **APIs**.

## 2. Core Architecture
Spring MVC uses a single Servlet called **DispatcherServlet** to handle HTTP requests.

A **Servlet** is a **server-side Java component** that runs inside a **Servlet container** (like Tomcat) and acts as a **middle layer** between a client and the server.
#### Request Lifecycle:
1. **Client sends request** → Handled by `DispatcherServlet`.
2. **`HandlerMapping`** identifies appropriate controller method.
3. **Controller** processes logic and returns data (or view).
4. **`ViewResolver`** renders HTML (for MVC) or response body (for REST).

## 3. Annotations
- `@RestController`
    - Combines `@Controller` + `@ResponseBody`.
    - Returns **JSON or XML** (not a view).

- `@RequestMapping`
    - General-purpose mapping of URL + method (GET, POST, etc.).

- `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`
    - Shorthand annotations for RESTful HTTP verbs.

- `@PathVariable`
    - Binds URL path segments to method parameters.
    - Example: `/users/{id}` → `@PathVariable Long id`

- `@RequestParam`
    - Binds query parameters (e.g., `/search?q=abc`).

- `@RequestBody`
    - Automatically deserializes JSON/XML request into a Java object.

- `@ResponseBody`
    - Serializes method return value directly into the HTTP response.

- `@Valid`
	- Automatically validates request based on DTO annotations

## 4. Exception Handling
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

Or
```java
@ControllerAdvice
public class ExceptionConfiguration {

  @ResponseStatus(HttpStatus.CONFLICT)
  @ExceptionHandler(RuntimeException.class)
  public void handleConflict(63
  478
  ** e) throws RuntimeException {
      // Provide your general exception handling here
  }
}
```

## 5. Performance Optimization

1. **Caching with `Cacheable`:**
   ```java
   @GetMapping("/users/{id}")
   @Cacheable("users")
   public User getUser(@PathVariable Long id) {
       // Implementation
   }
   ```

2. **Pagination with `Pageable`:**
   ```java
   @GetMapping("/users")
   public Page<User> getUsers(Pageable pageable) {
       return userService.findAll(pageable);
   }
   ```
   Request: `GET /users?page=0&size=20&sort=name,asc`

3. **Threads and Virtual Threads:**
	- **Spring** uses **platform threads** for some use cases, such as Tomcat worker threads
	- With **Spring Boot** it is possible to enable **Virtual Threads** for **Spring MVC** which use less resources.

---

# **💠 Spring AOP (Aspect-Oriented Programming)**  

Spring AOP allows you to **modularize cross-cutting concerns** like logging, transactions, and security — adding behavior **without changing existing code**.

## **1. Core Concepts**
- **Aspect** – Class that contains cross-cutting logic (`@Aspect`)
- **Advice** – Code to run at specific points (e.g., `@Before`, `@Around`)
- **Pointcut** – Expression that selects where advice applies
- **Join Point** – A method execution where advice can run (Spring AOP only supports method-level join points)

## **2. Advice Types**

| Type              | Annotation    | When It Runs                     |
| ----------------- | ------------- | -------------------------------- |
| `@Before`         | Before method | Before execution                 |
| `@AfterReturning` | On success    | After method returns             |
| `@AfterThrowing`  | On exception  | If method throws                 |
| `@After`          | Always        | After method (finally)           |
| `@Around`         | Wraps method  | Controls before/after and result |

## **3. Pointcuts**

Used to define **where** advice applies. Common syntax:

```java
@Around("execution(* com.example.service.*.*(..))")
public void serviceMethods() {}
```
- `execution()` – Match method signatures
- `within()` – Match classes or packages
- `@annotation()` – Match based on annotations

## **4. Aspect Example**
```java
@Aspect
@Component
public class LoggingAspect {
    @Before("serviceMethods()")
    public void log(JoinPoint jp) {
        System.out.println("Called: " + jp.getSignature().getName());
    }
}

```


---

# 💠 **Testing**

Spring provides strong support for both **unit** and **integration testing**, making it easy to test application components in isolation or within a real runtime context.

## 1. Unit Tests
- Focused on **isolated components** (e.g., service, utility, controller logic).
- Should not rely on Spring context or external systems.
- Use **mocking** to simulate dependencies.
- Uses **JUnit** (`@Test`)
- Uses **Mockito**:
    - `@Mock` to create mock objects.
    - `@InjectMocks` to inject them into the class under test.
    - `when().thenReturn()` to define mock behavior.

## 2. Integration Tests
- **Integration testing** in Spring ensures that multiple components work **correctly together** within a **real runtime environment** (e.g., services + repositories + database).
- Unlike unit tests, integration tests load a **real or partial Spring context** and often interact with real infrastructure components.
- Use `@SpringBootTest` to load the full Spring context.
- Support embedded or containerized databases (e.g., **H2**, **PostgreSQL** via TestContainers)

## 3. TestContainers
- **Lightweight Docker containers** launched during tests.
- Ideal for **real external services** (e.g., PostgreSQL, Redis, Kafka).
- Works well with JUnit and Spring Boot.

## 4. End-to-End (E2E) Tests
- Simulate real user scenarios across the whole stack.
- Often use tools like **Selenium**.
- Helpful for validating controller behavior and web layer responses.
- Clean up data with:
	- `@Sql`: Run scripts before/after tests to **insert or delete data**.
	- `@Transactional`: Rolls back DB state after each test (not recommended).

## 5. Load and Stress Tests
- **Load Tests**: Simulate normal usage at expected scale, using **Gatling**.
- **Stress Tests**: Push system beyond limits to find failure thresholds.

## 6. TDD (Test Driven Development)
- **Write tests first** to , then implement just enough code to pass them.
- Cycle: **Test fails -> Write Code → Test passes → Refactor**
- Promotes better design, documentation, and confidence in code changes.
