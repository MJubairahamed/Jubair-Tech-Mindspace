## Functional programming basics.

### **Method Reference in Java**  

✅ **Method Reference** is a shorthand way to refer to a method **without calling it explicitly**. It makes the code **cleaner and more readable**, especially when using **Lambda Expressions**.  
✅  It works with static methods (`Class::staticMethod`), instance methods (`object::method` or `Class::method`), and constructors (`Class::new`).

### **🔹 Why Use Method References?**
🔸 Reduces **boilerplate code** in Lambda Expressions.  
🔸 Improves **code readability** and **reusability**.  
🔸 Works with **Functional Interfaces** (like `Consumer<T>`, `Supplier<T>`, `Predicate<T>`).  

### **🔹 Syntax of Method References**
```java
ClassName::methodName  // Syntax for static and instance methods
```

## **2️⃣ Types of Method References**
| Type | Syntax | Example |
|------|--------|---------|
| **Static Method Reference** | `ClassName::staticMethod` | `Math::sqrt` instead of `x -> Math.sqrt(x)` |
| **Instance Method Reference (on object)** | `object::instanceMethod` | `"hello"::toUpperCase` instead of `() -> "hello".toUpperCase()` |
| **Instance Method Reference (on class type, used in streams)** | `ClassName::instanceMethod` | `String::length` instead of `s -> s.length()` |
| **Constructor Reference** | `ClassName::new` | `ArrayList::new` instead of `() -> new ArrayList<>()` |

- **Method Reference:** [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/FunctionalInterface/LamdaExamples/MethodReferenceExample.java)

---