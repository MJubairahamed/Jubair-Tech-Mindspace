# String
### Key Points of string
In Java, a `String` is a built-in class used to represent sequences of characters. It can be created using string literals (e.g., `String str1 = "Java program";`) or through constructors. Strings are immutable, meaning they cannot be modified once created. Java also maintains a pool of string constants to optimize memory; identical string literals refer to the same object in the pool. New string objects created with the `new` keyword reside in heap memory. There are three string constructors: `String(char[])`, which converts a character array to a string; `String(byte[])`, converting a byte array; and `String(String)` for creating new strings from existing ones. Reference variables in Java hold or point to objects, including strings.

### How strings are stored?
* String is special class in Java and all String literal e.g. "abc"  (anything which is inside double quotes are String literal in Java) are maintained in a separate String pool, special memory location inside Java memory.

* Any time you create a new String object using String literal, JVM first checks String pool and if an object with similar content available, than it returns that and doesn't create a new object.

* JVM doesn't perform String pool check if you create object using 'new' operator.

![String Storage!](/Java/Images/StringStorage.png "String Storage")

## Concise list of key points about Java `String` that are frequently asked during interviews:

1. **Immutable Nature**: Strings in Java are immutable, meaning once a string is created, its value cannot be changed. Any modification creates a new object.
    * Why Java Strings are immutable?
        * Main reason behind it is for better performance. 
        * Creating a copy of existing java String is easier as there is no need to create a new instance but can be easily created by pointing to already existing String. This saves valuable primary memory.

2. **String Pool**: Java maintains a special memory pool (string pool) to store string literals. If a string with the same content exists in the pool, new references point to the existing object instead of creating a new one.

3. **Creating Strings**: Strings can be created using string literals (e.g., `String str = "text";`) or the `new` keyword (e.g., `String str = new String("text");`). The former allows for pooling optimization.

4. **String Methods**: Familiarity with common `String` methods such as `length()`, `charAt()`, `substring()`, `toLowerCase()`, `toUpperCase()`, `trim()`, `equals()`, `equalsIgnoreCase()`, `compareTo()`, `split()`, and `replace()` is crucial.

5. **String Comparison**: Use `equals()` to compare string content instead of `==`, which compares object references.

6. **StringBuilder and StringBuffer**: Both classes offer mutable alternatives to `String` for efficient string manipulation. `StringBuffer` is thread-safe (synchronized), whereas `StringBuilder` is not but offers better performance in single-threaded contexts.

7. **Concatenation and Performance**: Using the `+` operator for string concatenation creates new objects due to immutability, potentially impacting performance. `StringBuilder` or `StringBuffer` is recommended for iterative concatenation.

8. **Interning Strings**: The `intern()` method returns a canonical representation of the string from the pool if it already exists, helping save memory.

9. **Character Arrays vs. Strings**: Strings are immutable, while character arrays (`char[]`) are mutable. This distinction matters for sensitive data storage (e.g., passwords) due to security reasons.

10. **Regular Expressions (Regex)**: The `String` class supports basic regex functionalities through methods like `matches()`, `split()`, `replaceAll()`, and `replaceFirst()`.

11. **String immutability impact on Hashing**: Strings are commonly used as keys in `HashMap` due to their immutability, ensuring consistent hash codes for the same content.

12. **Unicode Support**: Java `String` supports Unicode, making it suitable for internationalization.

13. **Difference between `==` and `.equals()`**: `==` compares memory references, while `.equals()` checks the content of the strings.

14. **Substring Sharing Memory**: Prior to Java 7, `substring()` used to share the memory with the original string (due to `char[]` backing). This was changed to avoid memory leaks.

15. **Empty and Null Strings**: An empty string (`""`) is different from a `null` reference; it represents a `String` object with zero characters.

Having a deep understanding of these key points will help you effectively handle string-related questions in interviews.