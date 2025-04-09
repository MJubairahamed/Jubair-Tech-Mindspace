# JAVA FQA's
## Genereal Interview Questions

### General Java Questions**
### 1. **Explain the difference between `HashMap`, `LinkedHashMap`, and `TreeMap`.**
   - **Answer**:  
     - `HashMap` is **unordered** and offers O(1) time complexity for insert, delete, and search.
     - `LinkedHashMap` maintains **insertion order** and performs slightly slower than `HashMap`.
     - `TreeMap` maintains **sorted order** (according to keys) and offers O(log n) time complexity.

### 2. **How does Java handle memory management, and what is garbage collection?**
   - **Answer**:  
     Java uses **automatic memory management** with the help of **Garbage Collection (GC)**. GC reclaims unused objects in **heap memory**. The key GC algorithms include:
     - **Serial GC** (for small applications)
     - **Parallel GC** (for multi-threaded applications)
     - **G1 GC** (for low-latency applications)
     - **ZGC & Shenandoah** (for ultra-low-latency needs)

### 3. **What is the difference between `Callable` and `Runnable`?**
   - **Answer**:  
     - `Runnable` runs on a separate thread but **cannot return a result**.
     - `Callable<V>` allows returning a value and can **throw checked exceptions**.

### 4. **Explain the SOLID principles in Java.**
   - **Answer**:
     - **S**ingle Responsibility Principle (SRP) – A class should have **one reason to change**.
     - **O**pen/Closed Principle (OCP) – A class should be **open for extension but closed for modification**.
     - **L**iskov Substitution Principle (LSP) – Subtypes must be **interchangeable** with their base types.
     - **I**nterface Segregation Principle (ISP) – Prefer **small, specific interfaces** over large, general ones.
     - **D**ependency Inversion Principle (DIP) – Depend on **abstractions, not concrete implementations**.
    
        
### 5. **What is the difference between `@Transactional` and `propagation` in Spring?**
   - **Answer**:  
     - `@Transactional` ensures database operations are atomic (all succeed or fail).
     - `Propagation` defines how transactions interact when one method calls another:
       - `REQUIRED` (default) – Uses an existing transaction or creates one.
       - `REQUIRES_NEW` – Always starts a new transaction.
       - `NESTED` – Runs within a parent transaction but can roll back independently.

### 6. `volatile` Variable:**  
- Used for **multi-threading** to ensure **visibility** of variable changes across threads.  
- Prevents **caching** of the variable by threads, ensuring every read fetches the latest value from main memory.  
- Does **not guarantee atomicity** for compound operations (e.g., `x++`).  
- Example:  
  ```java
  class Example {
      volatile int counter = 0; // Changes visible to all threads
  }
  ```  

### 7. `transient` Variable:**  
- Used in **serialization** to prevent storing a variable's value when an object is serialized.  
- Useful for sensitive data like **passwords** or **temporary variables**.  
- Upon deserialization, the variable is reset to its **default value** (`null`, `0`, `false`, etc.).  
- Example:  
  ```java
  class Example implements Serializable {
      transient int tempData; // Will not be serialized
  }
  ```  

### 8. What is the difference between `fail-fast` &  `fail-safe`iterators in Java?**  
- **Fail-Fast Iterators:** Fail-fast iterators in Java are designed to immediately throw a **ConcurrentModificationException** if the underlying collection is structurally modified while the iterator is in use (except for modifications made through the iterator's own methods like remove()). They ensure that the iteration process is halted as soon as a concurrent modification is detected, preventing potential inconsistencies.
- Fail-fast iterators provide immediate feedback about concurrent modifications but might lead to exceptions and termination of the iteration.

- **Fail-Safe Iterators:** Fail-safe iterators in Java operate on a cloned copy of the collection. They do not throw exceptions if the underlying collection is modified during iteration. However, any modifications made to the original collection after the iterator is created will not be reflected in the iterator. This approach ensures that the iterator operates on a stable copy of the data and avoids potential concurrent modification issues.
- Fail-safe iterators continue the iteration without exceptions but might not reflect recent changes in the collection.

- **Fail Fast** [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/CollectionExamples/CheckFailFast.java)
- **Fail Safe** [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/CollectionExamples/CheckFailSafe.java)

### 9. What is the instanceOf Operator ?**  
- 

