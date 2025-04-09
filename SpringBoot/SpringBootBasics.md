### What is Spring Boot, and how is it different from Spring Framework?  
✅ **Spring Boot** is a framework that simplifies **Spring-based applications** by eliminating XML configuration, providing embedded servers, and enabling auto-configuration.  
✅ **auto-configuration** A key feature, which automatically sets up your application based on the dependencies present on the classpath.
✅ **Providing production-ready** features like metrics, health checks, and externalized configuration.

**Key Differences:**  
| Feature | Spring Framework | Spring Boot |
|---------|----------------|-------------|
| Configuration | Requires XML / Java Config | Uses auto-configuration |
| Deployment | Needs external server (Tomcat, Jetty) | Comes with embedded servers |
| Complexity | More manual setup | Less boilerplate, faster development |

📌 **Example:** Spring Boot removes the need for a `web.xml` file and allows you to start an application with a simple `main()` method.

---
###  What are the main features and advantages of using Spring Boot for application development?
1. **Auto Configuration**: Auto-configures beans based on classpath and dependencies using conditional annotations.
   - It Loads auto-configuration classes from META-INF/spring.factories, applies conditional checks, and registers qualifying beans.
2. **Embedded Servers**: Spring Boot comes with embedded servers like Tomcat, Jetty, or Undertow, so you don’t need to deploy WAR files or set up an external server.
3. **Spring Boot Actuator**: It includes built-in production-ready features like health checks, metrics, application monitoring, and externalized configuration.
4. **Starter Dependencies**: Spring Boot simplifies dependency management with a set of curated, versioned dependencies that work well together.
5. **Spring Boot CLI**: A command-line interface for running and testing Spring Boot applications quickly, allowing you to write Groovy scripts and start applications with minimal setup.
6. **Spring Boot DevTools**: Provides a set of tools to improve the development experience, such as automatic restarts, live reload, and enhanced logging, to speed up development cycles.

---

### What is the purpose of the `@SpringBootApplication` annotation? 
- `@SpringBootApplication` is a **meta-annotation** combining:  
    - `@Configuration` – Marks the class as a Spring configuration. Marks the class as a source of bean definitions for the application
context. It is equivalent to using XML configuration in traditional Spring, but in a more concise and Java-based way. 
    - `@EnableAutoConfiguration` – Enables automatic configuration based on dependencies is present in the classpath.  
    - `@ComponentScan` – Scans for Spring components (like @Controllers, @Services,@Repository).  

📌 **Example:**
```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```