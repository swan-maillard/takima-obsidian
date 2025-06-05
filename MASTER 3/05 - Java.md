---
cover: "[[java.jpg]]"
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

# 💠 Core Java Concepts

## 1. Main Versions
- Last version: **24**
- LTS: **11**, **17**, **21**

## 2. Object-Oriented Programming (OOP)
OOP is a **programming paradigm** based on objects, which represents concepts.
Based on 4 main principles:

- **Encapsulation**: **Group** related data and **intern logic / components** => **Control the visibility / access** => Generalize behavior

- **Inheritance**: Extend functionality by inheriting properties and methods from a parent class =>  **Specialize behavior** => **Avoids code duplication**

- **Polymorphism**: Use objects of different classes but derived from a same class uniformly => **Overloading** / **Overriding** / **Genericity** => **Avoid code duplication**

- **Abstraction**: Focus on essential qualities of an entity by **hiding implementation details** => Defines a **contract** hiding the complexity, useful with several implementations

## 3. JVM (Java Virtual Machine)
- **Compiles** source code into **bytecode**
- **Bytecode** is a platform-independent, intermediate representation
- The **JVM** interprets or compiles bytecode at runtime on any system with a compatible JVM
- This enables **cross-platform** compatibility:  
    → _"Write once, run anywhere"_—the same bytecode runs on Windows, macOS, Linux, etc.
- JVM handles **memory management
- Includes a **Garbage Collector** to automatically reclaim unused memory

## 3. Exception Handling
- **Checked vs Unchecked Exceptions**:
    - _Checked_: Must be declared or handled explicitly.
    - _Unchecked_: Runtime exceptions that do not require explicit handling.
- **try-with-resources**: Automates closing of resources (implementing `AutoCloseable`), preventing resource leaks.

---

# 💠 SOLID and DRY Principles

## 1. SOLID
=> Important principle of OOP  -> Best practices, improves maintainability

- **S (Single Responsibility)**: A class should have only one reason to change.
- **O (Open/Closed)**: Classes are open for extension but closed for modification.
- **L (Liskov Substitution)**: objects of a superclass should be able to be replaced with objects of a subclass without affecting the correctness of the program => **Parent class can be replaced by child**
- **I (Interface Segregation)**: Provide small, client-specific interfaces rather than large, general-purpose ones.
- **D (Dependency Inversion)**: Depend on abstractions, not on concrete implementations.

## 2. DRY (Don't Repeat Yourself)
- Avoid code duplication by extracting common functionality into methods, classes, or libraries.
- Employ abstraction and modularization to keep code clean and maintainable.

---

# 💠 Equals and HashCode

## 1. Contract
- If 2 objects are **equals** then they have the **same hash code**
- If 2 objects have the **same hash code** they are **not necessarily equals**
- Failing to override both methods consistently can cause **unexpected behavior** in hash-based collections (e.g., a `HashMap` may not find a key that exists).

## 1. Equals
- By default, `Object.equals()` compares memory addresses.
- When overriding `equals`, ensure you properly compare field values and check type compatibility.
## 2. HashCode
- By default, `Object.hashCode()` hashes memory address.
- It is used in **hash-based collections** like `HashMap`, `HashSet`, and `Hashtable` to determine the **bucket location** for storing objects.
- **Hash collisions** are possible, so aim for a balanced hash function to minimize collisions.


---

# 💠 Collections
## 1. List

- **Purpose**: Ordered collection that allows duplicates.
- **Common Implementations**:
    - `ArrayList`: Backed by a dynamic array. Provides fast random access (amortized O(1) for `get`, O(1) average for adding at the end). Insertions/removals in the middle can be costly (O(n)).
    - `LinkedList`: Uses a doubly-linked list. Offers faster insertions/removals at the ends (O(1)) but slower random access (O(n) for `get`).
## 2. Set

- **Purpose**: Collection that disallows duplicate elements.
- **Common Implementations**:
    - `HashSet`: Backed by a hash table. Offers average O(1) insertion, removal, and lookup. Elements are not stored in any particular order.
    - `LinkedHashSet`: Preserves insertion order of elements. Slightly higher overhead than `HashSet` due to maintaining a doubly-linked list of entries.
    - `TreeSet`: Backed by a Red-Black tree. Stores elements in a sorted order. Operations like insertion, removal, and lookup run in O(log n) time.
## 3. Queue

- **Purpose**: FIFO (First-In-First-Out) or specialized ordering of elements.
- **Common Implementations**:
    - `PriorityQueue`: Orders elements based on their natural ordering or a custom `Comparator`. Insertion is O(log n), and retrieval of the highest/lowest priority element is O(log n).
    - `ArrayDeque` (a type of `Deque`): Can function as a stack (LIFO) or a queue (FIFO). Provides O(1) amortized insertion/removal from both ends.

---

# 💠 Map

⚠ Maps are **NOT** Collections

- **Purpose**: Key-value pair storage with fast lookups by key.
- **Common Implementations**:
    - `HashMap`: Backed by a hash table. Average O(1) insertion and lookup. No ordering guarantees on keys.
    - `LinkedHashMap`: Maintains a doubly-linked list of the entries, preserving insertion order (or access order, if configured). Slightly higher overhead than `HashMap`.
    - `TreeMap`: Backed by a Red-Black tree. Keys are stored in a sorted order. Insertion, removal, and lookup run in O(log n) time.

---

# 💠 Streams API

## 1. Creating a Stream
- From a **Collection**: `collection.stream()` or `collection.parallelStream()`
- From **arrays**: `Arrays.stream(array)`
- Via **static methods**: `Stream.of(...)`, `Stream.generate(...)`, `Stream.iterate(...)`

## 2. Intermediate Operations

These operations return a new `Stream` and are lazily evaluated. Examples include:

- `map(Function)`: Transforms each element to another object.
- `filter(Predicate)`: Keeps only elements that match a condition.
- `sorted() / sorted(Comparator)`: Sorts the stream’s elements.
- `distinct()`: Removes duplicate elements based on `equals()`.
- `limit(long n)` / `skip(long n)`: Truncates or advances the stream.

No actual processing takes place until a **terminal operation** is invoked.

## 3. Terminal Operations

These operations trigger the _evaluation_ of the stream and typically produce a result or side-effect. Examples include:

- `collect(Collector)`: Accumulates elements into a collection, such as via `Collectors.toList()`.
- `forEach(Consumer)`: Executes a block of code for each element.
- `reduce(BinaryOperator)`: Accumulates elements into a single value (e.g., sum).
- `count()`: Returns the number of elements in the stream.
- `findFirst()`, `findAny()`: Retrieves an element from the stream that matches a condition (if any).

## 4. Parallel Streams

- Using `parallelStream()` (or `stream().parallel()`) can leverage multiple CPU cores.
- **Caution**: Parallel performance gains are not guaranteed. Always measure. Avoid shared mutable state, as it can cause concurrency issues or degrade performance if synchronization is required.

## 5. Common Collectors

- **`Collectors.toList()`**: Gathers stream elements into a `List`.
- **`Collectors.toSet()`**: Gathers stream elements into a `Set` (duplicates discarded).
- **`Collectors.groupingBy(Function)`**: Groups stream elements into a `Map<K, List<V>>`.
- **`Collectors.joining(String delimiter)`**: Concatenates string representations of the elements using a given delimiter.

## 6. Optional

`Optional<T>` is a container object that may or may not contain a non-null value. It helps reduce `NullPointerException` by forcing the caller to explicitly deal with the possibility of an absent value.

---

# 💠 Multithreading

## 1. Scheduling & Thread Management

### The Executor Framework
Java’s `java.util.concurrent` package provides high-level abstractions for managing tasks:

1. **ExecutorService**
    - A higher-level API for managing thread pools and task execution.
    - You submit **tasks** (either as `Runnable` or `Callable<V>`) and let the framework handle scheduling and thread allocation.
    
2. **Thread Pools**
    - **FixedThreadPool**: A fixed number of threads. Once all threads are busy, new tasks wait in a queue until a thread is free.
    - **CachedThreadPool**: Dynamically creates threads as needed and reuses existing ones when available.
    - **ScheduledThreadPool**: Schedules tasks to run after a delay or repeatedly at fixed intervals.
    - **WorkStealingPool** (Java 8+): Uses a fork-join pool internally for parallelism.

### Submitting Tasks
- **execute(Runnable task)**: Submits a `Runnable` with no return value.
- **submit(Callable task)**: Submits a `Callable` that returns a `Future<V>`; the `Future` can be used to check task status, retrieve results, or handle exceptions.

### Handling Exceptions & Futures
When using `submit(...)`, any exception in the `Callable` is captured and can be re-thrown when calling `future.get()`. This approach makes it simpler to handle and log errors that occur in separate threads.

## 2. Synchronization & Thread Safety

When multiple threads share mutable state, conflicts can arise if updates or reads happen at the same time. Java provides several mechanisms to coordinate access and ensure data integrity.

### Synchronized
- Placing the `synchronized` keyword on a method or block ensures only one thread can enter that section at a time, effectively serializing access to the critical section.
    ```java
    public synchronized void increment() {
        count++;
    }
    ```
> :LiAlertTriangle: ***Drawback**: Synchronization can cause contention, reducing parallelism.*

### Volatile
- Declaring a variable as `volatile` ensures visibility of changes to that variable across threads; every read sees the latest write.
    ```java
    private volatile boolean running = true;
    ```
> :LiAlertTriangle: ***Caution**: `volatile` does **not** provide atomicity; it only guarantees that updates are immediately visible to other threads. Complex operations (like `count++`) are not inherently thread-safe.*

### Atomic Classes
- **`AtomicInteger`, `AtomicBoolean`, `AtomicReference`**, etc., offer thread-safe operations on single variables without using locks.
    ```java
    private AtomicInteger count = new AtomicInteger(0);
    
    public void increment() {
        count.incrementAndGet(); // an atomic operation
    }
    ```
- Atomic classes can perform compound actions (e.g., compare-and-swap) atomically, which may be more efficient than using `synchronized` for single-variable operations.

---

# 💠 Config and Maven

## 1. pom.xml

The `pom.xml` (Project Object Model) file is the core of a Maven project. It contains:

- **GroupId**: Typically corresponds to the base package (e.g., `com.example`).
- **ArtifactId**: Unique name of the project/artifact (e.g., `my-app`).
- **Version**: Identifies the specific project version (e.g., `1.0.0-SNAPSHOT`).
- **Dependencies**: External libraries and frameworks required at compile time or runtime.
- **Plugins**: Tools to perform tasks like code coverage, packaging, or code analysis.
- **Repositories**: Defines where Maven will look for dependencies (e.g., Maven Central).

## 2. Version Properties

Using **properties** in the `pom.xml` allows you to avoid repeating version numbers for dependencies or plugins. This approach makes upgrades easier because you only need to update a single property in the `<properties>` section:

```xml
<properties>
    <spring.boot.version>3.0.0</spring.boot.version>
</properties>
```

Then reference them in dependencies:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>${spring.boot.version}</version>
</dependency>
```

This ensures version consistency and centralizes version management.

## 3. Dependency Scopes

Maven defines several **scopes** that control the classpath and visibility of a dependency throughout different phases of the build lifecycle:

1. **compile**
    - **Default scope** if none is specified.
    - Dependencies are available in all phases (compiling, testing, and running the project) - packaged into artifact.
2. **runtime**
    - Dependencies not required for compilation but needed at runtime.
    - They are included in the runtime or packaged artifact but not on the compile classpath.
3. **test**
    - Dependencies only used for compiling and running tests, not included in the final artifact or runtime outside tests.
4. **provided**
    - Similar to `compile`, but the dependency is assumed to be provided by the environment (e.g., a servlet container) - not included in artifact.
5. **system**
	- Similar to `provided`, but you explicitly define a local path on your file syste.
6. **import**
    - Used when importing dependency **management** from another POM.
    
## 4. Common Maven Commands

These are some frequently used Maven goals:
1. **mvn compile**  
    Compiles your main source code and places compiled `.class` files in `target/classes`.
2. **mvn test**  
    Executes your unit tests, typically found in `src/test/java`, using frameworks like JUnit.
3. **mvn package**  
    Packages your compiled code into a distribution format, such as a `.jar` or `.war` file, placed in `target/`.
4. **mvn install**  
    Installs the packaged artifact into your local Maven repository (`~/.m2/repository`), making it available for other local projects.
5. **mvn clean**  
    Deletes the `target/` directory, removing all previously compiled artifacts.
6. **mvn clean package**  
    Combines `clean` and `package` in one step, ensuring a fresh build.
7. **mvn dependency:tree**  
    Prints the dependency tree, helping you detect clashes in transitive dependencies or version conflicts.


---

# 💠 JVM

**JVM** is a **Virtual Machine** able to run compiled bytecode of langages such as **Java**, **Kotlin** or **Scala** (Example of JVM: **GraalVM** with good opti, **Hotspot (Oracle)** by default)

## 1. JVM Memory Model
When you run a Java application, the JVM divides its memory into distinct areas, each with a specific purpose:

1. **Heap**
    - Stores dynamically allocated objects and arrays.
    - Managed by GC, when no more reference from the stack OR cyclic references.
    - Largest memory region (80%)
2. **Stack**
    - Holds stack frames for each thread, containing local variables, method parameters, and references to objects on the heap.
3. **Metaspace**
    - Stores class metadata (such as class structures, methods, and constant pools).


## 2. Garbage Collection (GC) Algorithms
Garbage collection automatically frees memory by removing objects no longer reachable by active references. 

1. **CMS (Concurrent Mark-Sweep)**
	- Introduced at the **begining**
	- Depreciated in **Java 9**
    - **How it works**: New objects are placed in **Eden**, then are placed into **Survivor space**, then into **Old Generation** and is then cleaned by the CMS GC

2. **G1 GC
    - Introduced in **Java 7/8**
    - Depreciated in **Java 14**
 3. **ZGC**
	 - Introduced in **Java 11/15**


---

# 💠 Differences with Kotlin

## 1. Versions
| Feature             | Java                    | Kotlin                |
| ------------------- | ----------------------- | --------------------- |
| Initial Release     | 1995                    | 2011                  |
| Current LTS Version | Java 17 / Java 21 (LTS) | Kotlin 2.0+           |
| Developed by        | Oracle                  | JetBrains             |

## 2. Key Differences
- **Null Safety**  
	- Java allows `null` by default, which often leads to `NullPointerException` (NPE).  
    - Kotlin avoids this by making `null` handling **explicit**—you must declare a variable nullable using `?` and handle it safely.

- **Data Classes**  
    - Kotlin provides `data class` which **automatically generates** simple data-holding class with minimal code.

- **Syntax and Conciseness**  
    - Java tends to be more verbose due to its boilerplate-heavy syntax.  
    - Kotlin is designed to be **concise and expressive**, reducing the amount of code you write (e.g., no need for semicolons, simple getters/setters).

- **Extension Functions**  .  
    - Kotlin allows you to write **extension functions** that behave like native methods on existing classes.

- **Coroutines for Concurrency**  
    - Java uses threads, executors, and external libraries (like `CompletableFuture`) for concurrency.  
    - Kotlin has **built-in coroutines**, which offer a **lightweight and simpler** approach to asynchronous programming.

- **Checked Exceptions**  
    - Java forces you to handle or declare **checked exceptions**, which can lead to verbose code.  
    - Kotlin does **not have checked exceptions**, simplifying error handling but requiring more discipline.

- **Default and Named Arguments**  
    - Kotlin supports **default arguments** and **named parameters**, which simplifies function calls.

- **Functional Programming Support**  
    - Java added lambdas and streams in Java 8, but functional features are still limited.  
    - Kotlin was designed with **functional programming in mind**, offering features like higher-order functions, `map`, `filter`, `fold`, etc.
    
- **Interoperability with Java**  
    - Kotlin is **100% interoperable** with Java—existing Java libraries and frameworks work seamlessly.  