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

**Compiled** in bytecode => **Interpreted** by JVM 
	=> **CROSS-PLATFORM**
	=> Handles memory
	=> Garbage Collector

## 1. Object-Oriented Programming (OOP)

- **Encapsulation**: **Group** related data and **intern logic / components** => **Control the visibility / access** => Generalize behavior
- **Inheritance**: Extend functionality by inheriting properties and methods from a parent class => **Generalize behavior** => **Specialize behavior**
- **Polymorphism**: Redefining behavior of a method => **Overloading** / **Overriding** / **Genericity** => Main interest is **Re-usability of code / Avoid duplication**
- **Abstraction**: Focus on essential qualities of an entity by hiding implementation details => Defines a **contract** hiding the complexity, useful with several implementations

## 2. Primitive vs Reference Types

- **Primitive Types**: `int`, `double`, `char`, `boolean`, etc. (store values directly).
- **Reference Types**: `String`, custom objects, arrays, etc. (store references to objects in memory and can be `null`).

## 3. Static vs Instance Members

- **Static**: Belong to the class itself (shared by all instances).
- **Instance**: Belong to specific objects created from a class.

## 4. Exception Handling

- **Checked vs Unchecked Exceptions**:
    - _Checked_: Must be declared or handled explicitly.
    - _Unchecked_: Runtime exceptions that do not require explicit handling.
- **try-catch-finally**: Primary mechanism to catch and handle exceptions.
- **try-with-resources**: Automates closing of resources (implementing `AutoCloseable`), preventing resource leaks.
- **throws**: Declares an exception may be thrown by a method.
- **throw**: Explicitly generates an exception in code.
## 5. Generics

- Use type parameters (`<T>`) for collections and methods to achieve type safety and reduce casts.

## 6. Lambda Expressions & Functional Interfaces

- **Lambda Expressions**: Simplified syntax for implementing single-abstract-method interfaces.
- **Functional Interfaces**: Interfaces with exactly one abstract method (e.g., `Consumer<T>`, `Function<T,R>`, `Predicate<T>`, `Supplier<T>`).

---

# 💠 SOLID and DRY Principles

## 1. SOLID
=> Important principle of OOP  -> Best practices, improves maintainability

- **S (Single Responsibility)**: A class should have only one reason to change.
- **O (Open/Closed)**: Classes are open for extension but closed for modification.
- **L (Liskov Substitution)**: Subtypes should be interchangeable with their base types without altering correctness => **Parent class can be replaced by child**
- **I (Interface Segregation)**: Provide small, client-specific interfaces rather than large, general-purpose ones.
- **D (Dependency Inversion)**: Depend on abstractions, not on concrete implementations.

## 2. DRY (Don't Repeat Yourself)

- Avoid code duplication by extracting common functionality into methods, classes, or libraries.
- Employ abstraction and modularization to keep code clean and maintainable.

---

# 💠 Equals and HashCode

## 1. Equals

- Must satisfy **reflexivity**, **symmetry**, **transitivity**, and **consistency**.
- By default, `Object.equals()` compares memory addresses.
- When overriding `equals`, ensure you properly compare field values and check type compatibility.
- Example:
    
    ```java
    public class MyClass {
        private String s;
        private float x;
    
        @Override
        public boolean equals(Object o) {
            return o instanceof MyClass other
                    && other.x == this.x
                    && other.s.equals(this.s);
        }
    }
    ```
    

## 2. HashCode

- If you override `equals`, you must also override `hashCode`.
- Hash collisions are possible, so aim for a balanced hash function to minimize collisions.
- Tools like **EqualsVerifier** help ensure correct implementations.

---

# 💠 Collections
## 1. List

- **Purpose**: Ordered collection that allows duplicates.
- **Common Implementations**:
    - `ArrayList`: Backed by a dynamic array. Provides fast random access (amortized O(1) for `get`, O(1) average for adding at the end). Insertions/removals in the middle can be costly (O(n)).
    - `LinkedList`: Uses a doubly-linked list. Offers faster insertions/removals at the ends (O(1)) but slower random access (O(n) for `get`).
- **Use Cases**:
	- `ArrayList` is typically preferred for most scenarios where random access is common.
	- `LinkedList` can be beneficial if you frequently insert or remove elements at the beginning or middle, and random access is less common.

## 2. Set

- **Purpose**: Collection that disallows duplicate elements.
- **Common Implementations**:
    - `HashSet`: Backed by a hash table. Offers average O(1) insertion, removal, and lookup. Elements are not stored in any particular order.
    - `LinkedHashSet`: Preserves insertion order of elements. Slightly higher overhead than `HashSet` due to maintaining a doubly-linked list of entries.
    - `TreeSet`: Backed by a Red-Black tree. Stores elements in a sorted order. Operations like insertion, removal, and lookup run in O(log n) time.
- **Use Cases**:
	- Use `HashSet` when fast insertion and lookup are needed, and order does not matter.
	- Use `LinkedHashSet` when you need to preserve the order in which elements were inserted.
	- Use `TreeSet` when you need a sorted set or if you need to quickly retrieve elements in ascending or descending order.

## 4. Queue

- **Purpose**: FIFO (First-In-First-Out) or specialized ordering of elements.
- **Common Implementations**:
    - `PriorityQueue`: Orders elements based on their natural ordering or a custom `Comparator`. Insertion is O(log n), and retrieval of the highest/lowest priority element is O(log n).
    - `ArrayDeque` (a type of `Deque`): Can function as a stack (LIFO) or a queue (FIFO). Provides O(1) amortized insertion/removal from both ends.
- **Use Cases**:
	- Use `PriorityQueue` when elements need to be processed based on priority instead of pure insertion order.
	- Use `ArrayDeque` for stack-like (LIFO) or queue-like (FIFO) operations with minimal overhead.

## 5. Concurrent Collections

- **Purpose**: Thread-safe collections designed for concurrency.
- **Common Implementations**:
    - `ConcurrentHashMap`: Allows concurrent read/write operations without explicit synchronization in most cases. Threads can safely update different parts of the map.
    - `CopyOnWriteArrayList`: An array-backed list that creates a fresh copy of the underlying array upon each modification. Ideal for mostly-read scenarios with few writes.
- **Use Cases**:
	- Use `ConcurrentHashMap` when multiple threads need simultaneous read/write access to a shared map.
	- Use `CopyOnWriteArrayList` in highly concurrent environments when reads vastly outnumber writes (like maintaining a list of listeners).

---

# 💠 Map

⚠ Maps are **NOT** Collections

- **Purpose**: Key-value pair storage with fast lookups by key.
- **Common Implementations**:
    - `HashMap`: Backed by a hash table. Average O(1) insertion and lookup. No ordering guarantees on keys.
    - `LinkedHashMap`: Maintains a doubly-linked list of the entries, preserving insertion order (or access order, if configured). Slightly higher overhead than `HashMap`.
    - `TreeMap`: Backed by a Red-Black tree. Keys are stored in a sorted order. Insertion, removal, and lookup run in O(log n) time.
- **Use Cases**:
	- `HashMap` is typically preferred for general-purpose key-value storage with fast lookups.
	- `LinkedHashMap` is useful if you need to iterate keys/values in insertion order (for example, in caching scenarios).
	- `TreeMap` is ideal when you need to iterate over keys in sorted order or quickly fetch subsets of keys (e.g., in a range).

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

Key methods:
- `Optional.of(value)`: Creates an `Optional` for a non-null value.
- `Optional.empty()`: Represents a missing value.
- `orElse(T other)`: Returns the contained value or `other` if empty.
- `orElseGet(Supplier<? extends T> supplier)`: Lazily supplies an alternate value if empty.
- `orElseThrow(Supplier<? extends Throwable> exceptionSupplier)`: Throws the provided exception if empty.
- `map(Function)`, `flatMap(Function)`: Transforms the contained value if present.
- `filter(Predicate)`: Returns an `Optional` describing the value if it matches, otherwise empty.

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

### Graceful Shutdown
- **shutdown()**: Initiates an orderly shutdown where new tasks are not accepted, but previously submitted tasks are allowed to complete.
- **shutdownNow()**: Attempts to stop all actively executing tasks and halts the processing of waiting tasks.
- **awaitTermination(long timeout, TimeUnit unit)**: Blocks until all tasks have completed execution after a shutdown request, or the timeout occurs, or the current thread is interrupted—whichever happens first.

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

### Best Practices
1. **Identify Shared Mutable State**: Whenever threads access and modify the same objects, you need a strategy (locks, atomics, etc.) to prevent race conditions.
2. **Minimize Lock Scope**: Keep synchronized sections as small as possible to reduce contention.
3. **Use Thread-Safe Collections**: Java provides concurrent variants (e.g., `ConcurrentHashMap`, `CopyOnWriteArrayList`) that handle synchronization internally.
4. **Avoid Unnecessary Synchronization**: Overuse can lead to performance bottlenecks and deadlocks.
5. **Prefer Higher-Level Abstractions**: Whenever possible, use the concurrency utilities (`ExecutorService`, concurrent collections, etc.) instead of manual thread manipulation.

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

# 💠 Memory Management

**JVM** is a **Virtual Machine** able to run compiled bytecode of langages such as **Java**, **Kotlin** or **Scala** (Example of JVM: **GraalVM** with good opti, **Hotspot** by default)

## 1. JVM Memory Model

When you run a Java application, the JVM divides its memory into distinct areas, each with a specific purpose:

1. **Heap**
    - **Purpose**: Stores dynamically allocated objects and arrays.
    - **Characteristics**:
        - Every new object in Java is allocated on the heap (unless it’s optimized away via escape analysis).
        - Managed by the GC, which deallocates objects that are no longer reachable by any thread.
        - The largest memory region in most JVM configurations.
2. **Stack**
    - **Purpose**: Holds stack frames for each thread, containing local variables, method parameters, and references to objects on the heap.
    - **Characteristics**:
        - Each thread has its own stack, so data on one thread’s stack is not visible to other threads.
        - Automatically allocated and freed as methods are invoked and return.
        - Size is typically fixed or can be configured. If the stack exceeds its limit, you may encounter a `StackOverflowError`.
3. **Metaspace**
    - **Purpose**: Stores class metadata (such as class structures, methods, and constant pools).
    - **Characteristics**:
        - Class loading/unloading affects Metaspace usage.
        - Mismanagement (e.g., loading too many classes) can lead to memory leaks in Metaspace.
4. **Native Memory**
    - **Purpose**: Memory allocated outside the JVM heap for lower-level resources, such as direct byte buffers, or by native libraries (e.g., JNI calls).
    - **Characteristics**:
        - Not governed by the Java GC.
        - Must be carefully managed when using native code or libraries that allocate memory off-heap.

## 2. Garbage Collection (GC) Algorithms

Garbage collection automatically frees memory by removing objects no longer reachable by active references. Different GC algorithms have different trade-offs in terms of throughput, latency, and memory footprint:

1. **Serial GC**
    - **How it works**: Uses a single thread for all GC tasks.
    - **Pros**: Simple, with minimal overhead and works well with small heaps (few hundred MB).
    - **Cons**: Application is paused during GC; not ideal for larger heaps or multi-core systems.
    
2. **Parallel GC**
    - **How it works**: Multiple threads perform the collection in parallel, typically reducing total GC time.
    - **Pros**: Higher throughput because more CPU cores can be used for GC.
    - **Cons**: Can still introduce noticeable pause times, although usually shorter than Serial GC.
    
3. **CMS (Concurrent Mark-Sweep)**
    - **How it works**: Performs most of its GC work concurrently with the application, aiming to reduce long pauses.
    - **Pros**: Good for applications needing low latency.
    - **Cons**: More CPU overhead to track concurrent activity. It might leave some memory fragments (because it’s a mark-sweep), and it can still have “stop-the-world” phases for final remark or cleanup.

4. **G1 GC (Garbage First)**
    - **How it works**: Splits the heap into regions and collects them incrementally, focusing on regions with the most garbage first.
    - **Pros**: Designed for large heaps and aims for predictable, short pause times.
    - **Cons**: More complex tuning parameters, though defaults often work well for many applications.

## 3. Tools for Memory Management

Diagnosing memory issues and performance bottlenecks often involves gathering data about how your application uses the heap, threads, and CPU resources. Java provides several powerful tools for these tasks:

1. **Heap Dump Analysis**
    - **`jmap`**: Command-line utility for generating heap dumps of a running JVM.
        ```bash
        jmap -dump:live,file=heapdump.hprof <PID>
        ```

2. **Thread Dump Analysis**
    - **`jstack`**: Command-line tool that prints the stack traces of all threads in a JVM. Helpful for diagnosing deadlocks or identifying performance bottlenecks in thread execution.
        ```bash
        jstack <PID> > threaddump.txt
        ```
    - **VisualVM**: A graphical tool (included in most JDK distributions) to inspect the current thread states, CPU usage, and memory usage in real time.

3. **Profilers**
    - **JProfiler**: A commercial tool offering powerful CPU and memory profiling capabilities, thread analysis, and more.
    - **VisualVM**: Bundled with OpenJDK/Oracle JDK, allowing you to profile CPU and memory usage, take heap/thread dumps, and monitor GC activity.
    - **Java Flight Recorder (JFR)**: A low-overhead, event-based profiler integrated into the JVM. It collects detailed diagnostic and profiling data, which can be viewed in **Java Mission Control**.

## 4. Best Practices

1. **Choose an Appropriate GC**: Evaluate your application’s requirements around throughput vs. latency. Start with the G1 collector for most modern Java applications unless your use case clearly favors another algorithm.

2. **Use Proper JVM Flags**: Tweak heap size (`-Xmx`, `-Xms`), Metaspace size (`-XX:MaxMetaspaceSize`), and GC-specific options (`-XX:+UseG1GC`, `-XX:+UseZGC`) based on workload profiles.
    
3. **Profile in Production-like Environments**: Profilers and heap dumps in development may differ significantly from actual loads. Performance bottlenecks or memory leaks might only appear under real-world stress.
    
4. **Watch Out for Metaspace Leaks**: Dynamic class loading (e.g., in frameworks, OSGi modules, or reflection-heavy libraries) can cause Metaspace to grow. Ensure classes are unloaded properly.
