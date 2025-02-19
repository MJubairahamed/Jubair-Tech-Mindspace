# Java String - Interview Notes  

- **Definition**: `String` is a built-in class representing sequences of characters.  
- **Creation**:  
  - Using **string literals** (e.g., `String str1 = "Java program";`) → Stored in **String Pool**.  
  - Using **constructors** (e.g., `new String("Java")`) → Stored in **Heap Memory**.  
  - **JVM** doesn't perform String pool check if you create object using 'new' operator.
      ![String Storage!](/Java/Images/StringStorage.png "String Storage")
- **Immutability**: Strings **cannot be modified** once created.  
- **String Pool Optimization**: Identical string literals refer to the **same object** in the **String Constant Pool** to save memory.  
- **Heap Allocation**: Strings created with `new` are stored in the heap, even if they have the same value as a pooled string.  
- **Constructors**:  
  1. `String(char[])` → Converts character array to string.  
  2. `String(byte[])` → Converts byte array to string.  
  3. `String(String)` → Creates a new string from an existing one.  
- **Reference Variables**: Store memory addresses pointing to string objects.

---

### **Java `String` - Key Interview Points**  

1. **Immutability**:  
   - `String` objects are immutable, meaning modifications create new instances.  
   - **Why?**  
     - Improves performance by enabling string pooling.  
     - Saves memory by reusing existing string literals instead of creating new ones.  

2. **String Pool (Interning)**:  
   - Java stores string literals in a **special memory pool** to optimize memory.  
   - If a string with the same content exists, new references point to the existing object.  
   - The `intern()` method explicitly stores a string in the pool if not already present.  

3. **Creating Strings**:  
   - **String Literals**: `String str = "Java";` (stored in the string pool).  
   - **Using `new` Keyword**: `String str = new String("Java");` (creates a new object in heap memory).  

4. **String Comparison**:  
   - Use `.equals()` to compare string **content**.  
   - `==` checks if two references point to the same object, not content.  

5. **String Methods** *(Commonly Asked in Interviews)*:  
   - `length()`, `charAt()`, `substring()`, `toLowerCase()`, `toUpperCase()`, `trim()`,  
   - `equals()`, `equalsIgnoreCase()`, `compareTo()`, `split()`, `replace()`.  

6. **Performance & Concatenation**:  
   - Using `+` repeatedly creates multiple string objects due to immutability.  
   - **Use `StringBuilder` or `StringBuffer`** for efficient string manipulation.  

7. **StringBuilder vs. StringBuffer**:  
   - `StringBuilder` (faster, non-thread-safe).  
   - `StringBuffer` (thread-safe, synchronized).  

8. **String and Hashing**:  
   - Strings are widely used as keys in `HashMap` because immutability ensures a **consistent hash code**.  

9. **Character Arrays vs. Strings**:  
   - `String` is **immutable**, while `char[]` is **mutable**.  
   - Using `char[]` for passwords is safer as it can be cleared after use.  

10. **Regular Expressions (Regex) in Strings**:  
   - Methods like `matches()`, `split()`, `replaceAll()`, and `replaceFirst()` support regex operations.  

11. **Unicode Support**:  
   - Java `String` supports **Unicode**, making it useful for internationalization.  

12. **Empty vs. Null Strings**:  
   - `""` (empty string) is a valid `String` object.  
   - `null` means the reference doesn’t point to any object.  

13. **Substring Memory Issue (Fixed in Java 7+)**:  
   - Before Java 7, `substring()` used to **share memory** with the original string, leading to **memory leaks**.  
   - Now, it creates a **new character array** instead.  

---
