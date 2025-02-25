# Thread Concepts

### **Java Threads & Multithreading - Key Concepts for Interviews**  

---

## **🔹 Basics of Threads in Java**
1. **What is a Thread?**  
   - A thread is the **smallest unit of execution** within a process.  
   - Java provides built-in support for multithreading using the `Thread` class and `Runnable` interface.  

2. **Ways to Create a Thread in Java**  
   ✅ **Extending `Thread` class**  
   ```java
   class MyThread extends Thread {
       public void run() {
           System.out.println("Thread running...");
       }
   }

   public class Test {
       public static void main(String[] args) {
           MyThread t = new MyThread();
           t.start(); // Starts a new thread
       }
   }
   ```
   ✅ **Implementing `Runnable` interface** (Preferred for better design)  
   ```java
   class MyRunnable implements Runnable {
       public void run() {
           System.out.println("Runnable thread running...");
       }
   }

   public class Test {
       public static void main(String[] args) {
           Thread t = new Thread(new MyRunnable());
           t.start();
       }
   }
   ```

3. **Difference Between `Thread` and `Runnable`**
   - `Thread` consumes more memory (as it extends `Thread`), while `Runnable` is more scalable (since it can be used with thread pools).  
   - `Runnable` allows multiple threads to share the same instance.  

---

## **🔹 Thread Lifecycle & Important Methods**
### **Thread States**
- **`NEW`** – Created but not started (`Thread t = new Thread();`).  
- **`RUNNABLE`** – Running or ready to run.  
- **`BLOCKED`** – Waiting for a lock.  
- **`WAITING` & `TIMED_WAITING`** – Waiting indefinitely or for a specified time.  
- **`TERMINATED`** – Thread execution completed.  

### **Common Thread Methods**
| **Method** | **Description** |
|------------|----------------|
| `start()` | Starts a new thread. |
| `run()` | Defines the task for the thread (called by `start()`). |
| `join()` | Makes the calling thread wait until another thread finishes execution. |
| `sleep(ms)` | Pauses execution for the given time. |
| `yield()` | Suggests that the thread scheduler allow other threads to run. |
| `interrupt()` | Interrupts a sleeping or waiting thread. |

✅ **Example: `join()` to Ensure Thread Completes Before Main Thread Proceeds**
```java
public class ThreadJoinExample {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread running: " + i);
            }
        });

        t1.start();
        t1.join(); // Main thread waits for t1 to finish

        System.out.println("Main thread resumes after t1.");
    }
}
```

---

## **🔹 Thread Synchronization & Locks**
### **Why Synchronization?**
- To prevent **race conditions** where multiple threads access shared resources incorrectly.  
- Ensures **thread safety** when modifying shared objects.


### **What is `Callable` in Java?**  
`Callable<T>` is an interface in Java introduced in **Java 5** under the **`java.util.concurrent`** package. It is used to define **tasks that return a result** and **can throw checked exceptions**, unlike `Runnable`.

---

### **🔹 Key Differences Between `Callable` and `Runnable`**
| Feature | `Runnable` | `Callable<T>` |
|---------|-----------|--------------|
| **Return Type** | `void` (Does not return a result) | Returns a value (`T`) |
| **Exception Handling** | Cannot throw checked exceptions | Can throw checked exceptions |
| **Method** | `public void run()` | `public T call() throws Exception` |
| **Usage** | Used with `Thread` | Used with `ExecutorService.submit()` |

---



- **Callable Example** [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/ThreadConcepts/CallableExample.java)
- **MultiCallable Example** [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/ThreadConcepts/MultiCallableExample.java)