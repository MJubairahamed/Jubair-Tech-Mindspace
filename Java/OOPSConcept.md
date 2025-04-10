# OOPS Concepts
-
- Unstructured Programming Languages - The most primitive of all programming languages having sequentially flow of control.  Code is repeated throughout the program.
- Structured Programming Languages - Has non-sequentially flow of control. Use of functions allows for re-use of code.
- Object Oriented Programming: Combines Data & Action Together.

## Principle Concepts OOPS  
- **Abstraction**
- **Encapsulation**
- **Polymorphism**
- **Inheritance**

- **Abstraction :**
    - Representing essential features without including the background details or explanations.
    - Abstract class must be extended/subclassed (to be useful). It serves as a template. 
    - A class that is abstract may not be instantiated (ie. you may not call its constructor), abstract class may contain static data.
    - An abstract class may also have concrete (complete) methods.
    - For design purpose, a class can be declared abstract even if it does not contain any abstract methods.
    - Reference of an abstract class can point to objects of its sub-classes thereby achieving run-time polymorphism
        `Ex: Shape obj = new Rectangle();`
    - A class must be compulsorily labeled abstract , if it has one or more abstract methods.   
    - Example: 
        - `Rectangle obj = new Rectangle();//An object of the class rectangle, will gives a rectangle.`
        - `Triangle obj = new Triangle();//An object of the class triangle, will gives a triangle.`
        - `Shape obj = new Shape();// Parent Class to above.An shape object gives?Here we have to declare a class a abstract.`
        - `abstract public void calcArea(); //no implementation required.`

- **Encapsulation :**   
    - Encapsulation is a technique used for hiding the properties and behaviours of an object and allowing outside access only as appropriate. It prevents other objects from directly altering or accessing the properties or methods of the encapsulated object.
    - Although a lesser degree of encapsulation can be achieved by making the members public or protected.
    - Encapsulation helps the developer to make the code more flexible and maintainable by binding related data in a single unit and access/restrict that using appropriate access modifier. With well encapsulation implementation, one can change one part of the code easily without affecting the other part of the code.

- **Polymorphism :** 
    - An object to have more than one form.
    - Inheritance, Overloading and Overriding are used to achieve Polymorphism in java.
    - There are two types of polymorphism one is **Compile time polymorphism** and the other is **run time polymorphism**.
        - **Dynamic or Runtime Polymorphism**
            - The process in which a call to an overridden method is resolved at runtime rather than compile-time.
            - A reference variable of the super class can refer to a sub class object   
            - `Doctor obj = new Surgeon(); obj.treatPatient();`
            - Here the reference variable “obj” is of the parent class , but the object it is pointing to is of the child class.
            - `obj.treatPatient()` will execute treatPatient() method of the sub-class – Surgeon.
            - If a base class reference is used to call a method, the method to be invoked is decided by the JVM, depending on the object the reference is pointing to.
            - This is decided during run-time and hence termed dynamic or run-time polymorphism.

- **Inheritance :** 
    - When a “Is-A” relationship exists between two classes we use Inheritance.
    - The parent class is termed super class and the inherited class is the sub class>.
    - The keyword extends is used by the sub class to inherit the features of super class.
    - Inheritance is important since it leads to reusability of code.

- **Method Overriding :** 
    - Redefining a super class method in a sub class is called method overriding.
    - Rules for Method Overriding
        - The method signature i.e. method name, parameter list and return type have to match exactly.
        - The overridden method can widen the accessibility but not narrow it, i.e. if it is private in the base class, the child class can make it public but not vice versa.

- **Method OverLoading :** 
    - Overloading in java occurs when methods in a same class or in child classes shares a same name with a ‘difference in number of arguments’ or ‘difference in argument type’ or both.
   
- **Method OverLoading :** 
    - The class which implements the interface needs to provide functionality for the methods declared in the interface.
    - All methods in an interface are implicitly public and abstract.
    - An interface cannot be instantiated.
    - An interface reference can point to objects of its implementing classes.
    - An interface can extend from one or many interfaces. A class can extend only one class but implement any number of interfaces.

### **Abstraction vs Encapsulation **

| **Aspect**            | **Abstraction**                                                                 | **Encapsulation**                                                            |
|-----------------------|----------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Definition**         | Hiding **implementation details** and showing only **essential features**       | Wrapping **data and code together** and **restricting direct access**       |
| **Goal**              | Focus on **what the object does**                                               | Focus on **how data is protected**                                           |
| **Example**           | Using a `List` interface without knowing if it’s backed by `ArrayList` or `LinkedList` | Making fields `private` and accessing them via `getters/setters`            |
| **Used for**          | Simplifying complexity for the user                                             | Protecting data from unwanted changes                                        |
| **Access**            | Achieved via **abstract classes, interfaces**                                   | Achieved via **access modifiers** (`private`, `public`, etc.)               |
| **Real-world analogy**| Driving a car without knowing how the engine works                              | Keeping the engine locked so no one can tamper with its internals           |
| **Benefit**           | Promotes **loose coupling**, reusability                                        | Promotes **data hiding**, security                                           |
| **When to Use**       | When you want to **hide complexity and expose functionalities**                 | When you want to **safeguard internal state of objects**                    |

### 🧠 Interview Tip:
> "Abstraction is about **hiding the 'how'** and showing only the **'what'**. Encapsulation is about **hiding the data** to protect it. Both are core OOP principles and work best **together** to create clean, modular, and secure code."

###  **Abstract Class vs Interface**

| **Aspect**                | **Abstract Class**                                                   | **Interface**                                                              |
|---------------------------|----------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Definition**             | A class that can have **abstract and non-abstract methods**          | A contract with **abstract methods (default/static allowed)**             |
| **Purpose**               | Used when classes share **common behavior**                          | Used to define **capability/contract**                                     |
| **Keyword**               | `abstract class`                                                     | `interface`                                                                |
| **Inheritance Type**      | Supports **single inheritance**                                      | Supports **multiple inheritance** (via multiple interfaces)               |
| **Access Modifiers**      | Can have **private, protected, public** methods and fields           | Only **public** methods (by default), fields are `public static final`     |
| **Constructors**          | ✔ Can have constructors                                              | ❌ Cannot have constructors                                                |
| **State (fields/vars)**   | ✔ Can have instance variables                                        | ❌ Cannot have instance variables (only constants)                         |
| **Default Implementation**| ✔ Can provide method implementation                                  | ✔ Can provide `default` and `static` method implementations (since Java 8) |
| **When to Use**           | When you need a **base class with shared code**                      | When you need to define **common capabilities** across unrelated classes  |
| **Real-world analogy**    | A **partially built blueprint** used by subclasses                  | A **contract** that classes agree to follow                               |

### 🧠 Interview Tip :
> "Use an abstract class when you want to share code among closely related classes. Use an interface when you expect unrelated classes to implement a common set of behaviors. Thanks to Java 8+, interfaces can now include default methods, but abstract classes still offer more structure like constructors and state."

Here's a **simple and effective table** to explain the **difference between Static Polymorphism and Dynamic Polymorphism**, tailored for **senior software engineer interviews**:

### **Static vs Dynamic Polymorphism**

| **Aspect**               | **Static Polymorphism** (Compile-time)                              | **Dynamic Polymorphism** (Run-time)                                       |
|--------------------------|----------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Also Known As**        | Method Overloading                                                   | Method Overriding                                                         |
| **When is it Resolved?** | At **compile time**                                                  | At **run time**                                                           |
| **How it Works**         | Based on **method signature** (name + parameters)                    | Based on **object type** at runtime                                       |
| **Flexibility**          | Less flexible – method to call is fixed at compile time              | More flexible – behavior decided dynamically                              |
| **Inheritance Required?**| ❌ Not required                                                      | ✔ Required – typically via superclass and subclass                        |
| **Performance**          | Slightly **faster** (resolved early)                                 | Slightly **slower** (resolved at runtime via virtual table)              |
| **Real-world analogy**   | A calculator with **buttons for each operation**                     | A remote that behaves **differently with different TVs**                 |
| **Java Example**         | Multiple `add()` methods with different parameters                   | A `draw()` method overridden in `Circle`, `Rectangle` subclasses         |
| **Use Case**             | When you want to **perform similar operations with different inputs**| When you want **subclass-specific behavior through a base class**        |

### 🧠 Interview Tip :
> "Static polymorphism improves code readability with overloading, while dynamic polymorphism enhances extensibility through overriding. Mastery of both is key to designing scalable and flexible object-oriented systems."

## What is Data hiding?
* Data hiding in Java is a way to protect the internal details of a class by keeping its data (like variables) private and providing only public methods (functions) to access or change that data. This helps prevent others from directly changing the data in unexpected ways and keeps the inner workings of the class safe and controlled.
* It's like hiding your valuables in a locked box and only letting others use a key to access or change them through a controlled opening.