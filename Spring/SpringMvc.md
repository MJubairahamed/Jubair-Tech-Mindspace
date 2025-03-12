# Spring MVC Concepts

### **What is a Controller in Spring MVC?**  

In **Spring MVC**, a **Controller** is a key component that handles incoming HTTP requests, processes them, and returns responses. It acts as an intermediary between the **Model** (business logic/data) and the **View** (UI). Controllers are typically annotated with `@Controller` or `@RestController` to define request-handling logic.

### **Key Annotations in Spring MVC Controllers**  

1. **`@Controller`** – Marks a class as a Spring MVC controller that returns **view templates (JSP, Thymeleaf, etc.)**.
2. **`@RestController`** – A specialized version of `@Controller` that returns **JSON or XML responses** (used in REST APIs).
3. **`@RequestMapping`** – Maps HTTP requests to specific handler methods.
4. **`@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`** – Shortcut annotations for HTTP methods.
5. **`@RequestParam`, `@PathVariable`** – Used to extract parameters from the request.

### **Example of a Spring MVC Controller**
#### **1. Using `@Controller` (Returns a View)**
```java
@Controller
@RequestMapping("/user")
public class UserController {

    @GetMapping("/welcome")
    public String welcomePage(Model model) {
        model.addAttribute("message", "Welcome to Spring MVC!");
        return "welcome";  // Returns "welcome.jsp" or "welcome.html"
    }
}
```
- Maps `GET /user/welcome` to `welcomePage()`.
- Adds data to the `Model` object.
- Returns a view name (resolved by `ViewResolver`).

-
#### **2. Using `@RestController` (Returns JSON Response)**
```java
@RestController
@RequestMapping("/api/users")
public class UserRestController {

    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable int id) {
        User user = new User(id, "John Doe", "john@example.com");
        return ResponseEntity.ok(user); // Returns JSON response
    }
}
```
- Maps `GET /api/users/{id}` to `getUser()`.
- Extracts `id` from the URL using `@PathVariable`.
- Returns a JSON response instead of a view.

---

