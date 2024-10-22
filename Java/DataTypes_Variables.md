# Data Types & Variables  
## Data Types
### Basic Data Types in Java: 
* There are two types of data types in Java: 
* Primitive data types. 
* Non-primitive data types. 
![Data Types!](/Java/Images/DataTypes_ss.png "Data Types")

### Java primitive data types with their types, size, range, and default values:

| **Type**  | **Size**       | **Range**                                                               | **Default Value** |
|-----------|----------------|-------------------------------------------------------------------------|-------------------|
| `byte`    | 1 byte (8 bits) | -128 to 127                                                             | 0                 |
| `short`   | 2 bytes (16 bits) | -32,768 to 32,767                                                       | 0                 |
| `int`     | 4 bytes (32 bits) | -2^31 to 2^31-1 (approx. -2.1 billion to 2.1 billion)                   | 0                 |
| `long`    | 8 bytes (64 bits) | -2^63 to 2^63-1 (approx. -9.2 quintillion to 9.2 quintillion)           | 0L                |
| `float`   | 4 bytes (32 bits) | Approximately ±3.40282347E+38F (6-7 significant decimal digits)         | 0.0f              |
| `double`  | 8 bytes (64 bits) | Approximately ±1.79769313486231570E+308 (15 significant decimal digits) | 0.0d              |
| `char`    | 2 bytes (16 bits) | 0 to 65,535 (Unsigned Unicode characters)                              | '\u0000' (null character) |
| `boolean` | 1 bit           | `true` or `false`                                                       | `false`           |


## Variables
* Variables are used to store data.
* Variable can store the value based on the min & max range of the datatypes. Ex: byte b=128 will throw as byte max value is 127.

### Java variable naming rules
| **Rule**                              | **Description**                                                                                  | **Example**              |
|---------------------------------------|--------------------------------------------------------------------------------------------------|--------------------------|
| **Must Start with a Letter or Underscore** | The variable name must begin with a letter (a-z, A-Z) or an underscore (`_`). It cannot start with a number. | Correct: `age`, `_score` <br> Incorrect: `1stPlace`, `123name` |
| **Can Contain Letters, Numbers, and Underscores** | After the first character, variable names can include letters, digits, or underscores. No spaces allowed. | Correct: `student1`, `final_score` <br> Incorrect: `final score`, `my#name` |
| **No Special Characters**             | Variable names cannot contain special symbols like `@`, `#`, `%`, etc., except for `$` and `_`.   | Correct: `total$Amount`, `name_` <br> Incorrect: `@count`, `salary#` |
| **Case-Sensitive**                    | Java treats uppercase and lowercase letters differently. `name` and `Name` are different variables. | `studentAge`, `StudentAge` (different variables) |
| **Cannot Use Reserved Keywords**      | Java’s reserved keywords (e.g., `int`, `class`, `if`) cannot be used as variable names.          | Incorrect: `int`, `if`, `class` |
| **Descriptive and Meaningful Names**  | It is a good practice to use names that clearly describe the variable’s purpose.                  | Good: `studentAge`, `totalMarks` <br> Bad: `x`, `y` |
| **Use CamelCase for Multiple Words**  | When naming variables with more than one word, use camelCase: start with lowercase and capitalize subsequent words. | Correct: `studentName`, `totalMarks` <br> Incorrect: `Studentname`, `Totalmarks` |

