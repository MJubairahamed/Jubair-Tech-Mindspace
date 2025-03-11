
## **🔹 Core Spring Boot Questions**  

### ** What is Spring Boot, and how is it different from Spring Framework?**  
✅ **Spring Boot** is a framework that simplifies **Spring-based applications** by eliminating XML configuration, providing embedded servers, and enabling auto-configuration.  
    ✅ **auto-configuration** A key feature enabling this is Auto Configuration, which automatically sets up your application based on the dependencies present on the classpath.
✅ **Providing production-ready** features like metrics, health checks, and externalized configuration.

**Key Differences:**  
| Feature | Spring Framework | Spring Boot |
|---------|----------------|-------------|
| Configuration | Requires XML / Java Config | Uses auto-configuration |
| Deployment | Needs external server (Tomcat, Jetty) | Comes with embedded servers |
| Complexity | More manual setup | Less boilerplate, faster development |

📌 **Example:** Spring Boot removes the need for a `web.xml` file and allows you to start an application with a simple `main()` method.

---

### ** What is the purpose of the `@SpringBootApplication` annotation?**  
- `@SpringBootApplication` is a **meta-annotation** combining:  
- `@Configuration` – Marks the class as a Spring configuration.  
- `@EnableAutoConfiguration` – Enables automatic configuration based on dependencies.  
- `@ComponentScan` – Scans for Spring components (like controllers, services).  

📌 **Example:**
```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
---
### **Spring Boot Internal Flow**

1. **Initialization**: Main class with `@SpringBootApplication` starts the application, combining `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.
   - Entry point method calls `SpringApplication.run()` which begins the bootstrapping process.

2. **Spring Application Context Creation**: Creates application context to manage beans and dependencies.
   - It Builds environment, creates appropriate context type, prepares context with environment settings, then scans for components.

3. **Auto Configuration**: Auto-configures beans based on classpath and dependencies using conditional annotations.
   - It Loads auto-configuration classes from META-INF/spring.factories, applies conditional checks, and registers qualifying beans.

4. **Externalized Configuration**: Loads configuration from property files, environment variables, and command-line arguments.
   - It Creates PropertySources, loads values in order of precedence, binds them to configuration properties beans.

5. **Embedded Web Server Initialization**: For web applications, initializes and configures embedded web server.
   - It Detects web environment, creates server factory, configures connector properties, then starts server.

6. **Application Startup**: Invokes lifecycle callbacks and initialization methods on beans.
   - It Instantiates beans, injects dependencies, calls `@PostConstruct` methods, and executes other initialization callbacks.

7. **Application Ready**: Application context fully initialized and ready to handle requests.
   - It Publishes ApplicationReadyEvent, completes startup logging, and begins accepting client requests.
---

### ** What is the difference between `@Component`, `@Service`, and `@Repository`?**  
✅ All three are **Spring-managed beans**, but they have different use cases:  

| Annotation | Purpose |
|------------|---------|
| `@Component` | is the generic stereotype annotation that marks a class as a Spring-managed component.  It's the parent annotation that @Service and @Repository inherit from. Use this when a class doesn't fit into any specialized category.|
| `@Service` | indicates that a class performs business logic or calculations. It's functionally identical to @Component but communicates to developers that this class contains service-layer logic like transaction management, validation, or orchestration of multiple repositories. `@Service public class UserService { } ` |
| `@Repository` | designates a class that interacts with a database or other data store.Exception translation: Automatically converts persistence-specific exceptions into Spring's unified DataAccessException hierarchy.`@Repository public class UserRepository { } ` |

---

### ** How does Spring Boot handle exceptions globally?**  
- Spring Boot provides mechanisms for handling exceptions globally across the application using @ControllerAdvice and @ExceptionHandler annotations.
- `@ControllerAdvice`: This annotation enables a class to act as a global exception handler for all controllers. Any exception that is thrown within a controller will be caught by a method annotated with @ExceptionHandler inside a @ControllerAdvice class.
- `@ExceptionHandler`: This annotation is used within a @ControllerAdvice class to define methods that handle specific types of exceptions. It takes the exception class as an argument, specifying which exception type the method should handle.

📌 **Example:**
```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleResourceNotFoundException(ResourceNotFoundException ex) {
        ErrorResponse errorResponse = new ErrorResponse(HttpStatus.NOT_FOUND.value(), ex.getMessage());
        return new ResponseEntity<>(errorResponse, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneralException(Exception ex) {
       ErrorResponse errorResponse = new ErrorResponse(HttpStatus.INTERNAL_SERVER_ERROR.value(), "An unexpected error occurred");
        return new ResponseEntity<>(errorResponse, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```
- Note: In this example, GlobalExceptionHandler class handles ResourceNotFoundException and general Exception. When `ResourceNotFoundException ` is thrown, the handleResourceNotFoundException method will be invoked, returning a 404 Not Found response. If any other exception occurs, the handleGeneralException method will be invoked, returning a 500 Internal Server Error response.

---

## **🔹 REST API & Security Questions**  

### ** How do you create a REST API in Spring Boot?**  
✅ Use `@RestController` with `@RequestMapping`.  

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
📌 **Response:**  
```
GET /users/1  → { "id": 1, "name": "John Doe" }
```

---

### ** What are the different types of authentication in Spring Security?**  
# Types of Authentication in Spring Security

## Form-Based Authentication
- Uses HTML forms for credentials collection
- Default login page provided by Spring Security
- Session-based authentication 
- Good for traditional web applications

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .formLogin(form -> form
                .loginPage("/login")
                .permitAll()
            )
            .authorizeHttpRequests(authorize -> authorize
                .requestMatchers("/public/**").permitAll()
                .anyRequest().authenticated()
            );
        return http.build();
    }
}
```

## HTTP Basic Authentication
- Uses HTTP Authorization header
- Credentials sent with every request
- Simple implementation for APIs
- No session management required

```java
@Configuration
@EnableWebSecurity
public class BasicAuthConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .httpBasic(Customizer.withDefaults())
            .authorizeHttpRequests(authorize -> authorize
                .anyRequest().authenticated()
            );
        return http.build();
    }
}
```

## OAuth 2.0 / OpenID Connect
- Industry standard protocol for authorization
- Supports authentication delegation to identity providers
- Used for single sign-on and API access
- Handles various grant types (authorization code, client credentials, etc.)

```java
@Configuration
@EnableWebSecurity
public class OAuth2LoginConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .oauth2Login(oauth2 -> oauth2
                .loginPage("/login")
                .defaultSuccessUrl("/home")
            )
            .authorizeHttpRequests(authorize -> authorize
                .anyRequest().authenticated()
            );
        return http.build();
    }
}
```

## JWT Authentication
- Stateless authentication using JSON Web Tokens
- Token contains encoded claims about the user
- No server-side session storage needed
- Good for microservices and APIs

```java
@Configuration
@EnableWebSecurity
public class JwtSecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .addFilterBefore(new JwtAuthenticationFilter(), UsernamePasswordAuthenticationFilter.class)
            .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(authorize -> authorize
                .requestMatchers("/api/auth/**").permitAll()
                .anyRequest().authenticated()
            );
        return http.build();
    }
}
```

## Remember-Me Authentication
- Allows returning users to be automatically authenticated
- Uses persistent tokens or cookies
- Enhances user experience for frequent visitors

```java
@Configuration
@EnableWebSecurity
public class RememberMeConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .formLogin(Customizer.withDefaults())
            .rememberMe(rememberMe -> rememberMe
                .key("uniqueAndSecretKey")
                .tokenValiditySeconds(86400) // 1 day
            )
            .authorizeHttpRequests(authorize -> authorize
                .anyRequest().authenticated()
            );
        return http.build();
    }
}
```

## LDAP Authentication
- Integrates with LDAP directories for authentication
- Common for enterprise environments
- Supports Active Directory integration
- Can be combined with other authentication methods

```java
@Configuration
@EnableWebSecurity
public class LdapSecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(authorize -> authorize
                .anyRequest().authenticated()
            )
            .formLogin(Customizer.withDefaults());
        return http.build();
    }
    
    @Bean
    public EmbeddedLdapServerContextSourceFactoryBean contextSourceFactoryBean() {
        EmbeddedLdapServerContextSourceFactoryBean factory = 
            EmbeddedLdapServerContextSourceFactoryBean.fromEmbeddedLdapServer();
        factory.setPort(0);
        return factory;
    }
    
    @Bean
    public LdapBindAuthenticationManagerFactory authenticationManagerFactory(
            BaseLdapPathContextSource contextSource) {
        LdapBindAuthenticationManagerFactory factory = new LdapBindAuthenticationManagerFactory(contextSource);
        factory.setUserDnPatterns("uid={0},ou=people");
        return factory;
    }
}
```

---

### **8️⃣ How do you implement role-based access control in Spring Boot?**  
✅ Use `@PreAuthorize` for **method-level security**.  

📌 **Example:**
```java
@PreAuthorize("hasRole('ADMIN')")
@GetMapping("/admin")
public String adminPage() {
    return "Admin Content";
}
```
**Only ADMIN users can access this API.**

---

## **🔹 Database & JPA Questions**  

### **9️⃣ What is the difference between `CrudRepository`, `JpaRepository`, and `PagingAndSortingRepository`?**  

| Repository Type | Features |
|----------------|---------|
| `CrudRepository` | Basic CRUD methods (`save()`, `findById()`) |
| `JpaRepository` | Extends `CrudRepository`, adds `flush()` and batch operations |
| `PagingAndSortingRepository` | Provides **pagination & sorting** methods |

📌 **Example:**
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
}
```

---

### **🔟 How do you implement pagination in Spring Boot?**  
✅ Use `Pageable` with `JpaRepository`.  

📌 **Example:**
```java
@GetMapping("/users")
public Page<User> getUsers(Pageable pageable) {
    return userRepository.findAll(pageable);
}
```
📌 **Request Example:**  
```
GET /users?page=0&size=10&sort=name,asc
```

---

## **🔹 Microservices & Cloud Questions**  

### **1️⃣1️⃣ What is Spring Cloud, and why is it used?**  
✅ **Spring Cloud** provides tools to build **distributed systems** with features like:  
- **Service Discovery** (`Eureka`)  
- **Load Balancing** (`Ribbon`, `Spring Cloud LoadBalancer`)  
- **Circuit Breakers** (`Resilience4j`)  
- **API Gateway** (`Spring Cloud Gateway`)  

---

### **1️⃣2️⃣ How does Spring Boot handle inter-service communication?**  
✅ Using **RestTemplate (Legacy)** or **WebClient (Modern, Non-blocking)**.  

📌 **Example (WebClient):**
```java
WebClient client = WebClient.create("http://user-service");
User user = client.get().uri("/users/1").retrieve().bodyToMono(User.class).block();
```

---

### **1️⃣3️⃣ How do you implement Circuit Breaker in Spring Boot?**  
✅ Using **Resilience4j** to prevent cascading failures.  

📌 **Example:**
```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallback")
public String getUser() {
    return restTemplate.getForObject("http://user-service/users/1", String.class);
}

public String fallback(Throwable t) {
    return "User Service is down, please try later";
}
```

---

## **🔹 Other Advanced Questions**  

### **1️⃣4️⃣ How do you secure sensitive configurations in Spring Boot?**  
✅ Use **Spring Cloud Config + Vault** or **Environment Variables**.  

---

### **1️⃣5️⃣ How do you optimize a slow Spring Boot application?**  
✅ **Optimize SQL Queries, Enable Caching, Use Connection Pooling (HikariCP), Compress Responses, Use Profiling Tools.**  

---

### **1️⃣6️⃣ How does Spring Boot handle transactions?**  
✅ Using `@Transactional`.  

📌 **Example:**
```java
@Transactional
public void transferMoney(Long fromAcc, Long toAcc, Double amount) {
    debit(fromAcc, amount);
    credit(toAcc, amount);
}
```
If any method fails, **the entire transaction rolls back**.

---

## **🔹 Final Questions (Behavioral & Best Practices)**  

### **1️⃣7️⃣ What are best practices for designing REST APIs?**  
✅ Use **proper status codes**, **versioning**, **pagination**, **JWT for security**, and **HATEOAS**.  

### **1️⃣8️⃣ How do you handle large file uploads in Spring Boot?**  
✅ Use `MultipartFile` and configure `spring.servlet.multipart.max-file-size`.  

---

## **🔥 Final Thoughts**  
This set of **25+ high-impact questions** covers:  
✅ **Spring Boot Core**  
✅ **REST APIs & Security**  
✅ **Microservices & Cloud**  
✅ **Database & Performance**  

Would you like **mock interview practice** based on these questions? 🚀