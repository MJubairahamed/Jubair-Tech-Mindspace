### **Implementing OAuth2 in Spring Boot**  

OAuth2 allows users to authenticate via third-party providers like **Google, GitHub, Facebook**, etc. Here’s how you can implement it in **Spring Boot** using **Spring Security**.

---

## **1️⃣ Add Dependencies (`pom.xml`)**  
Add the required dependencies for Spring Security and OAuth2.  

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

---

## **2️⃣ Configure OAuth2 Provider (Google as an Example)**
Add your OAuth provider details in `application.yml` or `application.properties`.

### **🔹 Using `application.yml`**
```yaml
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: YOUR_GOOGLE_CLIENT_ID
            client-secret: YOUR_GOOGLE_CLIENT_SECRET
            scope: profile, email
```

To get **Client ID** and **Client Secret**, register your app at [Google Developer Console](https://console.developers.google.com/).

---

## **3️⃣ Configure Security (`SecurityConfig.java`)**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests()
            .requestMatchers("/", "/login").permitAll()
            .anyRequest().authenticated()
            .and()
            .oauth2Login(); // Enables OAuth2 login
        
        return http.build();
    }
}
```
- The `/` and `/login` endpoints are publicly accessible.  
- Other requests require authentication via OAuth2.  

---

## **4️⃣ Create a Simple Controller (`AuthController.java`)**
```java
import org.springframework.security.oauth2.core.user.OAuth2User;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.Map;

@RestController
@RequestMapping("/user")
public class AuthController {
    @GetMapping
    public Map<String, Object> getUser(OAuth2User user) {
        return user.getAttributes(); // Returns user details from OAuth provider
    }
}
```
- After authentication, this endpoint returns user details (e.g., name, email).  

---

## **5️⃣ Running and Testing**  
1. Start your Spring Boot app:  
   ```sh
   mvn spring-boot:run
   ```
2. Open **http://localhost:8080/login** → Redirects to Google login.  
3. After logging in, test the `/user` endpoint:  
   ```sh
   GET http://localhost:8080/user
   ```
   **Response:**  
   ```json
   {
      "name": "John Doe",
      "email": "johndoe@gmail.com",
      "picture": "https://example.com/profile.jpg"
   }
   ```

---

## **🔹 Summary**
✅ Users log in via **Google OAuth2**  
✅ Spring Security manages authentication  
✅ `/user` endpoint retrieves authenticated user details  

Would you like to **integrate other providers** like GitHub or **secure APIs with JWT tokens** after OAuth login? 🚀