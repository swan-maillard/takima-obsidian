---
cover: "[[spring.png]]"
---

# TODO
- Explain Profiles (for example, having several implementations, configs, etc)
- Explain Tomcat, threads in memory, reactive programming
- AOP, custom aspects, custom annotations

## 1. Core Concepts

### Inversion of Control (IoC) & Dependency Injection (DI)
- **IoC Container**: The Spring container manages the lifecycle of objects (beans) so that developers can rely on the framework for object creation, configuration, and management.
- **Dependency Injection**: Objects are provided with their dependencies, reducing tight coupling and improving testability.

### Spring Beans
- **Bean Definition**: A bean is any object that the Spring container manages. Beans are defined using XML configuration, annotations, or Java-based configuration.
- **Scopes**: Common scopes include `singleton` (one instance per container), `prototype` (new instance every time), and web-specific scopes like `request` or `session`.

### Configuration Approaches
1. **XML-Based Configuration**: Traditional, verbose, but still used in some legacy projects.
2. **Annotation-Based Configuration**: Uses `@Component`, `@Service`, `@Repository`, `@Controller`, etc. to mark classes as beans.
3. **Java-Based Configuration**: Uses `@Configuration` classes and `@Bean` methods to define beans programmatically.

---

## 2. Spring Modules & Projects

### Spring Core
- The foundational module providing IoC and DI features.

### Spring AOP (Aspect-Oriented Programming)
- Allows separation of cross-cutting concerns (e.g., logging, security).
- Key annotations include `@Aspect`, `@Around`, `@Before`, `@AfterReturning`, etc.

### Spring MVC
- Web framework using the Model-View-Controller pattern.
- Simplifies the creation of RESTful or traditional MVC applications.
- Commonly annotated classes and methods with `@Controller`, `@RestController`, `@RequestMapping`, etc.

### Spring Boot
- Opinionated approach to Spring application development.
- Provides **starter** dependencies and auto-configuration to reduce setup and configuration boilerplate.
- Includes an embedded server (Tomcat, Jetty, or Undertow), so you can run web apps quickly.

### Spring Data
- Simplifies data access across various data stores (relational databases, NoSQL, etc.).
- `Spring Data JPA` reduces boilerplate by providing repositories with CRUD functionality out of the box.

### Spring Security
- Provides robust security features for authentication and authorization.
- Supports common scenarios like form-based login, OAuth2, JWT, and method-level security.

### Spring Cloud
- Provides tools for building cloud-native applications and microservices.
- Features include service discovery, configuration management, circuit breakers, and more.

---

## 3. Key Annotations

1. **@Bean**
    - Marks a method that returns a bean to be managed by Spring.
    - A bean is by default a **singleton**.
    
2. **@Configuration**
    - Indicates a class contains bean definitions.
    
3. **@Component** / **@Service** / **@Repository** / **@Controller**
    - Marks a class as a candidate for component scanning and DI.
    
4. **@Autowired** / **@Inject**
    - Injects bean dependencies. Works on constructors, setters, or fields.
    - Prefer using it on **constructors**.
    
5. **@Qualifier**
    - Distinguishes between multiple beans of the same type.

6. **@Scope**
    - Defines the scope of a bean (e.g., `singleton`, `prototype`).
    
7. **@RestController** / **@RequestMapping** / **@GetMapping** / **@PostMapping**
    - Spring MVC/REST annotations to simplify URL routing and handling HTTP requests.
    
8. **@EnableAutoConfiguration** (Spring Boot)
    - Triggers auto-configuration of the Spring ApplicationContext.
    
9. **@SpringBootApplication** (Spring Boot)
    - Combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan` for convenience.

---

## 4. Spring Boot Essentials

- **Spring Initializr**: Web-based tool to quickly generate pre-configured Spring Boot projects.
- **Auto-Configuration**: Automatically configures beans based on classpath settings and property files.
- **Application Properties**: Centralizes settings in `application.properties` or `application.yml`.
- **Embedded Servers**: Eliminates the need to deploy WAR files manually; run applications directly with `java -jar`.

---

## 5. Testing with Spring

- **Spring Test Context**: Integrates with JUnit/TestNG to load and run tests with a Spring application context.
- **MockMVC**: Allows testing of Spring MVC controllers without needing to run on a server.
- **@SpringBootTest**: Provides a convenient way to load the entire Spring context for integration tests.

---

## 6. Microservices & Cloud-Native Development

- **Spring Boot** and **Spring Cloud** together offer solutions for:
    - Configuration management with **Spring Cloud Config**.
    - Service discovery with **Eureka**.
    - Intelligent routing with **Zuul** or **Spring Cloud Gateway**.
    - Distributed tracing with **Sleuth** and **Zipkin**.
    - Resilience patterns (circuit breakers, fallback methods) using **Hystrix** or **Resilience4j**

---

## 7. Best Practices & Patterns

1. **Use Constructor Injection**
    - Promotes immutability, makes testing easier.
    
2. **Keep Configuration External**
    - Rely on `application.yml`, environment variables, or config servers rather than hardcoding values.
    
3. **Packaged Architecture**
    - **Packages per-layers:** Separate business logic (service layer), data access (repository layer), and presentation (controller layer) for small project.
    - **Packages per-features:** Separate per features for large projects.
    
4. **Avoid God Classes**
    - Adhere to **SOLID** principles. Keep classes focused on single responsibilities.
    
5. **Monitor & Observe**
    - Use tools like **Spring Boot Actuator** to monitor application health and metrics.
