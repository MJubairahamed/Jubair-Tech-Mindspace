### **Key Annotations in Spring Boot and Their Usage**  

**important Spring Boot annotations** and their **usage**:  

| **Annotation** | **Usage** | **Example** |
|--------------|----------|------------|
| `@SpringBootApplication` | Marks the main application class and enables auto-configuration. | `@SpringBootApplication public class MyApp { public static void main(String[] args) { SpringApplication.run(MyApp.class, args); } }` |
| `@Component` | Marks a generic Spring-managed bean. | `@Component public class MyComponent { }` |
| `@Service` | Marks a **service layer** class (business logic). | `@Service public class UserService { }` |
| `@Repository` | Marks a **DAO (Data Access Object)** class and enables exception translation. | `@Repository public class UserRepository { }` |
| `@Controller` | Marks a **Spring MVC controller** (for returning views). | `@Controller public class HomeController { @GetMapping("/") public String home() { return "index"; } }` |
| `@RestController` | A combination of `@Controller` and `@ResponseBody` for REST APIs. | `@RestController public class UserController { @GetMapping("/users") public List<User> getUsers() { return userService.getAllUsers(); } }` |
| `@RequestMapping` | Maps HTTP requests to a controller method (supports all HTTP methods). | `@RequestMapping("/users") public class UserController { }` |
| `@GetMapping` | Handles **HTTP GET** requests. | `@GetMapping("/{id}") public User getUser(@PathVariable int id) { return userService.getUser(id); }` |
| `@PostMapping` | Handles **HTTP POST** requests. | `@PostMapping("/") public void createUser(@RequestBody User user) { userService.createUser(user); }` |
| `@PutMapping` | Handles **HTTP PUT** requests (update resource). | `@PutMapping("/{id}") public void updateUser(@PathVariable int id, @RequestBody User user) { userService.updateUser(id, user); }` |
| `@DeleteMapping` | Handles **HTTP DELETE** requests. | `@DeleteMapping("/{id}") public void deleteUser(@PathVariable int id) { userService.deleteUser(id); }` |
| `@PathVariable` | Extracts a value from the URL. | `@GetMapping("/{id}") public User getUser(@PathVariable int id) { return userService.getUser(id); }` |
| `@RequestParam` | Extracts query parameters from the request. | `@GetMapping("/users") public List<User> getUsers(@RequestParam String name) { return userService.findByName(name); }` |
| `@RequestBody` | Maps request body to a Java object (for JSON data). | `@PostMapping("/") public void createUser(@RequestBody User user) { }` |
| `@ResponseBody` | Converts Java object to JSON response. | `@ResponseBody public User getUser() { return new User(1, "John"); }` |
| `@Autowired` | Injects a Spring bean automatically. | `@Service public class UserService { @Autowired private UserRepository userRepository; }` |
| `@Qualifier` | Resolves conflicts when multiple beans of the same type exist. | ```java 
    interface Animal {}

    @Component("cat")
    class Cat implements Animal {}

    @Component("dog")
    class Dog implements Animal {}

    @Service
    class AnimalService {
        @Autowired
        @Qualifier("cat")
        private Animal animal;
    }``` |
| `@Primary` | Marks a bean as the primary candidate for autowiring. | `@Primary @Component public class PrimaryBean { }` |
| `@Value` | Injects values from properties files. | `@Value("${app.name}") private String appName;` |
| `@Configuration` | Marks a class as a **Spring configuration class**. | `@Configuration public class AppConfig { @Bean public RestTemplate restTemplate() { return new RestTemplate(); } }` |
| `@Bean` | Declares a Spring bean explicitly inside a `@Configuration` class. | `@Bean public RestTemplate restTemplate() { return new RestTemplate(); }` |
| `@ComponentScan` | Tells Spring to scan a package for components. | `@ComponentScan("com.example")` |
| `@EnableAutoConfiguration` | Enables automatic Spring Boot configuration. | `@EnableAutoConfiguration` |
| `@Transactional` | Ensures that a method runs within a transaction. | `@Transactional public void transferMoney() { debitAccount(); creditAccount(); }` |
| `@Cacheable` | Caches the method result. | `@Cacheable("users") public User getUser(int id) { return userRepository.findById(id); }` |
| `@Scheduled` | Runs a method at fixed intervals (cron jobs). | `@Scheduled(fixedRate = 5000) public void logTime() { System.out.println(new Date()); }` |
| `@Async` | Runs a method asynchronously in a separate thread. | `@Async public void sendEmail() { // Asynchronous email sending logic }` |
| `@PreAuthorize` | Applies method-level security based on roles. | `@PreAuthorize("hasRole('ADMIN')") public void deleteUser() { }` |

---

### **🔹 Key Takeaways**
✅ `@RestController`, `@RequestMapping`, `@GetMapping` → **For REST APIs**  
✅ `@Service`, `@Repository`, `@Component` → **For Business & DAO Layers**  
✅ `@Autowired`, `@Bean`, `@Value` → **For Dependency Injection**  
✅ `@Transactional`, `@Cacheable`, `@Async` → **For Performance & DB Handling**  
✅ `@Scheduled`, `@PreAuthorize` → **For Scheduling & Security**  
