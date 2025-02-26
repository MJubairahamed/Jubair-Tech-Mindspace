# Spring
---
## **🔹 Spring Basics Concepts**
**What is a Spring?**  
Spring Framework is a powerful, open-source framework for building Java applications, particularly enterprise-level applications. It provides comprehensive infrastructure support, making it easier to develop, test, and deploy Java applications. 

**Key Features of Spring Framework:**
1. **Inversion of Control (IoC)** – Uses Dependency Injection (DI) to manage object creation and dependencies.
2. **Aspect-Oriented Programming (AOP)** – Helps in separating cross-cutting concerns like logging, security, and transaction management.
3. **Spring MVC** – A framework for building web applications with a Model-View-Controller architecture.
4. **Spring Boot** – A subproject that simplifies Spring application development with auto-configuration and embedded servers.
5. **Spring Data** – Simplifies database access, working with JPA, Hibernate, and NoSQL databases.
6. **Spring Security** – Handles authentication and authorization for applications.
7. **Spring Cloud** – Supports building microservices with features like service discovery, load balancing, and circuit breakers.
8. **Spring Batch** – Facilitates batch processing of large datasets.

**Why Use Spring Framework?**
- Reduces boilerplate code with dependency injection.
- Provides a flexible, modular approach to development.
- Offers integration with various technologies like databases, messaging systems, and cloud platforms.
- Supports both monolithic and microservices architecture.

**What is a Spring Beans?**  
A **Spring Bean** is an object that is instantiated, managed, and controlled by the Spring IoC (Inversion of Control) container. Beans are the backbone of a Spring application and are defined in the Spring configuration file (XML-based or Java-based annotations).  

### **Defining a Spring Bean**
#### **1. Using XML Configuration**
```xml
<bean id="myBean" class="com.example.MyClass"/>
```

#### **2. Using Java-based Configuration**
```java
@Configuration
public class AppConfig {
    @Bean
    public MyClass myBean() {
        return new MyClass();
    }
}
```

#### **3. Using Annotations (Component Scanning)**
```java
@Component
public class MyBean {
    // Bean logic
}
```
If using `@ComponentScan`, Spring will automatically detect `@Component`, `@Service`, `@Repository`, and `@Controller` annotated classes.

---

### **Spring Bean Scopes**
Spring provides different scopes to control the lifecycle of beans:
- **Singleton (default)** – One instance per Spring container.
- **Prototype** – A new instance is created every time it is requested.
- **Request (Web Applications)** – One instance per HTTP request.
- **Session (Web Applications)** – One instance per HTTP session.
- **Application (Web Applications)** – One instance per ServletContext.
- **WebSocket (Web Applications)** – One instance per WebSocket connection.

Example of defining a prototype bean:
```java
@Bean
@Scope("prototype")
public MyClass myBean() {
    return new MyClass();
}
```
---

### **Bean Lifecycle in Spring**
Spring manages the complete lifecycle of a bean:
1. **Instantiation** – The container creates the bean instance.
2. **Dependency Injection** – Dependencies are injected into the bean.
3. **Initialization** – `@PostConstruct` or `init-method` executes.
4. **Usage** – The bean is used in the application.
5. **Destruction** – `@PreDestroy` or `destroy-method` executes before bean removal.

Example:
```java
@Component
public class MyBean {
    @PostConstruct
    public void init() {
        System.out.println("Bean is initialized.");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("Bean is about to be destroyed.");
    }
}
```
### **Does Spring Bean Provide Thread Safety**
- The default scope of the spring bean is singleton, so there will only one instance per context. That mean a class level variable that any thread can update will lead to data inconsistent. 
- To achieve thread safety either change the scope to prototype/session or Keep beans stateless,meaning they do not store instance variables. This eliminates concurrency issue.
Example:
```java
@Component
public class MyService {
    public String process(String input) {
        return "Processed: " + input;
    }
}
```

---
### **What is Spring IoC Container?**  

The **Spring IoC (Inversion of Control) Container** is responsible for managing the lifecycle, configuration, and dependencies of Spring beans. The IoC container follows the **Dependency Injection (DI)** principle to provide objects (beans) to a Spring application rather than the application manually creating them.  

### **How Does Spring IoC Work?**  
1. **Defines Beans** – Objects are defined in XML configuration, Java-based configuration, or using annotations.
2. **Manages Dependencies** – Automatically injects dependencies into beans.
3. **Controls Lifecycle** – Handles bean initialization, dependency injection, and destruction.

### **Types of IoC Containers in Spring**  

1. **BeanFactory (Lightweight Container)**  
   - The simplest container that provides basic DI support.
   - **Example:**
     ```java
     Resource resource = new ClassPathResource("beans.xml");
     BeanFactory factory = new XmlBeanFactory(resource);
     ```
   - Rarely used today, as `ApplicationContext` is preferred.

2. **ApplicationContext (Advanced Container)**  
   - A more powerful container that includes features like event propagation, declarative mechanisms, and internationalization.
   - **Common Implementations:**
     - `ClassPathXmlApplicationContext` – Loads beans from an XML configuration file.
     - `AnnotationConfigApplicationContext` – Uses Java-based configuration with `@Configuration`.
     - `WebApplicationContext` – Special version for web applications.
   - **Example:**
     ```java
     ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
     MyBean myBean = context.getBean(MyBean.class);
     ```

---
