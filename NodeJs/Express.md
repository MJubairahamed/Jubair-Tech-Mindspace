# Express Js Noted

### What is Express.js?
Express.js is a **fast, minimalist web framework** for **Node.js**. It simplifies the process of writing server-side code by providing a thin layer of fundamental web application features without obscuring Node's capabilities. It's widely used for **creating APIs, handling HTTP requests, and serving web content** through middleware functions that can examine/modify request and response objects.

---

### **Basic Express.js Example**
```javascript
const express = require('express');
const app = express();

// Define a simple route
app.get('/', (req, res) => {
    res.send('Hello, Express.js!');
});

// Start the server
app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});
```

🔹 **Run the app:**  
```sh
npm install express  
node app.js  
```
🔹 Open **http://localhost:3000** in a browser, and it will display: **"Hello, Express.js!"**

---

### **Why Use Express.js?**  
- 🚀 **Faster Development** – Reduces boilerplate code compared to raw Node.js.  
- 🔌 **Flexible & Extensible** – Easily integrates with databases, authentication, and other Node.js packages.  
- 📡 **Great for APIs & Microservices** – Commonly used in backend development for scalable applications.  

Let's set up a **full Express.js project** from scratch, step by step. 🚀  

---
### Set up a Express.js project
- Step 1: Install Node.js & npm then verify the using version
```sh
node -v
npm -v
```
- Step 2: Create a New Express Project
  - Navigate to your project folder and initialize a new Node.js project:  
    ```sh
    mkdir my-express-app && cd my-express-app
    npm init -y
    ```
 - This creates a `package.json` file.

- Step 3: Install Express.js
  - Run the following command to install **Express.js**:
    ```sh
    npm install express
    ```
- Step 4: Create the Main Server File (`server.js`)
  - Create a new file named **`server.js`** and add the following code:

    ```javascript
    const express = require('express');
    const app = express();
    const PORT = 3000;

    // Middleware to parse JSON
    app.use(express.json());

    // Home Route
    app.get('/', (req, res) => {
        res.send('Welcome to My Express.js App!');
    });

    // Sample API Route
    app.get('/api/data', (req, res) => {
        res.json({ message: 'Hello from Express API!', status: 'Success' });
    });

    // Start Server
    app.listen(PORT, () => {
        console.log(`Server is running on http://localhost:${PORT}`);
    });
    ```
- Step 5: Run the Server
  - Start the Express.js server with:
```sh
node server.js
```
You should see:  
```sh
Server is running on http://localhost:3000
```

Open **http://localhost:3000** in your browser, and you should see:  
**"Welcome to My Express.js App!"**

- Step 7: Install Nodemon (Optional)**
For automatic server restarts during development, install **nodemon**:
```sh
npm install -g nodemon
```
Run the server with:
```sh
nodemon server.js
```
---
