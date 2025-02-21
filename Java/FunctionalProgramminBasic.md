## Functional programming basics.

### **Difference Between `System.out::println` and `System.out.println` in Java**  

| Feature               | `System.out.println("Hello")` | `System.out::println` |
|----------------------|--------------------------------|----------------------|
| **Type** | Direct method call | Method reference (Functional Programming) |
| **Usage** | Executes `println()` immediately | Passes `println()` as a reference |
| **Where Used** | General method invocation | Used with functional interfaces like `forEach()` |
| **Example Usage** | `System.out.println("Hello");` | `list.forEach(System.out::println);` |
