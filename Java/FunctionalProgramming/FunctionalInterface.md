# Functional Interface Notes
### **What is Functional Interface in Java** 
- An interface that contains **only one abstract method**. 
- Functional interfaces can have multiple default or static methods, but only one abstract method. 
- Runnable, ActionListener, and Comparator are common examples of Java functional interfaces. 
- From Java 8 onwards, lambda expressions and method references can be used to represent the instance of a functional interface.
- Functional Interface is additionally recognized as Single Abstract Method Interfaces. In short, they are also known as SAM interfaces

- Example:
    ```java 
        public class Geeks {  
        public static void main(String[] args) {
                // Using lambda expression 
                // to implement Runnable
                new Thread(() -> System.out.println("New thread created")).start();
            }
        }
        Output: New thread created
        ```
### @FunctionalInterface Annotation
- **@FunctionalInterface** annotation is used to ensure that the functional interface cannot have more than one abstract method. In case more than one abstract methods are present, the compiler flags an **“Unexpected @FunctionalInterface annotation”** message. However, it is not mandatory to use this annotation.

### Java built in Functional Interface?
- There are many interfaces that are converted into functional interfaces. All these interfaces are annotated with @FunctionalInterface.  
    - These interfaces are as follows:
        - **Runnable:** This interface only contains the run() method.
        - **Comparable:** This interface only contains the compareTo() method.
        - **ActionListener:** This interface only contains the actionPerformed() method.
        - **Callable:** This interface only contains the call() method.

### Types of Functional Interfaces in Java
- four main kinds of functional interfaces which can be applied in multiple situations as mentioned below:.  
    1. Consumer - It accepts a single input argument and returns no result.        
    2. Predicate - It accepts a single argument and returns a boolean result.       
    3. Function - It accepts a single argument and returns a result.        
    4. Supplier - It does not take any arguments but provides a result.

- **Bi Variant of above:**
     - BiConsumer - It accepts two arguments and returns no result.
     - BiPredicate -It accepts two arguments and returns a boolean result.
     - BiFunction -It accepts two arguments and returns a result.

### What are static methods in Interfaces?
- **Static methods**, which contains method implementation is owned by the interface and is invoked using the name of the interface, it is suitable for defining the utility methods and cannot be overridden.

### What is the default method, and why is it required?
- In Java, a "default method" allows interfaces to have methods with implementations, enabling the addition of new methods to interfaces without breaking existing implementations of those interfaces.
- This is required to maintain backward compatibility and allow for evolving interfaces without forcing all implementing classes to recompile and update. 
- Example:
    ```java     
    interface MyInterface {
        void abstractMethod(); // Abstract method
        default void defaultMethod() { // Default method
            System.out.println("Default implementation");
        }
    }
    ```
### Important Points:
- An infinite number of methods (whether **static or default) can be added to the functional interface. In simple words, there is no limit to a functional interface containing static and default methods.
- **Overriding methods** from the parent class do not violate the rules of a functional interface in Java.
- The **java.util.function** package contains many built-in functional interfaces in Java 8.