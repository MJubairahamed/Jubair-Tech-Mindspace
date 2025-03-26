
## **🔹 Core Spring Boot Questions**  


---
### Spring Boot Internal Flow

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

### How does Spring Boot handle exceptions globally?
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

### What is ResponseEntity<>?
- **ResponseEntity<T>** represents the entire HTTP response, including the status code, headers, and body. It offers a way to fully customize the response sent to the client. The generic type T specifies the type of the response body. It is commonly used in RESTful web services to provide more control over the response than simply returning the data directly. 

---

## **🔹 REST API & Security Questions**  

### How do you create a REST API in Spring Boot?
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

### What are the different types of authentication in Spring Security?
- Form-Based Authentication
- HTTP Basic Authentication
- OAuth 2.0 / OpenID Connect
- JWT Authentication
### Form-Based Authentication
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
- Credentials sent with every request.
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
---

### ** How do you implement role-based access control in Spring Boot?**  
✅ Use `@PreAuthorize` for **method-level security**.  

📌 **Example:** **Only ADMIN users can access this API.**
```java
@PreAuthorize("hasRole('ADMIN')")
@GetMapping("/admin")
public String adminPage() {
    return "Admin Content";
}
```
---

## **🔹 Database & JPA Questions**  

### ** What is the difference between `CrudRepository`, `JpaRepository`, and `PagingAndSortingRepository`?**  

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

### ** How do you implement pagination in Spring Boot?**  
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

### ** What is Spring Cloud, and why is it used?**  
✅ **Spring Cloud** provides tools to build **distributed systems** with features like:  
- **Service Discovery** (`Eureka`)  
- **Load Balancing** (`Ribbon`, `Spring Cloud LoadBalancer`)  
- **Circuit Breakers** (`Resilience4j`)  
- **API Gateway** (`Spring Cloud Gateway`)  

---

### ** How does Spring Boot handle inter-service communication?**  
✅ Using **RestTemplate (Legacy)** or **WebClient (Modern, Non-blocking)**.  

📌 **Example (WebClient):**
```java
WebClient client = WebClient.create("http://user-service");
User user = client.get().uri("/users/1").retrieve().bodyToMono(User.class).block();
```

---

### ** How do you implement Circuit Breaker in Spring Boot?**  
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

### ** How do you secure sensitive configurations in Spring Boot?**  
✅ Use **Spring Cloud Config + Vault** or **Environment Variables**.  

---

### ** How do you optimize a slow Spring Boot application?**  
✅ **Optimize SQL Queries, Enable Caching, Use Connection Pooling (HikariCP), Compress Responses, Use Profiling Tools.**  

---

### ** How does Spring Boot handle transactions?**  
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

### ** What are best practices for designing REST APIs?**  
✅ Use **proper status codes**, **versioning**, **pagination**, **JWT for security**, and **HATEOAS**.  

### ** How do you handle large file uploads in Spring Boot?**  
✅ Use `MultipartFile` and configure `spring.servlet.multipart.max-file-size`.  

---
### ** How manage different environments in Spring Boot?**  
✅ Use `profile` and configure `spring.profile.active=dev or test`. Use Spring profiles (application-dev.properties, application-prod.properties) for environment-specific configurations, activated by SPRING_PROFILES_ACTIVE.