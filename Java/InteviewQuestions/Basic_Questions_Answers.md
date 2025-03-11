*** Java fundamentals questions and answers** 

| #  | Question | Answer | Example (if required) |
|----|----------|--------|----------------------|
| 1  | What is Java? | Java is a high-level, object-oriented programming language developed by Sun Microsystems (now owned by Oracle). | - |
| 2  | What are the key features of Java? | Platform independence, Object-oriented, Robust, Secure, Multithreading, High Performance, Dynamic. | - |
| 3  | What is JVM? | JVM (Java Virtual Machine) is an abstract machine that provides the runtime environment to execute Java bytecode. | - |
| 4  | What is JDK? | JDK (Java Development Kit) is a software package that includes the JRE and development tools like a compiler and debugger. | - |
| 5  | What is JRE? | JRE (Java Runtime Environment) is a package containing libraries and JVM to run Java applications. | - |
| 6  | What is the difference between JVM, JDK, and JRE? | JVM runs Java bytecode, JRE contains libraries + JVM, and JDK includes JRE + development tools. | - |
| 7  | What is the main() method in Java? | The `main()` method is the entry point of a Java application: `public static void main(String[] args)`. | `public static void main(String[] args) { System.out.println("Hello Java"); }` |
| 8  | Why is Java platform-independent? | Java is platform-independent because of the `JVM`, which allows Java programs to run on any OS. | - |
| 9  | What is bytecode in Java? | Bytecode is an intermediate representation of Java code that JVM interprets and executes. | - |
| 10 | What is the difference between == and .equals()? | `==` checks reference equality, while `.equals()` checks content equality. | `String a = "Java"; String b = "Java"; a.equals(b) → true; a == b → true (if interned)` |
| 11 | What are wrapper classes in Java? | In Java, wrapper classes serve as object representations of primitive data types (e.g., int, char, float, boolean). Each primitive type has a corresponding wrapper class: Integer, Character, Float, Boolean, and so on. These classes encapsulate a primitive value within an object, enabling the use of primitive types in contexts where objects are required. | `int a = 10; Integer obj = Integer.valueOf(a);` |
| 11a | Benefits of Wrapper Classes? | **Null Values:** Unlike primitive types, wrapper classes can represent null values. This is useful in situations where the absence of a value needs to be explicitly indicated, such as when interacting with databases or APIs.  <br> **Utility Methods:** Wrapper classes provide various utility methods for tasks like converting between strings and primitive types (parseInt(), valueOf()), comparing values (compareTo()), and obtaining hash codes (hashCode()).| `String a = 10; int parsedNum = Integer.parseInt(a);` |
| 12 | What is autoboxing and unboxing? | Autoboxing: converting a primitive to an object. Unboxing: converting an object to a primitive. | `Integer obj = 10; int num = obj;` |
| 13 | What are primitive data types in Java? | byte, short, int, long, float, double, char, boolean. | - |
| 14 | What is the default value of an uninitialized int variable? | Default value is `0` for int. | - |
| 15 | What is a class in Java? | A class is a blueprint for creating objects. It contains fields and methods. | `class Car { int speed; void drive() {} }` |
| 16 | What is an object in Java? | An object is an instance of a class that contains state (fields) and behavior (methods). | `Car myCar = new Car();` |
| 17 | What is the difference between class and object? | A class is a template; an object is an instance of a class. | `class Dog {} Dog obj = new Dog();` |
| 18 | What is the difference between static and instance variables? | Static variables are shared across all objects, instance variables are object-specific. | `static int count; int age;` |
| 19 | What is the difference between static and non-static methods? | Static methods belong to the class and don’t require an object, whereas non-static methods need an object. | `static void show() {}; void display() {};` |
| 20 | What is method overloading? | Method overloading allows multiple methods with the same name but different parameters. | `void add(int a, int b); void add(double a, double b);` |
| 21 | What is method overriding? | Method overriding allows a subclass to provide a specific implementation of a method in a superclass. | `class A { void show() {} } class B extends A { void show() {} }` |
| 22 | What is the final keyword in Java? | The `final` keyword is used to declare constants, prevent method overriding, and prevent inheritance. | `final int MAX = 100;` |
| 23 | What is the difference between abstract class and interface? | Abstract class can have method definitions; an interface only has method declarations (before Java 8). | `abstract class A { void show() {} } interface B { void display(); }` |
| 24 | What is polymorphism? | The ability of a method to take different forms (method overloading and overriding). | `Animal a = new Dog(); a.makeSound();` |
| 25 | What is encapsulation? | Encapsulation is wrapping data and methods into a single unit (class) with controlled access. | `private int age; public void setAge(int a) { age = a; }` |
| 26 | What is inheritance? | Inheritance allows a child class to acquire the properties of a parent class. | `class A {} class B extends A {}` |
| 27 | What are constructors in Java? | A constructor is a special method used to initialize an object. | `class A { A() { System.out.println("Constructor called"); } }` |
| 28 | Can a constructor be private? | Yes, a private constructor is used in Singleton design patterns. | `private A() {}` |
| 29 | What is a copy constructor in Java? | Java does not have a built-in copy constructor, but you can create one manually. | `class A { A(A obj) { this.x = obj.x; } }` |
| 30 | What is the super keyword? | The `super` keyword refers to the parent class and is used to call the superclass constructor or method. | `super(); super.show();` |
| 31 | What is the this keyword? | The `this` keyword refers to the current object instance. | `this.x = x;` |
| 32 | What is multiple inheritance? | Java does not support multiple class inheritance but allows multiple interface inheritance. | `class A {} class B {} class C extends A, B {} // Not Allowed` |
| 33 | What is an interface? | An interface is a blueprint of a class with only abstract methods (before Java 8). | `interface A { void show(); }` |
| 34 | What is an abstract class? | An abstract class is a class that cannot be instantiated and may contain abstract methods. | `abstract class A { abstract void show(); }` |
| 35 | What is exception handling? | Exception handling is a mechanism to handle runtime errors using try-catch blocks. | `try { int a = 5/0; } catch (Exception e) {}` |
| 36 | What are checked and unchecked exceptions? | Checked exceptions are checked at compile time, unchecked at runtime. | `IOException (checked), NullPointerException (unchecked)` |
| 37 | What is a finally block? | The `finally` block executes whether an exception occurs or not. | `try {} catch() {} finally {}` |
| 38 | What is a try-with-resources statement? | It automatically closes resources like streams after execution. | `try (FileReader fr = new FileReader("file.txt")) {}` |

## Additional Questions:
### **Difference Between Abstract Class and Interface After Java 8 (Interview Perspective)**  

Since **Java 8**, interfaces have been enhanced with **default and static methods**, reducing the gap between interfaces and abstract classes. Here’s a **detailed comparison** considering the latest changes:  

| Feature | **Abstract Class** | **Interface (After Java 8)** |
|---------|------------------|----------------------------|
| **Methods** | Can have both abstract and concrete methods. | Can have **abstract**, **default**, and **static** methods. |
| **Default Methods** | Allowed (as normal methods). | Introduced in Java 8 using `default` keyword to provide implementation in interfaces. |
| **Static Methods** | Allowed. | Introduced in Java 8. Static methods can have a body and be called using `InterfaceName.method()`. |
| **Fields (Variables)** | Can have instance variables (non-static). | Can only have **public static final (constants)** variables. |
| **Access Modifiers** | Can have **public, private, protected, or default** members. | Methods are **public by default**, but Java 9 introduced **private methods**. |
| **Multiple Inheritance** | Not supported (a class can extend only one abstract class). | Supported (a class can implement multiple interfaces). |


### **Example: Abstract Class vs. Interface After Java 8**
#### **Abstract Class Example**
```java
abstract class Vehicle {
    int speed = 50;
    
    abstract void start(); // Abstract method

    void stop() { // Concrete method
        System.out.println("Vehicle stopped");
    }
}
```

#### **Interface Example (After Java 8)**
```java
interface Engine {
    int power = 100; // Implicitly public, static, and final

    void start(); // Abstract method

    default void fuelEfficiency() { // Default method (Introduced in Java 8)
        System.out.println("This engine has good fuel efficiency");
    }

    static void engineType() { // Static method (Introduced in Java 8)
        System.out.println("This is a petrol engine");
    }
}
```

### **Key Interview Points:**
- **Before Java 8:** Interfaces only had abstract methods, while abstract classes could have concrete methods.  
- **After Java 8:** Interfaces support **default** and **static** methods, reducing the need for abstract classes.  
- **When to Use What?**  
  - Use **abstract class** when you need **state (instance variables)** and **partial implementation**.  
  - Use **interface** when you need **multiple inheritance** or **a strict contract** for implementation.  


- "Can an interface have concrete methods after Java 8?" (**Yes, via default/static methods**).  

- "What is the difference between default and static methods in interfaces?" (**Default methods can be overridden, but static methods belong to the interface itself**).  
- "Can an interface extend another interface?" (**Yes, multiple inheritance is allowed**).  

- Why were default methods introduced in Java 8?
    - To enable backward compatibility without breaking existing implementations.Before Java 8, if a new method was added to an interface, all implementing classes needed to implement it. Default methods allow adding new methods without breaking existing implementations.
    - Also, Java 8 introduced Lambda Expressions and Functional Interfaces (interfaces with a single abstract method). To support this, changes in interfaces were required.

- Can default methods be overridden?
    - Yes, implementing classes can override default methods.
```java
    interface Vehicle {
        default void start() {
            System.out.println("Vehicle is starting...");
        }
    }

    class Car implements Vehicle {
        // Inherits default method start()
    }

    public class Main {
        public static void main(String[] args) {
            Car car = new Car();
            car.start(); // Output: Vehicle is starting...
        }
    }
```
- Can static methods in interfaces be overridden?
    - No, static methods belong to the interface and cannot be overridden by implementing classes.
```java
    interface Engine {
        static void engineType() {
            System.out.println("This is a petrol engine.");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Engine.engineType(); // Output: This is a petrol engine.
        }
    }
```

- Why do we need static methods in interfaces?
    - To define helper/utility methods within the interface instead of using external utility classes.

### **Explain try-with-resources with examples** 

- It is introduced in Java 7 — allows us to declare resources to be used in a try block with the assurance that the resources will be closed after the execution of that block.The resources declared need to implement the AutoCloseable interface.
 - **Example Without finally (Using Try-with-Resources)**
```java
   try (Connection conn = DriverManager.getConnection(jdbcUrl, username, password)) {
    conn.setAutoCommit(false);

    try (PreparedStatement stmt = conn.prepareStatement("INSERT INTO users(name) VALUES ('John Doe')")) {
        stmt.executeUpdate();
    }

    conn.commit();
    } catch (SQLException e) {
        e.printStackTrace();
    }
```
 - **Example Without Try-with-Resources (Needs finally)**
```java
   Connection conn = null;
    try {
        conn = DriverManager.getConnection(jdbcUrl, username, password);
        conn.setAutoCommit(false);

        PreparedStatement stmt = conn.prepareStatement("INSERT INTO users(name) VALUES ('John Doe')");
        stmt.executeUpdate();
        stmt.close();

        conn.commit();
    } catch (SQLException e) {
        e.printStackTrace();
    } finally {
        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }
```
- Note:
    - In try-with-resources, any object that implements AutoCloseable (like `Connection`, `PreparedStatement`, and `ResultSet`) is **automatically closed** when the block exits, regardless of whether it exits normally or due to an exception.
    - `Connection` in JDBC implements AutoCloseable, so it gets closed automatically when the try block finishes.
  

### ** `PATH` Variable:**  
- The `PATH` environment variable tells the **operating system** where to find executable files, including Java tools like `javac` and `java`.  
- It should include the **bin directory** of the Java installation (e.g., `C:\Program Files\Java\jdk-17\bin`).  
- Without setting `PATH`, running `javac` or `java` from the command line will result in a **"command not found"** error.  
- Example:  
  ```sh
  export PATH=$PATH:/usr/lib/jvm/java-17-openjdk-amd64/bin
  ```

### ** `CLASSPATH` Variable:**  
- The `CLASSPATH` environment variable tells the **JVM** where to find **Java class files or JAR files** for execution and compilation.  
- If not set, Java looks in the **current directory (`.`) by default**.  
- Required when referencing **external libraries** in class execution.  
- Example:  
  ```sh
  export CLASSPATH=.:/home/user/lib/myLibrary.jar
  ```

  ### **Java `Properties` Class**  

- The **`Properties` class** in Java is a **subclass of `Hashtable`** used to store **key-value pairs**, where both the key and value are **Strings**.  
- It is commonly used for **reading and writing configuration files**, such as `.properties` files for application settings.  
- Supports **I/O operations** to **load and store properties** from a file using methods like `load()` and `store()`.  
- Example:  
  ```java
  import java.io.FileInputStream;
  import java.util.Properties;

  public class PropertiesExample {
      public static void main(String[] args) throws Exception {
          Properties prop = new Properties();
          prop.load(new FileInputStream("config.properties")); // Load properties file
          System.out.println(prop.getProperty("database.url")); // Read property
      }
  }
  ```

