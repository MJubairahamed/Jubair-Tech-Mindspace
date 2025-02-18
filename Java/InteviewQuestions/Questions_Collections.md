**30 Java Collections Framework questions** 

| #  | Question | Answer | Example (if required) |
|----|----------|--------|----------------------|
| 1  | What is the Java Collections Framework? | It is a unified architecture for representing and manipulating collections (groups of objects). It includes interfaces, implementations (classes), and algorithms. | - |
| 2  | What are the core interfaces in the Collections Framework? | The main interfaces are `Collection`, `List`, `Set`, `Queue`, `Deque`, and `Map`. | - |
| 3  | What is the difference between Collection and Collections? | `Collection` is an interface, whereas `Collections` is a utility class that contains static methods for manipulating collections. | `Collections.sort(list);` |
| 4  | What is the difference between List, Set, and Map? | `List`: Ordered collection with duplicates. `Set`: Unordered, no duplicates. `Map`: Key-value pairs, keys are unique. | - |
| 5  | What is the difference between ArrayList and LinkedList? | `ArrayList` is backed by a dynamic array, offers fast random access but slow insert/delete in the middle. `LinkedList` is a doubly linked list, providing faster insertions/deletions but slower random access. | - |
| 6  | When should you use an ArrayList over a LinkedList? | Use `ArrayList` when **frequent access** operations are required. Use `LinkedList` when **frequent insertions/deletions** are needed. | - |
| 7  | How does HashSet maintain uniqueness? | It uses a **hashing mechanism** and relies on `hashCode()` and `equals()` to prevent duplicates. | - |
| 8  | What is the difference between HashSet and TreeSet? | `HashSet` is unordered, while `TreeSet` maintains a **sorted order** (Red-Black Tree). | - |
| 9  | How does HashMap work internally? | It uses an **array of buckets** and applies **hashing** (`hashCode()`) to store key-value pairs efficiently. **Collisions** are handled via **Linked List (before Java 8)** or **Tree (after Java 8, for high collision cases).** | - |
| 10 | What is the difference between HashMap and Hashtable? | `HashMap` is **non-synchronized** and allows **null keys/values**,HashMap allows adding one Entry with null as key as well as many entries with null as value. `Hashtable` is **synchronized** and **does not allow null keys or values**. | - |
| 11 | What is LinkedHashMap, and how does it differ from HashMap? | `LinkedHashMap` maintains the **insertion order**, while `HashMap` does not guarantee any order. | - |
| 12 | What is the time complexity of basic operations in HashMap? | **O(1)** (best case) for `put()`, `get()`, `remove()`,meaning that the operation takes constant time regardless of the size of the map. In worst-case collision scenarios, it is **O(log n)** (Java 8+ due to tree structure). | - |
| 13 | What is WeakHashMap? | `WeakHashMap` stores keys as **WeakReferences**, allowing GC to remove entries if the key is no longer referenced elsewhere. | - |
| 14 | What is IdentityHashMap? | Unlike `HashMap`, it uses **reference equality (`==`)** instead of `.equals()` for key comparison. | - |
| 15 | What is the difference between TreeMap and HashMap? | `TreeMap` maintains **sorted order** (Red-Black Tree), while `HashMap` has no ordering guarantees. | - |
| 16 | What is ConcurrentHashMap? | The ConcurrentHashMap is a **thread-safe implementation of the Map interface**. It allows multiple threads to read and write data simultaneously, without the need for locking the entire map. Unlike a regular HashMap, which is not thread-safe, ConcurrentHashMap ensures that the operations are thread-safe, making it ideal for scenarios where multiple threads need to access and modify the map concurrently.| - |
| 17 | What is CopyOnWriteArrayList? | It implements the List Interface. A thread-safe `ArrayList` where all mutative operations (`add`, `remove`) create a **new copy** of the list. Best suited for **read-heavy scenarios**. | - |
| 18 | What is BlockingQueue? | A blocking queue is a data structure in Java that allows threads to wait for space to become available when adding items to a queue, or for items to become available when removing them. | `LinkedBlockingQueue, ArrayBlockingQueue` |
| 19 | What are PriorityQueue and its use case? | A PriorityQueue in Java is a special type of queue where each element is associated with a priority. Elements are retrieved based on their priority, with the highest priority element being dequeued first. If multiple elements have the same priority, they are dequeued in the order they were added. It is based on the heap data structure. | - |
| 20 | How does TreeSet maintain order? | `TreeSet` uses a **Red-Black Tree**, ensuring elements are stored in **sorted order**. | - |
| 21 | What is the difference between SynchronizedList and CopyOnWriteArrayList? | `SynchronizedList` is synchronized using **locks**, whereas `CopyOnWriteArrayList` uses **copy-on-write** (creating a new list on modification). | - |
| 22 | What is the difference between Poll() and Remove() in Queue? | `poll()` retrieves and removes the head **or returns null** if empty. `remove()` does the same but **throws an exception** if empty. | - |
| 23 | How do you implement a custom comparator in Java? | Implement `Comparator<T>` and override `compare()` method. | `Collections.sort(list, new MyComparator());` |
| 24 | Can we use null as a key in TreeMap? | No, `TreeMap` does not allow `null` as a key because it needs to compare keys using `compareTo()`. | - |
| 25 | How do you synchronize a collection in Java? | Use `Collections.synchronizedList()`, `Collections.synchronizedSet()`, or `Collections.synchronizedMap()`. | `List list = Collections.synchronizedList(new ArrayList());` |
| 26 | What is a Deque in Java? | A **double-ended queue** that allows insertion and deletion from both ends. Implemented via `ArrayDeque` or `LinkedList`. | `Deque<Integer> deque = new ArrayDeque<>();` |
| 27 | How do you convert an array to an ArrayList? | Using `Arrays.asList()` or `new ArrayList<>(Arrays.asList())`. | `List<Integer> list = Arrays.asList(1, 2, 3);` |
| 28 | What is the difference between Iterable and Iterator? | `Iterable` provides an `iterator()`, while `Iterator` is used to iterate elements using `next()`. | - |
| 29 | How do you remove an element while iterating a collection? | Using `Iterator.remove()`, as `for-each` loop will cause `ConcurrentModificationException`. | `Iterator<Integer> it = list.iterator(); while(it.hasNext()) { it.remove(); }` |
| 30 | What is EnumSet and its advantages? | A high-performance `Set` for enums, internally using a **bitwise representation**, making it very memory-efficient. | `EnumSet.of(Day.MONDAY, Day.TUESDAY);` |

---
**What is the difference between `Collection` and `Collections?`**
| Feature | **Collection** | **Collections** |
|---------|--------------|----------------|
| **Definition** | `Collection` is an **interface** in Java that represents a group of objects. | `Collections` is a **utility class** that provides static methods for working with collections. |
| **Package** | `java.util.Collection` (superinterface for List, Set, Queue). | `java.util.Collections` (utility class for collection manipulation). |
| **Type** | Interface | Class |
| **Usage** | Provides a blueprint for implementing data structures like `List`, `Set`, `Queue`. | Provides helper methods such as sorting, searching, and thread-safety. |
| **Methods** | Contains methods like `add()`, `remove()`, `size()`, `iterator()`. | Contains static utility methods like `sort()`, `reverse()`, `synchronizedList()`, `min()`, `max()`. |
| **Inheritance** | Extended by subinterfaces (`List`, `Set`, `Queue`). | Cannot be extended (final class). |
| **Implementation** | Implemented by classes like `ArrayList`, `HashSet`, `LinkedList`, etc. | Not implemented, only contains static methods. |
| **Thread Safety** | Does not provide synchronization by default. | Provides methods like `synchronizedList()` and `synchronizedMap()` for thread safety. |
| **Sorting Support** | No built-in sorting mechanism. | Provides `Collections.sort()` for sorting lists. |

---

### **Example of `Collection` (Interface) Usage**
```java
import java.util.ArrayList;
import java.util.Collection;

public class CollectionExample {
    public static void main(String[] args) {
        Collection<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        System.out.println(fruits);
    }
}
```

### **Example of `Collections` (Utility Class) Usage**
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();
        fruits.add("Orange");
        fruits.add("Apple");
        fruits.add("Banana");

        Collections.sort(fruits); // Sorting list using Collections class
        System.out.println(fruits); // Output: [Apple, Banana, Orange]
    }
}
```
---
### **Difference Between `Collections.sort()` with and without `Comparator`**  
### **🔹 Summary**
| Feature | `Collections.sort(list)` (Without Comparator) | `Collections.sort(list, Comparator)` (With Comparator) |
|---------|--------------------------------|------------------------------------|
| **Sorting Order** | Natural order (ascending for numbers, lexicographical for Strings). | Custom order (ascending, descending, or based on other properties). |
| **Implementation Requirement** | Class must implement `Comparable<T>` and override `compareTo()`. | No need to modify class; sorting logic is external. |
| **Flexibility** | One sorting logic per class. | Multiple sorting strategies possible. |
| **Best Use Case** | Simple sorting when natural order is sufficient. | Complex sorting scenarios (e.g., sorting by multiple fields). |

---


---
## Notes:
 - In Java, "non-synchronized" signifies that a method or block of code does not have any built-in mechanism to control concurrent access from multiple threads. When a method is not synchronized, multiple threads can execute it simultaneously, potentially leading to data corruption or inconsistent state if the method accesses shared resources. 
    - on-synchronized methods are faster due to the absence of locking overhead
 - synchronized methods or blocks, which allow only one thread to execute them at a time, ensuring data consistency.