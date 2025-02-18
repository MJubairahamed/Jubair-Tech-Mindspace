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
| 11 | What are wrapper classes in Java? | Wrapper classes (Integer, Double, Boolean, etc.) convert primitives to objects. | `int a = 10; Integer obj = Integer.valueOf(a);` |
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
