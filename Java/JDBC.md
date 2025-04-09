

### **Difference Between `Statement.executeBatch()` and `PreparedStatement.executeUpdate()`**

Both `executeBatch()` and `executeUpdate()` are used to execute **SQL statements** in **JDBC**, but they serve different purposes and have distinct advantages.

---

## **1. `Statement.executeBatch()` (Batch Execution)**
**Used when executing multiple SQL queries together as a batch.**  
- It reduces the number of database round trips, improving performance.  
- Used for bulk inserts, updates, or deletes.  
- Typically used with `Statement` or `PreparedStatement`.  
- **Best for large data processing (bulk operations).**  

### **Example: Batch Execution (Multiple Inserts)**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class BatchExample {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/your_database";
        String username = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(jdbcUrl, username, password);
             Statement stmt = conn.createStatement()) {

            conn.setAutoCommit(false); // Disable auto-commit for batch processing

            // Add multiple insert statements to batch
            stmt.addBatch("INSERT INTO users(name, email) VALUES ('John Doe', 'john@example.com')");
            stmt.addBatch("INSERT INTO users(name, email) VALUES ('Jane Doe', 'jane@example.com')");
            stmt.addBatch("UPDATE accounts SET balance = balance + 500 WHERE user_id = 1");

            // Execute batch
            int[] results = stmt.executeBatch();
            conn.commit(); // Commit only if all queries succeed

            System.out.println("Batch executed successfully!");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
### **Key Points of `executeBatch()`**
✔ **Multiple queries executed in a single database round-trip** (better performance).  
✔ **Rollback possible** (if used inside a transaction).  
✔ **Efficient for bulk operations** (e.g., inserting thousands of records).  
⚠ **If one query fails, the whole batch may fail** (depending on database settings).  

---

## **2. `PreparedStatement.executeUpdate()` (Single Query Execution)**
**Used for executing a single `INSERT`, `UPDATE`, or `DELETE` query at a time.**  
- Executes one query at a time.  
- Accepts **dynamic parameters** (`?` placeholders) to prevent SQL injection.  
- **Best for executing queries with dynamic values in loops.**  

### **Example: Executing a Single Query with `executeUpdate()`**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class UpdateExample {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/your_database";
        String username = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(jdbcUrl, username, password)) {
            String updateQuery = "UPDATE users SET email = ? WHERE name = ?";
            
            try (PreparedStatement pstmt = conn.prepareStatement(updateQuery)) {
                pstmt.setString(1, "updated_email@example.com");
                pstmt.setString(2, "John Doe");

                int rowsAffected = pstmt.executeUpdate();
                System.out.println(rowsAffected + " row(s) updated.");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
### **Key Points of `executeUpdate()`**
✔ **Executes a single `INSERT`, `UPDATE`, or `DELETE` query.**  
✔ **Safer than `Statement.executeBatch()`** (as it executes one query at a time).  
✔ **Prevents SQL injection using placeholders (`?`).**  
⚠ **Multiple executions require multiple database calls (less efficient for bulk operations).**  

---

## **3. When to Use Which?**
| Feature | `Statement.executeBatch()` | `PreparedStatement.executeUpdate()` |
|---------|---------------------------|-----------------------------------|
| **Use Case** | Bulk operations (multiple queries) | Single `INSERT`, `UPDATE`, `DELETE` |
| **Performance** | High (single round trip) | Lower (multiple round trips) |
| **Dynamic Parameters (`?`)** | ❌ No | ✅ Yes |
| **SQL Injection Protection** | ❌ No | ✅ Yes |
| **Transaction Support** | ✅ Yes | ✅ Yes |
| **Best For** | Bulk inserts/updates/deletes | Updating/inserting single records |

---

## **4. Best of Both Worlds: `PreparedStatement.executeBatch()`**
You can also use **`PreparedStatement` with `executeBatch()`** to combine batch execution and SQL injection protection.

### **Example: Batch Execution Using `PreparedStatement`**
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class PreparedStatementBatchExample {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/your_database";
        String username = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(jdbcUrl, username, password)) {
            conn.setAutoCommit(false);

            String insertQuery = "INSERT INTO users(name, email) VALUES (?, ?)";
            try (PreparedStatement pstmt = conn.prepareStatement(insertQuery)) {
                
                pstmt.setString(1, "User1");
                pstmt.setString(2, "user1@example.com");
                pstmt.addBatch(); // Add to batch
                
                pstmt.setString(1, "User2");
                pstmt.setString(2, "user2@example.com");
                pstmt.addBatch(); // Add to batch
                
                pstmt.setString(1, "User3");
                pstmt.setString(2, "user3@example.com");
                pstmt.addBatch(); // Add to batch
                
                // Execute batch
                int[] result = pstmt.executeBatch();
                conn.commit(); // Commit transaction
                
                System.out.println("Batch insert completed!");

            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
✔ **Combines batch execution and SQL injection prevention.**  
✔ **Efficient for bulk inserts and updates.**  

---

## **Final Recommendation**
- **Use `executeUpdate()`** if executing **one query at a time** (e.g., updating a single record).  
- **Use `executeBatch()`** if executing **multiple queries in a single transaction** (better performance).  
- **Use `PreparedStatement.executeBatch()`** to get **both performance and security** (ideal for bulk inserts/updates).  

Would you like an example using **HikariCP for better connection management? 🚀**