Here are **10 advanced Object-Oriented Programming (OOP) concepts** that are frequently tested in **senior-level Java interviews**, along with their explanations and examples:  

---

### **1. SOLID Principles**  
SOLID is a set of design principles for writing maintainable and scalable software.  

**Answer:**  
- **S** - **Single Responsibility Principle (SRP)**: A class should have only one reason to change.  
- **O** - **Open/Closed Principle (OCP)**: Classes should be open for extension but closed for modification.  
- **L** - **Liskov Substitution Principle (LSP)**: Subtypes must be replaceable with their base types without altering program behavior.  
- **I** - **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they do not use.  
- **D** - **Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules. Both should depend on abstractions.  

**Example (SRP)**:  
```java
class Report {
    void generateReport() { /* Generates report */ }
}

class ReportPrinter {
    void printReport() { /* Prints report */ }
}
```
Here, `Report` is responsible for generating the report, and `ReportPrinter` is responsible for printing it, following SRP.  

---

### **2. Method Overloading vs. Method Overriding**  
These are key concepts of **polymorphism** in Java.  

**Answer:**  
- **Method Overloading**: Defining multiple methods with the same name but different parameters. (Compile-time polymorphism)  
- **Method Overriding**: Redefining a method in a subclass that already exists in the parent class. (Runtime polymorphism)  

**Example (Overriding):**  
```java
class Parent {
    void display() { System.out.println("Parent class"); }
}

class Child extends Parent {
    @Override
    void display() { System.out.println("Child class"); }
}
```

---

### **3. Composition vs. Inheritance**  
Favor **composition over inheritance** for better maintainability.  

**Answer:**  
- **Inheritance**: A subclass derives properties from a parent class (tight coupling).  
- **Composition**: A class contains an instance of another class instead of inheriting from it (loose coupling).  

**Example (Composition):**  
```java
class Engine {
    void start() { System.out.println("Engine started"); }
}

class Car {
    private Engine engine = new Engine();
    void startCar() { engine.start(); }
}
```
Here, `Car` contains an `Engine` instead of extending it, reducing tight coupling.  

---

### **4. Abstract Classes vs. Interfaces**  
Understanding when to use an **abstract class** vs. an **interface** is crucial.  

**Answer:**  
- **Abstract Class**:  
  - Can have both abstract and concrete methods.  
  - Used when classes share common behavior.  
- **Interface**:  
  - Only contains abstract methods (before Java 8) or default/static methods (Java 8+).  
  - Used for defining contracts.  

**Example:**  
```java
abstract class Animal {
    abstract void makeSound();
    void sleep() { System.out.println("Sleeping..."); }
}

interface Flyable {
    void fly();
}

class Bird extends Animal implements Flyable {
    void makeSound() { System.out.println("Chirp"); }
    public void fly() { System.out.println("Flying"); }
}
```

---

### **5. Covariant Return Types**  
Allows overriding methods to return a subclass type instead of the parent type.  

**Example:**  
```java
class Animal {}
class Dog extends Animal {}

class Parent {
    Animal getAnimal() { return new Animal(); }
}

class Child extends Parent {
    @Override
    Dog getAnimal() { return new Dog(); } // Covariant return type
}
```

---

### **6. Object Cloning (Deep Copy vs. Shallow Copy)**  
Cloning helps create exact copies of objects.  

**Answer:**  
- **Shallow Copy**: Copies object references (changes in the copy affect the original).  
- **Deep Copy**: Creates a completely independent copy.  

**Example (Shallow Copy):**  
```java
class Person implements Cloneable {
    String name;
    Person(String name) { this.name = name; }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```
**Deep Copy Example:**  
```java
class Address {
    String city;
    Address(String city) { this.city = city; }
}

class Person {
    String name;
    Address address;

    Person(String name, Address address) {
        this.name = name;
        this.address = new Address(address.city);
    }
}
```
Here, the deep copy creates a new instance of `Address`.  

---

### **7. Static Binding vs. Dynamic Binding**  
Understanding how Java resolves method calls at compile-time vs. runtime.  

**Answer:**  
- **Static Binding (Compile-time)**: Method resolution happens at compile time (e.g., method overloading).  
- **Dynamic Binding (Runtime)**: The actual method to be executed is determined at runtime (e.g., method overriding).  

**Example (Dynamic Binding):**  
```java
class Parent {
    void show() { System.out.println("Parent"); }
}

class Child extends Parent {
    void show() { System.out.println("Child"); }
}

Parent obj = new Child();
obj.show(); // Output: "Child" (Runtime resolution)
```

---

### **8. Reflection in Java**  
Reflection allows inspecting and modifying class behavior at runtime.  

**Example:**  
```java
import java.lang.reflect.Method;

class Test {
    void display() { System.out.println("Hello"); }
}

public class ReflectionExample {
    public static void main(String[] args) throws Exception {
        Class<?> obj = Class.forName("Test");
        Method method = obj.getDeclaredMethod("display");
        method.invoke(obj.getDeclaredConstructor().newInstance()); // Output: Hello
    }
}
```

---

### **9. Singleton Design Pattern**  
Ensures that only one instance of a class exists in the application.  

**Example (Thread-Safe Singleton):**  
```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static synchronized Singleton getInstance() {
        if (instance == null) instance = new Singleton();
        return instance;
    }
}
```

---

### **10. Dependency Injection (DI) and IoC**  
Used in frameworks like **Spring** to achieve loose coupling.  

**Example (Constructor Injection):**  
```java
class Service {
    void serve() { System.out.println("Service running"); }
}

class Client {
    private Service service;

    Client(Service service) { this.service = service; }

    void doSomething() { service.serve(); }
}

// Usage
Client client = new Client(new Service());
client.doSomething();
```
Here, `Service` is injected into `Client`, following the **Inversion of Control (IoC)** principle.  

---
### **11. What is the difference between Composition, Aggregation, and Association?**  
**Answer:**  
- **Association**: A general relationship where one class is related to another without ownership.  
- **Aggregation** (Weak Association): A "has-a" relationship where one class contains another, but the contained object can exist independently.  
- **Composition** (Strong Association): A "has-a" relationship where the contained object’s lifecycle is dependent on the container class.  

**Example:**  
```java
class Address {} // Exists independently

class Employee {
    Address address; // Aggregation (Employee "has-a" Address)
}

class Engine {} // Exists only with Car

class Car {
    private final Engine engine = new Engine(); // Composition
}
```
---

### **12. What is a Marker Interface? Can we create our own?**  
**Answer:**  
A **marker interface** is an empty interface (without methods) used to provide metadata to Java classes. Examples: `Serializable`, `Cloneable`.  
Yes, we can create our own.  

**Example:**  
```java
interface MyMarker {} // Custom marker interface

class MyClass implements MyMarker {} 
```
Java frameworks (e.g., `instanceof` checks in serialization) use marker interfaces to identify capabilities.  

---

### **13. How does Garbage Collection (GC) work in Java? What are the types of GC algorithms?**  
**Answer:**  
GC in Java automatically removes unused objects from memory. Java has multiple GC algorithms:  
- **Serial GC** (Good for single-threaded applications)  
- **Parallel GC** (Multi-threaded, default for Java 8)  
- **G1 (Garbage First) GC** (Balances performance, used in Java 9+)  
- **ZGC and Shenandoah GC** (Low-latency GCs introduced in newer Java versions)  

**Example:**  
```java
System.gc(); // Suggests JVM to run garbage collection
```
However, explicit calls to `System.gc()` are discouraged.  

---

### **14. What is Method Hiding in Java? How is it different from Overriding?**  
**Answer:**  
When a **static method** in a subclass has the same name as one in its superclass, it is **hidden**, not overridden.  

**Example:**  
```java
class Parent {
    static void display() { System.out.println("Parent static method"); }
}

class Child extends Parent {
    static void display() { System.out.println("Child static method"); }
}

Parent obj = new Child();
obj.display(); // Output: Parent static method (Not overridden)
```
Unlike overriding, **method hiding binds at compile time**.  

---

### **15. What is the Role of `final`, `finally`, and `finalize()` in Java?**  
**Answer:**  
- **`final`**: Used for **constants, methods, and classes**.  
- **`finally`**: A block in exception handling that **always executes**, even if an exception is thrown.  
- **`finalize()`**: A **deprecated** method that was called before an object was garbage collected.  

**Example (finally block):**  
```java
try {
    int x = 5 / 0;
} catch (ArithmeticException e) {
    System.out.println("Exception caught");
} finally {
    System.out.println("This always executes");
}
```
---

### **16. How does Java handle multiple inheritance?**  
**Answer:**  
Java **does not support multiple inheritance** with classes to avoid **Diamond Problem**, but it supports it using **interfaces**.  

**Example:**  
```java
interface A { void show(); }
interface B { void show(); }

class C implements A, B {
    public void show() { System.out.println("Resolved multiple inheritance"); }
}
```
Here, `C` implements both `A` and `B` but provides its own implementation of `show()`, resolving ambiguity.  

---

### **17. What is a Functional Interface? Can it have multiple methods?**  
**Answer:**  
A **functional interface** has exactly **one abstract method** and may have **default/static methods**.  

**Example:**  
```java
@FunctionalInterface
interface MyFuncInterface {
    void execute(); // Single abstract method
    default void log() { System.out.println("Logging..."); }
}
```
Java 8 introduced **lambda expressions**, which rely on functional interfaces.  

---

### **18. What are Proxy Classes in Java? How are they used in frameworks like Spring?**  
**Answer:**  
A **proxy class** is a dynamically created class at runtime that wraps another class to add functionality (e.g., logging, security).  

**Example (Dynamic Proxy in Java Reflection API):**  
```java
import java.lang.reflect.*;

interface Service {
    void serve();
}

class RealService implements Service {
    public void serve() { System.out.println("Serving..."); }
}

class ServiceProxy {
    public static Service createProxy(Service realService) {
        return (Service) Proxy.newProxyInstance(
            realService.getClass().getClassLoader(),
            new Class[]{Service.class},
            (proxy, method, args) -> {
                System.out.println("Logging before execution");
                return method.invoke(realService, args);
            }
        );
    }
}
```
Used in **Spring AOP** for method interception.  

---

### **19. What is a Thread-Safe Singleton? How do we implement it?**  
**Answer:**  
A **thread-safe singleton** ensures only one instance of a class is created, even in multi-threaded environments.  

**Example (Double-Checked Locking):**  
```java
class Singleton {
    private static volatile Singleton instance;
    
    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
This ensures **lazy initialization** and **thread safety**.  

---

### **20. How does Java’s `Optional` Class Help in Handling Null Values?**  
**Answer:**  
`Optional<T>` helps avoid `NullPointerException` by explicitly handling null values.  

**Example:**  
```java
import java.util.Optional;

class Test {
    static Optional<String> getData() {
        return Optional.ofNullable(null); // Returns empty Optional
    }

    public static void main(String[] args) {
        Optional<String> data = getData();
        System.out.println(data.orElse("Default Value")); // Output: Default Value
    }
}
```
Used in **functional programming** to replace traditional null checks.  

---

### **Conclusion**  
These **10 additional Java interview questions** cover topics like **memory management, concurrency, design patterns, Java 8+, and Spring framework-related topics**, which are essential for **senior developers**. 🚀