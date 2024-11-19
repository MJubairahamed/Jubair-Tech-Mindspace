# Introduction

### What it is Angular?
* Angular is an open-source framework developed by Google that uses TypeScript (Convert in JS after Compile), a JavaScript-based programming language. It includes a collection of libraries, developer tools, and a component-based framework.

### Why Angular?
* Plain Venilla JS/Jquery is hard to maintain.Angular can help developers create scalable, maintainable, and interactive web applications more efficiently and faster. It provides a **standard structure** and a set of features that can help developers avoid rebuilding code from scratch.

### Difference between AngularJs and Angular?

 | **Feature**             |**AngularJs**                              | **Angular**                                 |
|----------------------------------------------|----------------------------------------------|----------------------------------------------|
| **Architecture**          | AngularJS uses MVC or Model-View-Controller architecture, where the Model contains the business logic, Controller processes information and View shows the information present in the Model . | Angular replaces controllers with Components. **Components are nothing but directives with a predefined template**. |
| **Language**          | AngularJS uses JavaScript language, which is a dynamically typed language. | Angular uses **TypeScript** language, which is a statically typed language and is a **superset of JavaScript**. By using statically typed language, Angular provides better performance while developing larger applications.  |
| **Mobile Support**          | AngularJS does not provide mobile support.  | Angular is supported by all popular mobile browsers. |

#
### What are the different types of Complier in Angular? 
* There are 2 types of complier 
    * **JIT** – Just in Time 
        * By Default, Angular build and serves using JIT. Ex: ng build, ng serve 
    * **AOT** – Ahead of Time compilation. 
        * To use AOT, Ex: `ng build --aot`, `ng serve --aot `
    ![JIT AOT!](/Angular/Images/AOT_JIT.png "JIT AOT")

### The advantages of using AOT compilation are: 
 * Since the application compiles before running inside the browser, the browser loads the executable code and renders the application immediately, which leads to faster rendering. 
 * In AOT compilation, the compiler sends the external HTML and CSS files along with the application, eliminating separate AJAX requests for those source files, which leads to fewer ajax requests. 
 * Developers can detect and handle errors during the building phase, which helps in minimizing errors. 
 * The AOT compiler adds HTML and templates into the JS files before they run inside the browser. Due to this, there are no extra HTML files to be read, which provide better security to the application. 

### What is a Bootstrapping in Angular? 

* Bootstrapping is the process of initializing or loading our Angular application. 
* Angular takes the following steps to load our first view. 
    * Loads `Index.html` 
    * Loads Angular & Third-party libraries & Application 
    * Executes application entry point (`main.ts`) 
    * Load & execute Root Module (`app.module.ts`) 
    * Executes the Root Component (`app.component.ts`) 
    * Displayes the template (`app.component.html`) 
#
### How Angular works:
* **Angular.json**(Ealier angular-cli.json) :
    * This file will contain all the configurations of the app. While building the app, the builder looks at this file to find the entry point of the application. 
    * Entry point of the application (`Main.ts`) is declared under build section 

* **Main.ts** :
    * These two steps are performed in the following order inside the main.ts file: 
        * The main.ts file creates a browser environment for the application to run.  
        * It also calls a function called bootstrapModule, which bootstraps the application.  
        * `platformBrowserDynamic().bootstrapModule(AppModule)`

* **App Module** : 
    * The AppModule is declared in the **app.module.ts** file. This module contains declarations of all the components. 

* **App Component** :
    * This component is defined in **app.component.ts** file. This file interacts with the webpage and serves data to it. 
    * Each component is declared with three properties: 
        * **Selector** - used for accessing the component. It can be defined in 3 ways. 
            * Element Selector : **`'app-root'`** – Then uses `<app-root>` in html. 
            * Attribute Selector : **`'[app-root]'`** – Then uses `<div app-root></div>` in html. 
            * Class Selector : **'.app-root'** – Then uses `<div class="app-root"></div>` in html. 
        * **Template/TemplateURL** - Can provide inline or external template url which contains HTML of the component 
        * **StylesURL** -Can provide inline or external css file url which contains component-specific stylesheets.

* **Index.html** :
    * This file consequently calls the root component that is app-root. The root component is defined in **app.component.ts**. 
