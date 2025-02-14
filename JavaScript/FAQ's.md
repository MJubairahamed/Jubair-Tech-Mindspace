# JAVA SCRIPT FQA's
## Genereal Interview Questions
Here’s a set of **Senior Java Developer** interview questions, including **10 coding challenges with answers**. The questions cover **core Java, multithreading, collections, design patterns, Spring, Hibernate, and coding problems**.

---

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
    
    
    | **SOLID Principle** | **Definition** | **Example in Java** |
    |---------------------|---------------|----------------------|
    | **S** - **Single Responsibility Principle (SRP)** | A class should have only **one reason to change**—it should **only do one thing**. | ```java class Employee { private String name; private double salary; public Employee(String name, double salary) { this.name = name; this.salary = salary; } public String getName() { return name; } public double getSalary() { return salary; } } class SalaryCalculator { public double calculateBonus(Employee emp) { return emp.getSalary() * 0.1; } } class EmployeePrinter { public void printDetails(Employee emp) { System.out.println("Employee: " + emp.getName() + ", Salary: " + emp.getSalary()); } } ``` |
    | **O** - **Open/Closed Principle (OCP)** | A class should be **open for extension, but closed for modification**—you should be able to **add new functionality without changing existing code**. | ```java interface Shape { double area(); } class Circle implements Shape { private double radius; public Circle(double radius) { this.radius = radius; } public double area() { return Math.PI * radius * radius; } } class Rectangle implements Shape { private double length, width; public Rectangle(double length, double width) { this.length = length; this.width = width; } public double area() { return length * width; } } class AreaCalculator { public double calculateArea(Shape shape) { return shape.area(); } } ``` |
    | **L** - **Liskov Substitution Principle (LSP)** | **Subclasses should be replaceable for their base classes** without affecting the correctness of the program. | ```java class Bird { public void fly() { System.out.println("Bird is flying"); } } class Sparrow extends Bird {} class Ostrich extends Bird { @Override public void fly() { throw new UnsupportedOperationException("Ostriches cannot fly!"); } } // Violates LSP because Ostrich cannot fully substitute Bird. ``` **FIX:** Use an interface instead of forcing all birds to fly: ```java interface Flyable { void fly(); } class Sparrow implements Flyable { public void fly() { System.out.println("Sparrow is flying"); } } class Ostrich {} ``` |
    | **I** - **Interface Segregation Principle (ISP)** | **Clients should not be forced to implement unnecessary methods** that they don't need. **Prefer multiple small interfaces over a large general one.** | ```java interface Workable { void work(); } interface Eatable { void eat(); } class Developer implements Workable, Eatable { public void work() { System.out.println("Coding..."); } public void eat() { System.out.println("Eating lunch..."); } } class Robot implements Workable { public void work() { System.out.println("Working..."); } } ``` **Good:** Robot doesn’t implement `Eatable` since it doesn’t need it. |
    | **D** - **Dependency Inversion Principle (DIP)** | **High-level modules should not depend on low-level modules; both should depend on abstractions.** **Use interfaces instead of concrete classes.** | ```java interface Keyboard { void type(); } class MechanicalKeyboard implements Keyboard { public void type() { System.out.println("Typing on mechanical keyboard"); } } class Computer { private Keyboard keyboard; public Computer(Keyboard keyboard) { this.keyboard = keyboard; } public void startTyping() { keyboard.type(); } } class Main { public static void main(String[] args) { Keyboard keyboard = new MechanicalKeyboard(); Computer pc = new Computer(keyboard); pc.startTyping(); } } ``` |
        
5. **What is the difference between `@Transactional` and `propagation` in Spring?**
   - **Answer**:  
     - `@Transactional` ensures database operations are atomic (all succeed or fail).
     - `Propagation` defines how transactions interact when one method calls another:
       - `REQUIRED` (default) – Uses an existing transaction or creates one.
       - `REQUIRES_NEW` – Always starts a new transaction.
       - `NESTED` – Runs within a parent transaction but can roll back independently.

---

### 

### **Coding Challenges with Solutions**

#### **1. Reverse a String without using built-in methods**
```java
public class ReverseString {
    public static String reverse(String str) {
        StringBuilder sb = new StringBuilder();
        for (int i = str.length() - 1; i >= 0; i--) {
            sb.append(str.charAt(i));
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        System.out.println(reverse("Hello")); // Output: olleH
    }
}
```

---

#### **2. Find the first non-repeating character in a string**
```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstUniqueChar {
    public static char findFirstUnique(String str) {
        Map<Character, Integer> charCount = new LinkedHashMap<>();
        for (char c : str.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }
        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            if (entry.getValue() == 1) return entry.getKey();
        }
        return '_'; // Return '_' if no unique character found
    }

    public static void main(String[] args) {
        System.out.println(findFirstUnique("swiss")); // Output: w
    }
}
```

---

#### **3. Check if a number is prime**
```java
public class PrimeCheck {
    public static boolean isPrime(int num) {
        if (num <= 1) return false;
        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPrime(11)); // Output: true
    }
}
```

---

#### **4. Find the factorial of a number using recursion**
```java
public class Factorial {
    public static int factorial(int n) {
        return (n == 0) ? 1 : n * factorial(n - 1);
    }

    public static void main(String[] args) {
        System.out.println(factorial(5)); // Output: 120
    }
}
```

---

#### **5. Find the missing number in an array**
```java
public class MissingNumber {
    public static int findMissing(int[] arr, int n) {
        int total = n * (n + 1) / 2;
        int sum = 0;
        for (int num : arr) sum += num;
        return total - sum;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 4, 5, 6};
        System.out.println(findMissing(nums, 6)); // Output: 3
    }
}
```

---

#### **6. Check if a string is a palindrome**
```java
public class PalindromeCheck {
    public static boolean isPalindrome(String str) {
        int left = 0, right = str.length() - 1;
        while (left < right) {
            if (str.charAt(left++) != str.charAt(right--)) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("madam")); // Output: true
    }
}
```

---

#### **7. Implement a simple Singleton pattern**
```java
public class Singleton {
    private static Singleton instance;

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

---

#### **8. Find the intersection of two arrays**
```java
import java.util.HashSet;

public class ArrayIntersection {
    public static void findIntersection(int[] arr1, int[] arr2) {
        HashSet<Integer> set = new HashSet<>();
        for (int num : arr1) set.add(num);
        for (int num : arr2) {
            if (set.contains(num)) System.out.print(num + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {3, 4, 5, 6, 7};
        findIntersection(arr1, arr2); // Output: 3 4 5
    }
}
```

---

#### **9. Reverse a linked list**
```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class ReverseLinkedList {
    public static ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```

---

#### **10. Implement a simple Producer-Consumer using `BlockingQueue`**
```java
import java.util.concurrent.*;

class Producer implements Runnable {
    private BlockingQueue<Integer> queue;
    Producer(BlockingQueue<Integer> queue) { this.queue = queue; }
    public void run() {
        try {
            for (int i = 1; i <= 5; i++) {
                queue.put(i);
                System.out.println("Produced: " + i);
                Thread.sleep(500);
            }
        } catch (InterruptedException e) { e.printStackTrace(); }
    }
}
```

---
