---
cover: "[[java.jpg]]"
---
## 1. Core Java Concepts

### Object-Oriented Programming (OOP)

- **Encapsulation**: Group related data and methods within a class.
- **Inheritance**: Extend functionality by inheriting properties and methods from a parent class.
- **Polymorphism**: Use a single interface or method to represent different underlying forms.
- **Abstraction**: Focus on essential qualities of an entity by hiding implementation details.

### Primitive vs Reference Types

- **Primitive Types**: `int`, `double`, `char`, `boolean`, etc. (store values directly).
- **Reference Types**: `String`, custom objects, arrays, etc. (store references to objects in memory).

### Static vs Instance Members

- **Static**: Belong to the class itself (shared by all instances).
- **Instance**: Belong to specific objects created from a class.

### Exception Handling

- **Checked vs Unchecked Exceptions**: Checked exceptions must be declared or handled; unchecked are runtime exceptions.
- **try-catch-finally**: Primary mechanism to handle exceptions.
- **throws**: Declares an exception may be thrown.
- **throw**: Explicitly generates an exception in code.

### Annotations

- Provide metadata to the compiler or runtime.
- Common examples: `@Override`, `@FunctionalInterface`.

### Generics

- Use type parameters (`<T>`) for collections and methods to achieve type safety and reduce casts.

### Lambda Expressions & Functional Interfaces

- **Lambda Expressions**: Simplified syntax for implementing functional interfaces.
- **Functional Interfaces**: Single abstract method (SAM) interfaces (e.g., `Consumer<T>`, `Function<T,R>`, `Predicate<T>`, `Supplier<T>`).

### Records

- Introduced in Java 14 for creating concise, immutable data classes.

### Modules

- Introduced in Java 9 to improve encapsulation and manage package visibility across modules.

---

## 2. SOLID Principles

- **S (Single Responsibility)**: Each class should address only one concern.
- **O (Open/Closed)**: Classes should be extendable without modifying existing code.
- **L (Liskov Substitution)**: Subtypes must be interchangeable with their base types.
- **I (Interface Segregation)**: Provide small, client-specific interfaces rather than large, general-purpose ones.
- **D (Dependency Inversion)**: Depend on abstractions (interfaces), not on concrete implementations.

---

## 3. DRY (Don't Repeat Yourself)

- Avoid code duplication by extracting common functionality into methods, classes, or libraries.
- Employ abstraction and modularization to keep code clean and maintainable.

---

## 4. Equals and HashCode

### Equals

- Must satisfy **reflexivity**, **symmetry**, **transitivity**, and **consistency**.
- By default, `Object.equals()` compares memory addresses.
- Overridden `equals` methods should carefully check class types and field values.
- Best way to write an equals:
```java
private String s;
private float x;

public boolean equals(Object 0) {
	return o instanceof MyClass other &&
		other.x == this.x &&
		other.s.equals(this.s);
}
	```

### HashCode

- If you override `equals`, you must also override `hashCode`.
- Hash collisions are possible; design hash functions that minimize collisions.
- Tools like **EqualsVerifier** help ensure correct `equals` and `hashCode` implementations.

---

## 5. Collections & Streams

### Collections

- **List**: `ArrayList`, `LinkedList` (ordered, duplicates allowed).
- **Set**: `HashSet`, `TreeSet`, `LinkedHashSet` (no duplicates).
- **Map**: `HashMap`, `TreeMap`, `LinkedHashMap` (key-value pairs).
- **Queue**: `PriorityQueue`, `Deque` implementations.
- **Concurrent Collections**: `ConcurrentHashMap`, `CopyOnWriteArrayList`, etc.

### Streams API

- Offers functional-style operations (`map`, `filter`, `reduce`).
- Supports **parallel execution** for performance gains.
- Common collectors include `Collectors.toList()`, `Collectors.groupingBy()`.
- **Optional** type helps avoid `null` checks, providing safer alternatives with methods like `orElse()` and `orElseGet()`.

---

## 6. Multithreading

### Scheduling & Thread Management

- **First Come, First Serve (FCFS)** is a basic scheduling algorithm.
- Prefer **ExecutorService** over creating `Thread` objects directly:
    - **execute** (no return) and **submit** (returns a `Future`) for tasks.
    - **shutdown** and **awaitTermination** to manage graceful shutdown.

### Synchronization & Thread Safety

- Use **synchronized** for critical sections writing shared data.
- Use **volatile** for variables accessed across threads.
- Prefer **Atomic** classes (`AtomicInteger`, `AtomicBoolean`, etc.) over direct `volatile/synchronized`.

---

## 7. Memory Management

### JVM Memory Model

- **Heap**: Stores objects.
- **Stack**: Stores method calls and local variables.
- **Metaspace**: Stores class metadata (replaced PermGen in Java 8).
- **Native Memory**: Memory allocated outside the JVM.

### Garbage Collection (GC) Algorithms

- **Serial GC**: Simple, single-threaded.
- **Parallel GC**: Multi-threaded, default in many JVMs.
- **CMS**: Concurrent Mark-Sweep for low latency.
- **G1 GC**: Garbage First, well-suited for large heaps.
- **ZGC**: A low-latency, scalable GC.

### Tools for Memory Management

- **Heap Dump Analysis**: `jmap`, Eclipse Memory Analyzer.
- **Thread Dump Analysis**: `jstack`, VisualVM.
- **Profiling**: `JProfiler`, Java Flight Recorder (JFR), VisualVM.