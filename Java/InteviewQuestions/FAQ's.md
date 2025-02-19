# JAVA FQA's
## Genereal Interview Questions

### **General Java Questions**
1. **Explain the difference between `HashMap`, `LinkedHashMap`, and `TreeMap`.**
   - **Answer**:  
     - `HashMap` is **unordered** and offers O(1) time complexity for insert, delete, and search.
     - `LinkedHashMap` maintains **insertion order** and performs slightly slower than `HashMap`.
     - `TreeMap` maintains **sorted order** (according to keys) and offers O(log n) time complexity.

2. **How does Java handle memory management, and what is garbage collection?**
   - **Answer**:  
     Java uses **automatic memory management** with the help of **Garbage Collection (GC)**. GC reclaims unused objects in **heap memory**. The key GC algorithms include:
     - **Serial GC** (for small applications)
     - **Parallel GC** (for multi-threaded applications)
     - **G1 GC** (for low-latency applications)
     - **ZGC & Shenandoah** (for ultra-low-latency needs)

3. **What is the difference between `Callable` and `Runnable`?**
   - **Answer**:  
     - `Runnable` runs on a separate thread but **cannot return a result**.
     - `Callable<V>` allows returning a value and can **throw checked exceptions**.

4. **Explain the SOLID principles in Java.**
   - **Answer**:
     - **S**ingle Responsibility Principle (SRP) – A class should have **one reason to change**.
     - **O**pen/Closed Principle (OCP) – A class should be **open for extension but closed for modification**.
     - **L**iskov Substitution Principle (LSP) – Subtypes must be **interchangeable** with their base types.
     - **I**nterface Segregation Principle (ISP) – Prefer **small, specific interfaces** over large, general ones.
     - **D**ependency Inversion Principle (DIP) – Depend on **abstractions, not concrete implementations**.
    
        
5. **What is the difference between `@Transactional` and `propagation` in Spring?**
   - **Answer**:  
     - `@Transactional` ensures database operations are atomic (all succeed or fail).
     - `Propagation` defines how transactions interact when one method calls another:
       - `REQUIRED` (default) – Uses an existing transaction or creates one.
       - `REQUIRES_NEW` – Always starts a new transaction.
       - `NESTED` – Runs within a parent transaction but can roll back independently.

---


