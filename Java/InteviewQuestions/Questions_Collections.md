Here is a **table with 30 Java Collections Framework questions** suitable for a **10-year experienced candidate** in an interview setting.  

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
| 10 | What is the difference between HashMap and Hashtable? | `HashMap` is **non-synchronized** and allows **null keys/values**. `Hashtable` is **synchronized** and **does not allow null keys or values**. | - |
| 11 | What is LinkedHashMap, and how does it differ from HashMap? | `LinkedHashMap` maintains the **insertion order**, while `HashMap` does not guarantee any order. | - |
| 12 | What is the time complexity of basic operations in HashMap? | **O(1)** (best case) for `put()`, `get()`, `remove()`. In worst-case collision scenarios, it is **O(log n)** (Java 8+ due to tree structure). | - |
| 13 | What is WeakHashMap? | `WeakHashMap` stores keys as **WeakReferences**, allowing GC to remove entries if the key is no longer referenced elsewhere. | - |
| 14 | What is IdentityHashMap? | Unlike `HashMap`, it uses **reference equality (`==`)** instead of `.equals()` for key comparison. | - |
| 15 | What is the difference between TreeMap and HashMap? | `TreeMap` maintains **sorted order** (Red-Black Tree), while `HashMap` has no ordering guarantees. | - |
| 16 | What is ConcurrentHashMap? | A thread-safe version of `HashMap` using **segment-based locking** for better performance. | - |
| 17 | What is CopyOnWriteArrayList? | A thread-safe `ArrayList` where all mutative operations (`add`, `remove`) create a **new copy** of the list. Best suited for **read-heavy scenarios**. | - |
| 18 | What is BlockingQueue? | It is a **thread-safe queue** used for producer-consumer scenarios, blocking when retrieving from an empty queue or inserting into a full one. | `LinkedBlockingQueue, ArrayBlockingQueue` |
| 19 | What are PriorityQueue and its use case? | A queue where elements are ordered based on **natural ordering** or a **custom comparator**. Used in **task scheduling** and **graph algorithms** (Dijkstra’s). | - |
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
