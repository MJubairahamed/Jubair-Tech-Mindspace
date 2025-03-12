### **Spring Boot Annotations with Real-World Use Cases**  

**important Spring Boot annotations**, their **real-world use cases**, and **practical examples**.  

---

## **🔹 1. Annotations for REST API Development**  

### **1️⃣ `@RestController` – Build REST APIs**  
✅ **Use Case:** When you need to create a REST API that returns JSON data.  

📌 **Example:**  
```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable int id) {
        return new User(id, "John Doe");
    }
}
```
📌 **Real-World Scenario:**  
- Used in **microservices** to expose REST endpoints.  
- **Example:** A **User Service** providing customer details.  

---

### **2️⃣ `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping` – Handle HTTP Requests**  
✅ **Use Case:** When defining different HTTP operations in a REST API.  

📌 **Example:**
```java
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping("/{id}")
    public Product getProduct(@PathVariable Long id) {
        return new Product(id, "Laptop", 1200);
    }

    @PostMapping("/")
    public void createProduct(@RequestBody Product product) {
        // Save product
    }

    @PutMapping("/{id}")
    public void updateProduct(@PathVariable Long id, @RequestBody Product product) {
        // Update product
    }

    @DeleteMapping("/{id}")
    public void deleteProduct(@PathVariable Long id) {
        // Delete product
    }
}
```
📌 **Real-World Scenario:**  
- Used in **e-commerce applications** to handle CRUD operations on products.  
- **Example:** Managing inventory items in an **ERP system**.  

---

### **3️⃣ `@RequestParam` – Handle Query Parameters**  
✅ **Use Case:** When filtering API results using query parameters.  

📌 **Example:**  
```java
@GetMapping("/search")
public List<Product> searchProducts(@RequestParam String name) {
    return productService.findByName(name);
}
```
📌 **Real-World Scenario:**  
- Used in **search functionality** for **filtering users, orders, or products**.  
- **Example:** Searching movies on a streaming platform (`GET /movies?name=Inception`).  

---

## **🔹 2. Annotations for Dependency Injection**  

### **4️⃣ `@Autowired` – Inject Dependencies Automatically**  
✅ **Use Case:** When you need to **inject a service** into a controller.  

📌 **Example:**  
```java
@RestController
public class OrderController {

    @Autowired
    private OrderService orderService;

    @GetMapping("/orders")
    public List<Order> getOrders() {
        return orderService.getAllOrders();
    }
}
```
📌 **Real-World Scenario:**  
- Used in **banking applications** to inject `AccountService` into `TransactionService`.  
- **Example:** A **food delivery app** where `DeliveryService` is injected into `OrderService`.  

---

### **5️⃣ `@Component`, `@Service`, `@Repository` – Define Beans**  
✅ **Use Case:** To create **Spring-managed beans** for business logic and data access.  

📌 **Example:**  
```java
@Service
public class EmailService {
    public void sendEmail(String message) {
        System.out.println("Sending email: " + message);
    }
}
```
📌 **Real-World Scenario:**  
- Used in **e-commerce platforms** to send email notifications.  
- **Example:** Sending an **order confirmation email** after purchase.  

---

## **🔹 3. Annotations for Database Access**  

### **6️⃣ `@Repository` – Define Data Access Layer**  
✅ **Use Case:** When interacting with the database using **Spring Data JPA**.  

📌 **Example:**  
```java
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByName(String name);
}
```
📌 **Real-World Scenario:**  
- Used in **inventory management systems** to fetch products from the database.  
- **Example:** Fetching available seats in a **movie booking app**.  

---

### **7️⃣ `@Transactional` – Handle Transactions Automatically**  
✅ **Use Case:** When performing **database updates** that must be atomic.  

📌 **Example:**  
```java
@Service
public class BankService {

    @Transactional
    public void transferMoney(Long fromAcc, Long toAcc, Double amount) {
        debitAccount(fromAcc, amount);
        creditAccount(toAcc, amount);
    }
}
```
📌 **Real-World Scenario:**  
- Used in **banking applications** to **prevent inconsistent transactions**.  
- **Example:** Ensuring that **money is not deducted unless deposited** successfully.  

---

## **🔹 4. Annotations for Performance Optimization**  

### **8️⃣ `@Cacheable` – Enable Caching**  
✅ **Use Case:** When optimizing API calls by caching frequently accessed data.  

📌 **Example:**  
```java
@Cacheable("products")
public List<Product> getAllProducts() {
    return productRepository.findAll();
}
```
📌 **Real-World Scenario:**  
- Used in **stock market applications** to cache **real-time stock prices**.  
- **Example:** Caching frequently searched flights in a **travel booking app**.  

---

### **9️⃣ `@Async` – Execute Tasks in Background Threads**  
✅ **Use Case:** When performing **long-running operations** asynchronously.  

📌 **Example:**  
```java
@Async
public void sendNotification() {
    System.out.println("Sending notification...");
}
```
📌 **Real-World Scenario:**  
- Used in **messaging applications** to **send push notifications** without blocking the main thread.  
- **Example:** Sending **SMS verification codes** in an authentication system.  

---

## **🔹 5. Annotations for Scheduling and Security**  

### **🔟 `@Scheduled` – Run Jobs Automatically**  
✅ **Use Case:** When running periodic tasks like **batch jobs**.  

📌 **Example:**  
```java
@Scheduled(fixedRate = 60000)
public void generateReport() {
    System.out.println("Generating report every 60 seconds...");
}
```
📌 **Real-World Scenario:**  
- Used in **financial applications** to generate **monthly statements**.  
- **Example:** Running **daily backups** in a database system.  

---

### **1️⃣1️⃣ `@PreAuthorize` – Secure API Endpoints**  
✅ **Use Case:** When **restricting access** to specific users.  

📌 **Example:**  
```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) {
    userRepository.deleteById(id);
}
```
📌 **Real-World Scenario:**  
- Used in **admin dashboards** to **restrict sensitive operations**.  
- **Example:** Preventing non-admin users from **deleting user accounts**.  

---

## **🔥 Final Takeaways**
| Annotation | Real-World Use Case |
|------------|--------------------|
| `@RestController` | Expose REST APIs in microservices. |
| `@Autowired` | Inject dependencies in business logic. |
| `@Repository` | Fetch data from the database. |
| `@Transactional` | Ensure atomic database transactions. |
| `@Cacheable` | Cache API results for performance. |
| `@Async` | Execute long-running tasks in background threads. |
| `@Scheduled` | Run batch jobs automatically. |
| `@PreAuthorize` | Secure API endpoints based on user roles. |
