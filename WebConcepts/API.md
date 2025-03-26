# API

### What is API?
- An API (Application Programming Interface) is a set of rules and protocols that allows different software applications to communicate and interact with each other, enabling them to share data and functionality. 

As a **Senior Java Developer**, having a strong understanding of **APIs (Application Programming Interfaces)** is crucial, especially for designing and consuming **RESTful APIs** efficiently. Below are the **major concepts** you should know:

---

## **1. REST API Basics**
### **What is a REST API?**
- **REST (Representational State Transfer)** is an architectural style for designing networked applications.
- Uses **HTTP methods** for communication and follows stateless principles.

### **Common HTTP Methods**
| **Method**   | **Usage**                      |
|-------------|--------------------------------|
| `GET`       | Retrieve resource data        |
| `POST`      | Create a new resource         |
| `PUT`       | Update/replace a resource     |
| `PATCH`     | Partially update a resource   |
| `DELETE`    | Remove a resource             |

### **RESTful API Principles**
- **Stateless**: No client context is stored on the server.
- **Client-Server Separation**: The frontend and backend should be independent.
- **Uniform Interface**: Follows a consistent structure (e.g., resource names in URLs).
- **Resource-Based URLs**: Avoid actions in URLs, use nouns instead.
  - ✅ `GET /users/123`
  - ❌ `GET /getUser?id=123`
- **Use Proper Status Codes**:
  - `200 OK` → Success
  - `201 Created` → Resource created
  - `400 Bad Request` → Invalid request
  - `401 Unauthorized` → Authentication required
  - `403 Forbidden` → Insufficient permissions
  - `404 Not Found` → Resource doesn’t exist
  - `500 Internal Server Error` → Server issue

---

## **2. API Security Best Practices**
### **Authentication & Authorization**
- **JWT (JSON Web Token)**: Used for secure API authentication.
- **OAuth 2.0**: Secure authorization framework for external access (Google, Facebook login).
- **Basic Auth**: Uses username/password (not recommended for production).
- **API Keys**: Unique tokens assigned to clients.

### **Prevent Common API Security Risks**
- **Rate Limiting**: Prevent DDoS attacks (e.g., limit `100 requests per minute` per user).
- **Input Validation**: Avoid SQL Injection and XSS attacks.
- **CORS (Cross-Origin Resource Sharing)**: Restrict API access from untrusted domains.
- **Encrypt Data**: Use **HTTPS (SSL/TLS)** for secure data transmission.

---

## **3. Designing a Good API**
### **Best Practices for API Design**
- **Use Plural Nouns for Resources**:
  - ✅ `GET /users`
  - ❌ `GET /getUserList`
- **Version Your API**:
  - ✅ `GET /api/v1/users`
- **Use Query Parameters for Filtering, Sorting, and Pagination**:
  ```bash
  GET /users?role=admin&sort=asc&page=2&size=10
  ```
- **Provide Consistent Error Responses**:
  ```json
  {
    "timestamp": "2025-03-25T14:00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "Invalid user ID",
    "path": "/api/v1/users/abc"
  }
  ```
- **Return Standardized Responses**:
  ```json
  {
    "status": "success",
    "data": {
      "id": 123,
      "name": "John Doe",
      "email": "john.doe@example.com"
    }
  }
  ```

---

## **4. Implementing APIs in Java with Spring Boot**
### **Creating a REST API with Spring Boot**
1. **Define the Model (`User.java`)**
   ```java
   @Data
   @Entity
   @Table(name = "users")
   public class User {
       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       private Long id;
       private String name;
       private String email;
   }
   ```
2. **Create Repository (`UserRepository.java`)**
   ```java
   public interface UserRepository extends JpaRepository<User, Long> { }
   ```
3. **Create Service Layer (`UserService.java`)**
   ```java
   @Service
   public class UserService {
       @Autowired
       private UserRepository repository;
       
       public List<User> getAllUsers() {
           return repository.findAll();
       }
   }
   ```
4. **Build the Controller (`UserController.java`)**
   ```java
   @RestController
   @RequestMapping("/api/v1/users")
   public class UserController {
       @Autowired
       private UserService userService;

       @GetMapping
       public ResponseEntity<List<User>> getUsers() {
           return ResponseEntity.ok(userService.getAllUsers());
       }
   }
   ```

---

## **5. Performance Optimization**
- **Use Caching (Redis, Ehcache)**: Reduce database calls.
- **Asynchronous Processing (CompletableFuture)**: Handle long-running tasks.
- **Pagination for Large Datasets**: Avoid loading millions of records at once.
- **Use GZIP Compression**: Reduce API response size.
- **Minimize Database Queries**: Use batch processing & avoid N+1 queries.

---


## **Interview Questions You Should Expect**
### **Basic Questions**
1. **What is REST, and how is it different from SOAP?**
    ## ** What is SOAP?**
        - SOAP is a **protocol** (not an architecture) for exchanging structured information in web services.
        - Uses **XML-based messaging** for request and response.
        - Requires **WSDL (Web Services Description Language)** to define the service structure.
        - Often used in **enterprise applications, banking, and payment systems**.
    
    ## ** REST vs SOAP: Key Differences**
    | Feature             | REST API | SOAP API |
    |---------------------|---------|---------|
    | **Protocol**       | Architectural style | Protocol |
    | **Format**         | JSON, XML, HTML, plain text | Only XML |
    | **Speed**         | Fast (lightweight) | Slower (heavy XML format) |
    | **Scalability**   | Highly scalable (suitable for microservices) | Less scalable |
    | **Stateless**     | Stateless (each request is independent) | Can be stateful or stateless |
    | **Security**      | Uses HTTPS, OAuth, JWT | Uses WS-Security (more secure) |
    | **Error Handling**| Uses HTTP status codes (e.g., `404 Not Found`, `500 Internal Server Error`) | Uses SOAP faults (custom error messages) |
    | **Flexibility**   | Can work with multiple formats | Strictly XML-based |
    | **Transport Protocol** | Works with HTTP, HTTPS | Works with HTTP, SMTP, TCP, etc. |
    | **Common Usage** | Web services, microservices, mobile apps | Financial transactions, banking services, legacy systems |

    Note:
    - **REST** is ideal for **modern web applications and microservices** due to its simplicity, scalability, and speed.
    - **SOAP** is preferred for **high-security, enterprise applications** like **banking, transactions, and legacy systems**.

2. **What is the purpose of API versioning?**
    ### **Purpose of API Versioning**  
    API versioning ensures **backward compatibility** while allowing **continuous improvements** in an API without breaking existing clients.  

    ### **Key Benefits:**  
    ✅ Allows **new features** without disrupting old users.  
    ✅ Supports **multiple versions** for different clients.  
    ✅ Ensures **smooth migration** from older to newer versions.  

    ### **Common API Versioning Methods:**  
    1. **URI Versioning (Most Common)**  
    ```plaintext
    GET /api/v1/users  
    GET /api/v2/users  
    ```
    2. **Header Versioning**  
    ```plaintext
    Accept: application/vnd.myapp.v1+json  
    ```
    3. **Query Parameter Versioning**  
    ```plaintext
    GET /users?version=1  
    ```
    4. **Content Negotiation (Accept Header)**  
    ```plaintext
    Accept: application/json; version=1.0  
    ```
3. **What is HATEOAS in REST APIs?**
### **What is HATEOAS in REST APIs?**  
HATEOAS (**Hypermedia as the Engine of Application State**) is a principle in REST APIs where the API responses include **links** to guide clients on possible next actions.  

### **Key Purpose:**  
✅ Makes APIs **self-descriptive** and **discoverable** without needing separate documentation.  
✅ Reduces dependency on **hardcoded API paths** in clients.  
✅ Enhances **navigation** by providing relevant actions dynamically.  

### **Example (Without HATEOAS)**  
```json
{
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com"
}
```
💡 The client must **know API endpoints** to perform further actions.

---

### **Example (With HATEOAS in Spring Boot)**  
```json
{
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com",
    "_links": {
        "self": { "href": "/users/123" },
        "update": { "href": "/users/123/update" },
        "delete": { "href": "/users/123/delete" }
    }
}
```
💡 Now, the response **guides the client** on what actions can be performed.

---

### **Spring Boot Implementation (Using Spring HATEOAS)**
```java
@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public EntityModel<User> getUser(@PathVariable Long id) {
        User user = userService.getUserById(id);
        return EntityModel.of(user,
            linkTo(methodOn(UserController.class).getUser(id)).withSelfRel(),
            linkTo(methodOn(UserController.class).updateUser(id)).withRel("update"),
            linkTo(methodOn(UserController.class).deleteUser(id)).withRel("delete")
        );
    }
}
```

--- 
### **Advanced Questions**
4. **What are the differences between synchronous and asynchronous API calls?**
### **Synchronous vs. Asynchronous API Calls**  

| Feature        | Synchronous API Call | Asynchronous API Call |
|--------------|----------------------|----------------------|
| **Definition** | Waits for the response before proceeding. | Does not wait for the response; continues execution. |
| **Blocking?** | **Blocking** (holds the thread until response is received). | **Non-blocking** (does not hold the thread). |
| **Performance** | Slower if response time is high (one request at a time). | Faster, handles multiple requests concurrently. |
| **Use Case** | When immediate response is required (e.g., **payment processing**). | When tasks can run in the background (e.g., **email sending, logging**). |
| **Implementation in Java (Spring Boot)** | Uses standard REST endpoints. | Uses `@Async`, CompletableFuture, or WebFlux (Reactive APIs). |

---

### **Example in Java (Spring Boot)**

#### **1️⃣ Synchronous API (Blocking)**
```java
@GetMapping("/sync")
public String synchronousCall() {
    return slowServiceCall();  // Waits for response before returning
}
```

#### **2️⃣ Asynchronous API (Non-blocking using `@Async`)**
```java
@Async
@GetMapping("/async")
public CompletableFuture<String> asynchronousCall() {
    return CompletableFuture.supplyAsync(() -> slowServiceCall());
}
```

💡 **Key Takeaway**:  
- **Use synchronous APIs** when order and consistency are critical.  
- **Use asynchronous APIs** when handling multiple independent tasks to improve performance.  
---
5. **How would you design an API that handles millions of requests per second?**
### **Designing a High-Performance API to Handle Millions of Requests per Second**  

To design a **scalable, high-performance API**, consider the following key areas:  

---

### **1️⃣ Use Load Balancing**  
✅ Distribute traffic across multiple servers to prevent overload.  
✅ Use **NGINX, HAProxy, AWS ELB, or Kubernetes Ingress**.  

```plaintext
Client -> Load Balancer -> Multiple API Instances
```

---

### **2️⃣ Optimize API Endpoints**  
✅ Use **lightweight JSON responses** (avoid unnecessary data).  
✅ Implement **pagination, filtering, and caching**.  

```java
@GetMapping("/users")
public ResponseEntity<List<User>> getUsers(
    @RequestParam(defaultValue = "10") int limit, 
    @RequestParam(defaultValue = "0") int offset) {
    return ResponseEntity.ok(userService.getUsers(limit, offset));
}
```

---

### **3️⃣ Caching for Faster Responses**  
✅ Use **Redis, Memcached, or CDN** to cache frequently requested data.  
✅ Reduce unnecessary database queries.  

```java
@Cacheable(value = "users", key = "#id")
public User getUserById(Long id) {
    return userRepository.findById(id).orElseThrow();
}
```

---

### **4️⃣ Asynchronous Processing & Message Queues**  
✅ Use **Kafka, RabbitMQ, or AWS SQS** for background tasks.  
✅ Handle non-critical tasks asynchronously (e.g., email sending, logging).  

```java
@Async
public void processOrder(Order order) {
    // Asynchronous processing
}
```

---

### **5️⃣ Use a Non-Blocking Reactive Stack**  
✅ **Spring WebFlux + Reactor** to handle concurrent requests efficiently.  
✅ Avoid thread blocking using **Mono & Flux**.  

```java
@GetMapping("/users")
public Flux<User> getUsers() {
    return userService.getUsers(); // Returns a non-blocking reactive stream
}
```

---

### **6️⃣ Database Optimization**  
✅ Use **Read-Replicas and Sharding** for database scaling.  
✅ Optimize queries with **Indexes, Connection Pooling, and NoSQL (MongoDB, Cassandra)** when needed.  

---

### **7️⃣ Rate Limiting & API Gateway**  
✅ Prevent API abuse with **Rate Limits** (e.g., 1000 requests/min).  
✅ Use **API Gateway** (Kong, Apigee, AWS API Gateway) to manage traffic.  

```java
@Bean
public KeyResolver userKeyResolver() {
    return exchange -> Mono.just(exchange.getRequest().getRemoteAddress().getHostName());
}
```

---

### **8️⃣ Use Microservices Architecture**  
✅ Break large applications into **smaller, scalable services**.  
✅ Each service handles a specific function (**e.g., User Service, Order Service**).  

---

### **9️⃣ Deploy with Auto-Scaling**  
✅ Use **Docker + Kubernetes** for containerized deployment.  
✅ Scale API dynamically based on traffic.  

```plaintext
Client -> Load Balancer -> API Pods (Kubernetes) -> Databases & Caches
```

---

### **🔹 Key Takeaways**  
✔ **Use Load Balancers** to distribute traffic.  
✔ **Implement Caching (Redis, CDN)** to reduce DB load.  
✔ **Go Asynchronous & Use Reactive APIs** for high throughput.  
✔ **Optimize Databases (Sharding, Replicas)** for speed.  
✔ **Enforce Rate Limiting & API Gateway** for protection.  
✔ **Deploy in a Scalable Cloud Environment** (AWS, GCP, Kubernetes).  

Would you like a **detailed example with Spring Boot implementation?** 🚀
---
