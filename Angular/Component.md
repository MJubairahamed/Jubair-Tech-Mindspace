# Introduction

### Anatomy of a component
* Every component must have:
    * A **TypeScript** class with behaviors such as handling user input and fetching data from a server
    * An **HTML template** that controls what renders into the DOM
    * A **CSS** selector that defines how the component is used in HTML

* Provide Angular-specific information for a component by adding a @Component decorator on top of the TypeScript class.
* The object passed to the @Component decorator is called **the component's metadata**. This includes the selector, template, and other properties described throughout this guide.

### Inline template and External File template declaration
* Inline template:
  ```
    @Component({`
        `selector: 'profile-photo',
        template: '<img src="profile-photo.jpg" alt="Your profile photo">',
        styles: 'img { border-radius: 50%; }',
    })
    export class ProfilePhoto { }
    ```
* External Reference:
    ```
    @Component({
    selector: 'profile-photo',
    templateUrl: 'profile-photo.html',
    styleUrl: 'profile-photo.css',
    })
    export class ProfilePhoto { }
    ```