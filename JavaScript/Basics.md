# JavaScript Basics
---

### **1. Introduction to JavaScript**  
- JavaScript is an **interpreted** programming language based on **ECMAScript**.  
- It is **prototype-based, dynamic, imperative, and weakly typed**.  
- Mainly used for **client-side web development**, but also found in **server-side applications (SSJS)** and other environments like **PDFs and desktop widgets**.  

---

### **2. History of JavaScript**  
- Created by **Brendan Eich** at **Netscape** in 1995.  
- Originally named **Mocha**, then **LiveScript**, before being renamed **JavaScript** to align with Java’s rising popularity.  
- Standardized as **ECMAScript (ES)** in **1997**, evolving through versions like ES5, ES6, and beyond.  

---

### **3. Uses of JavaScript**  
- Enhances **web interactivity** through **event handling, form validation, dynamic content loading, animations, and AJAX requests**.  
- Used in **front-end frameworks** (React, Angular, Vue) and **back-end environments** (Node.js).  
- Supports **real-time applications**, including stock tickers, sports scores, and chat applications.  

---

### **4. JavaScript and the DOM (Document Object Model)**  
- **DOM scripting** allows developers to **manipulate HTML and CSS** dynamically.  
- Enables **interactive web elements**, such as **dropdowns, modal popups, and live content updates**.  
- Uses **event listeners** to respond to **user actions like clicks, scrolls, and keystrokes**.  

---

### **5. Modern JavaScript Features (ES6+)**  
- **Arrow functions** for concise syntax.  
- **`let` and `const`** for better variable scoping.  
- **Template literals** for easy string interpolation.  
- **Promises & Async/Await** for handling asynchronous operations.  
- **Modules (`import/export`)** for better code organization.  

---

### **6. JavaScript and HTML**  
- JavaScript extends **HTML functionalities**, allowing **dynamic content updates**.  
- Can be embedded using:  
  - **Inline scripting (`<script>` tag in HTML)**.  
  - **External files (`.js` files linked in HTML)**.  
- Works with **events** like `onClick`, `onLoad`, and `onChange`.  

---

### **7. JavaScript and CSS**  
- JavaScript can dynamically **modify CSS properties** using the **style object**.  
- Supports **pseudo-elements** via JavaScript.  
- Can **load stylesheets dynamically** or add CSS rules at runtime.  
- Example:  
  ```js
  document.getElementById("box").style.backgroundColor = "blue";
  ```  

---

### **8. JavaScript and AJAX**  
- **Asynchronous JavaScript and XML (AJAX)** allows data retrieval from servers **without refreshing the page**.  
- Used for **live search, real-time updates, and single-page applications (SPA)**.  
- Example using `fetch()`:  
  ```js
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data));
  ```  

---

### **9. JavaScript and jQuery**  
- **jQuery** simplifies **DOM manipulation, event handling, and AJAX calls**.  
- Example:  
  ```js
  $("#button").click(function() {
    $("#text").hide();
  });
  ```  
- Though still in use, **modern JavaScript frameworks have reduced reliance on jQuery**.  

---

### **10. JavaScript Events & Event Listeners**  
- JavaScript uses **event-driven programming** to handle user interactions.  
- Example of adding an event listener:  
  ```js
  document.getElementById("btn").addEventListener("click", function() {
    alert("Button clicked!");
  });
  ```  
- Common events: `click`, `mouseover`, `keydown`, `scroll`, `load`, etc.  

---

### **11. JavaScript Functions & Closures**  
- Functions in JavaScript can be **named, anonymous, or arrow functions**.  
- **Closures** allow functions to **retain access to variables outside their scope**.  
- Example:  
  ```js
  function outer() {
    let count = 0;
    return function inner() {
      count++;
      console.log(count);
    };
  }
  const counter = outer();
  counter(); // 1
  counter(); // 2
  ```  

---

### **12. JavaScript Objects & Prototypes**  
- JavaScript follows a **prototype-based inheritance model**.  
- Objects can inherit methods via **prototypes**.  
- Example:  
  ```js
  function Person(name) {
    this.name = name;
  }
  Person.prototype.sayHello = function() {
    console.log("Hello, " + this.name);
  };
  const user = new Person("Alice");
  user.sayHello(); // "Hello, Alice"
  ```  

---

### **13. JavaScript Data Types & Type Coercion**  
- JavaScript is **loosely typed**, meaning variables can change types dynamically.  
- **Primitive types**: `String`, `Number`, `Boolean`, `Null`, `Undefined`, `Symbol`, `BigInt`.  
- **Reference types**: `Object`, `Array`, `Function`. 
- Type Coercion:
    - Type coercion in JavaScript refers to the automatic conversion of values from one data type to another during operations or comparisons. This implicit conversion happens when JavaScript expects a value of a certain type but receives a different one.
- Example of **type coercion**:  
  ```js
  console.log("5" + 2);  // "52" (string)
  console.log("5" - 2);  // 3 (number)
  ```  

---

### **14. JavaScript Scope & Hoisting**  
- **Scope**: Determines the accessibility of variables (`global`, `function`, `block`).  
- **Hoisting**: Variables and function declarations are moved to the top during execution.  
- Example:  
  ```js
  console.log(x); // undefined (due to hoisting)
  var x = 10;
  ```  

---

### **15. JavaScript Async Programming (Promises & Callbacks)**  
- **Callbacks**: Functions passed as arguments to execute after a task.  
- **Promises**: Handle asynchronous operations (`pending`, `fulfilled`, `rejected`).  
- **Async/Await** simplifies promise handling.  
- Example:  
  ```js
  async function fetchData() {
    let response = await fetch("https://api.example.com");
    let data = await response.json();
    console.log(data);
  }
  ```  

---

### **16. JavaScript Security Best Practices**  
- Avoid **`eval()`** due to security risks, because it makes code injection bugs possible.  
- Use **`Content Security Policy (CSP)`** to prevent XSS attacks.  
- Always **validate user inputs**.  

---

### **17. JavaScript Modules & Import/Export**  
- **ES6 modules** allow code organization across multiple files.  
- Example:  
  ```js
  // File: math.js
  export function add(a, b) { return a + b; }

  // File: main.js
  import { add } from './math.js';
  console.log(add(2, 3)); // 5
  ```  

---

### **18. JavaScript Memory Management & Performance**  
- **Garbage collection** automatically frees unused memory.  
- Optimize performance by **reducing memory leaks** and using **efficient loops** (`forEach`, `map`).  

---

### **19. JavaScript Frameworks & Libraries**  
- **Popular Front-End Frameworks**: React, Angular, Vue.js.  
- **Back-End with Node.js**: JavaScript can run **server-side applications**.  
- **Hybrid App Development**: JavaScript powers **React Native, Ionic, and Electron**.  

---

### **20. JavaScript Best Practices**  
- Use **`const` and `let`** instead of `var`.  
- Follow **modular coding** with separate files.  
- Use **strict mode (`"use strict"`)** for cleaner code.  
    -  It enforce stricter parsing and error handling on the code at runtime. It helps to write cleaner code and catch errors and bugs that might otherwise go unnoticed.
- Write **self-documenting code** with meaningful variable and function names.  

---
### **21. The Future of JavaScript**  
- JavaScript is evolving with **new ES6+ features**, making it more powerful and efficient.  
- Expanding into **AI, IoT, and Blockchain applications**.  
- Continuous improvements in **browser engines and JavaScript performance**.  

---