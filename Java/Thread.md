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

### **🔹 Why Synchronization?**
- To prevent **race conditions** where multiple threads access shared resources incorrectly.  
- Ensures **thread safety** when modifying shared objects.


### **🔹What is `Callable` in Java?**  
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

---
### **What is `Future` in Java?**  
`Future<T>` is an interface in Java's **`java.util.concurrent`** package that represents the **result of an asynchronous computation**. It allows you to:  
✅ **Check if a task is completed** (`isDone()`).  
✅ **Cancel a task** (`cancel()`).  
✅ **Retrieve the result** (`get()`, which blocks until completion).  

---

### **🔹 Key Methods of `Future<T>`**
| **Method** | **Description** |
|------------|----------------|
| `boolean cancel(boolean mayInterruptIfRunning)` | Attempts to cancel execution. |
| `boolean isCancelled()` | Returns `true` if the task was cancelled. |
| `boolean isDone()` | Returns `true` if the task is completed. |
| `T get()` | Retrieves the result (blocks if not ready). |
| `T get(long timeout, TimeUnit unit)` | Retrieves result with a timeout. |

✅ **Future waits until the task completes and retrieves the result.**  

### **🔹 `Future` vs `CompletableFuture`**
| Feature | `Future<T>` | `CompletableFuture<T>` |
|---------|------------|----------------------|
| **Blocking** | Yes (uses `get()`) | No (async support) |
| **Callbacks** | No | Yes (`thenApply()`, `thenAccept()`) |
| **Exception Handling** | Uses `try-catch` | Supports `exceptionally()` |
| **Chaining Tasks** | No | Yes (`thenCompose()`) |

### **🔹 𝗪𝗵𝗲𝗻 𝘁𝗼 𝗨𝘀𝗲 `𝗖𝗮𝗹𝗹𝗮𝗯𝗹𝗲` 𝗮𝗻𝗱 `𝗙𝘂𝘁𝘂𝗿𝗲`?**
✅ When **asynchronous processing** is needed but callbacks aren’t required.  
✅ When managing **long-running tasks** in **multi-threaded applications**. Split large tasks into smaller parallel ones.
✅ When using `ExecutorService` to **execute background tasks**.  
✅ Concurrent API Calls: Retrieve results from multiple endpoints simultaneously.

---
### **🔹 Difference Between `sleep()` and `wait()` in Java**  

Both `sleep()` and `wait()` cause a thread to pause, but they have different behaviors and use cases.
- **Sleep()** is a blocking operation that keeps a hold on the monitor/lock of the shared objects for the specified number of milliseconds.Use when delaying execution.
- **Wait()** is pauses the thread until either the specified number of milliseconds have elapsed or it recieves a desired notification from another thread. Note whithout keep hold on the monitor/lock of the shared objects. use when coordinating multiple threads 

### **🔹 Key Differences of `Sleep` and `Wait`**
| Feature | `sleep(long ms)` | `wait(long ms)` |
|---------|----------------|----------------|
| **Defined In** | `Thread` class | `Object` class |
| **Purpose** | Pauses the thread for a given time | Makes the thread wait until notified |
| **Lock Handling** | Does **not** release the lock | **Releases the lock** on the object |
| **Resumption** | Automatically resumes after timeout | Needs `notify()` or `notifyAll()` |
| **Usage Scenario** | Used to introduce **delays** | Used for **thread communication** |


### **🔹 When to Use What?**
| Use Case | Use `sleep()` | Use `wait()` |
|----------|-------------|-------------|
| **Delay execution for a fixed time** | ✅ Yes | ❌ No |
| **Pause execution until another thread notifies** | ❌ No | ✅ Yes |
| **Retain object lock while sleeping** | ✅ Yes | ❌ No (Releases lock) |
| **Thread synchronization and coordination** | ❌ No | ✅ Yes |

---