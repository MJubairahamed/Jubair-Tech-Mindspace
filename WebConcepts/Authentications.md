# Web Authentications
### How do you handle API authentication in Java?
In **Java (Spring Boot)**, API authentication can be handled using:  

### **1. Basic Authentication**  
- Uses `username:password` in **HTTP headers**.  
- Example:  
  ```java
  @Configuration
  public class SecurityConfig extends WebSecurityConfigurerAdapter {
      @Override
      protected void configure(HttpSecurity http) throws Exception {
          http.csrf().disable()
              .authorizeRequests().anyRequest().authenticated()
              .and().httpBasic();
      }
  }
  ```
  
### **2. Token-Based Authentication (JWT - JSON Web Token)**  
- Secure, **stateless** authentication using tokens.  
- Steps:
  - User logs in → Server issues JWT token.
  - User sends JWT in headers (`Authorization: Bearer <token>`).
  - Server validates token before allowing access.  
- **Spring Boot JWT Example:**  
  ```java
  @GetMapping("/secure-data")
  @PreAuthorize("hasRole('USER')")
  public ResponseEntity<String> getSecureData() {
      return ResponseEntity.ok("This is a secure API");
  }
  ```

### **3. OAuth2 Authentication**  
- Used for third-party logins (**Google, Facebook, GitHub**).  
- Uses **access tokens** for authentication.  
- Example:  
  ```java
  @Configuration
  @EnableOAuth2Client
  public class OAuth2Config {
      // OAuth2 security configurations
  }
  ```

### **4. API Key Authentication**  
- Uses an **API Key** in headers or query params.  
- Example:  
  ```java
  @GetMapping("/data")
  public ResponseEntity<String> getData(@RequestHeader("X-API-KEY") String apiKey) {
      if (!"MY_SECRET_KEY".equals(apiKey)) {
          return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Invalid API Key");
      }
      return ResponseEntity.ok("Authorized data");
  }
  ```


### Difference Between Cookies, Sessions, JWT, and PASETO in Web Authentication

| Feature | Cookies | Sessions | JWT (JSON Web Tokens) | PASETO (Platform-Agnostic Security Tokens) |
|---------|---------|----------|----------------------|-------------------------------------------|
| **Storage Location** | Client-side (browser) | Server-side with client reference | Client-side | Client-side |
| **How It Works** | Small data pieces stored in the browser | Server stores session data with ID reference in cookie | Self-contained token with encoded payload | Similar to JWT but with stronger cryptographic standards |
| **Stateful/Stateless** | Can be either | Stateful | Stateless | Stateless |
| **Data Access** | Sent automatically with requests to same domain | Session ID maps to server-stored data | All data encoded in token itself | All data encoded in token itself |
| **Security Features** | HttpOnly, Secure, SameSite flags | Relies on secure cookie transmission | Signature verification, expiration | Versioned protocol, modern crypto, no algorithm confusion |
| **Expiration** | Set via Expires/Max-Age attributes | Configurable server-side | Encoded in token payload | Encoded in token payload |
| **Use Cases** | Simple data storage, session references | Traditional web applications | Modern APIs, microservices | High-security requirements |
| **Pros** | • Simple to implement<br>• Built into browsers<br>• Can be secured well with proper flags | • Sensitive data stays on server<br>• Easy to invalidate<br>• Good for complex session data | • Stateless<br>• Portable across domains<br>• Contains all needed data<br>• Good for microservices | • Enhanced security<br>• Removes JWT algorithm vulnerabilities<br>• Standardized formats<br>• Future-proof cryptography |
| **Cons** | • Size limitations<br>• Vulnerable to CSRF attacks<br>• Privacy concerns | • Server storage overhead<br>• Scaling challenges<br>• Session fixation risks | • Can't be invalidated easily<br>• Payload increases size<br>• Algorithm confusion attacks | • Newer, less adoption<br>• Fewer libraries/support<br>• Slightly more complex |
| **Implementation** | `Set-Cookie` HTTP header | Session middleware + cookies | Sign/verify with secret or public/private keys | Use specialized PASETO libraries |


#### When comparing authentication methods in web applications:

 - **Cookies** are simple client-side storage mechanisms handled automatically by browsers. They're easy to implement but have size limitations and CSRF vulnerabilities. They typically store a session ID or small pieces of data.

 - **Sessions** use server-side storage with a reference (usually in a cookie) sent to the client. The server maintains all user data while the client only has an identifier. This offers better security for sensitive data but creates scaling challenges in distributed systems.

 - **JWT (JSON Web Tokens)** are self-contained tokens that include all necessary information encoded and signed within the token itself. They're ideal for stateless authentication in modern APIs and microservices. The main advantages are portability across domains and no server storage requirements, but they can't be easily invalidated once issued.

 - **PASETO (Platform-Agnostic Security Tokens)** is a more secure alternative to JWT, addressing several JWT security concerns. It uses modern cryptographic standards, has a versioned protocol, and eliminates algorithm confusion attacks. While offering enhanced security, PASETO has less adoption and fewer libraries available than JWT.
 ![Different Authentication!](/image/Authentication_ss.png "Authentication")

---
###  what is CSRF vulnerabilities and how to over come it
**CSRF (Cross-Site Request Forgery)** is an attack where a malicious website tricks a logged-in user into unknowingly submitting a request to another website where they have privileges (e.g., transferring money).  

#### **How to Prevent CSRF in JavaScript:**  
1. **Use CSRF Tokens** – Generate a unique token for each request and verify it on the server.  
2. **SameSite Cookies** – Set cookies with `SameSite=Strict` or `SameSite=Lax` to prevent cross-origin requests.  
3. **Referer & Origin Checks** – Validate the `Referer` and `Origin` headers in incoming requests.  
4. **User Authentication** – Require re-authentication for sensitive actions.  
5. **Use CORS Properly** – Restrict allowed domains and HTTP methods.  

**Example in Express.js (CSRF Token Implementation):**  
```javascript
const csrf = require('csurf');
const cookieParser = require('cookie-parser');

app.use(cookieParser());
app.use(csrf({ cookie: true }));

app.get('/form', (req, res) => {
    res.json({ csrfToken: req.csrfToken() });
});

app.post('/submit', (req, res) => {
    res.send('CSRF-protected request successful');
});
```
This ensures every form submission includes a valid CSRF token, blocking unauthorized requests. 
---