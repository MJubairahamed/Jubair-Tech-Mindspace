## Anatomy of a component
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
### Imports of a component
* To use a component, directive, or pipe, you must add it to the imports array in the @Component decorator:`imports: [ProfilePhoto]`

#### Note:
* In Angular versions prior to **19.0.0**, when creating a component, directive, or pipe, you had to explicitly set the standalone property to true if you wanted it to be standalone. If you didn't specify the standalone property, it would default to false, meaning the component, directive, or pipe would be considered part of an NgModule.


# Selector
* **Angular matches selectors statically at compile-time.** Changing the DOM at run-time, either via Angular bindings or with DOM APIs, does not affect the components rendered.
* **An element can match exactly one component selector.** If multiple component selectors match a single element, Angular reports an error.
* **Component selectors are case-sensitive**.

### Type of Selectors
    | **Selector Type**          |**Description**                                                 | **Examples**                                 |
    |----------------------------|----------------------------------------------------------------|----------------------------------------------|
    | **Type selector**          | Matches elements based on their HTML tag name, or node name. . | profile-photo |
    | **Attribute selector**     | Matches elements based on the presence of an HTML attribute and, optionally, an exact value for that attribute. |[dropzone] [type="reset"]  |
    | **Class selector**          | Matches elements based on the presence of a CSS class.  | .menu-item |

#### Notes:
* Angular component selectors do not support **combinators & namespaces**.
* Angular component selectors supports :not pseudo-class.
* You can combine multiple selectors by concatenating them. 
    * For example, you can match <button> elements that specify type="reset": `selector: 'button[type="reset"]',`
    * You can also define multiple selectors with a comma-separated list: `selector: 'drop-zone, [dropzone]'`

# Style
### Style Scoping
* Every component has a view encapsulation setting that determines how the framework scopes a component's styles. There are three view encapsulation modes: Emulated, ShadowDom, and None.

    #### **ViewEncapsulation.Emulated**
    - **Default Mode in Angular**: Encapsulates styles so that they only apply to the component's template.
    - **How it Works**:
        - Angular generates a unique HTML attribute for the component.
        - This attribute is applied to template elements and CSS selectors.
    - **Key Features**:
        - Component styles **don’t leak** to other components.
        - **Global styles** can still affect the component.
        - Supports `:host` and `:host-context()` pseudo-classes by transforming them into attributes (not native behavior).
        - **Limitations**: Does not support Shadow DOM pseudo-classes like `::shadow` or `::part`.
    - **Special Case - ::ng-deep**:
        - Used to **disable encapsulation** for a CSS rule, making it global.
        - Strongly discouraged for new development; retained only for backward compatibility.

    #### **ViewEncapsulation.ShadowDom**
    - **Uses Web Standard Shadow DOM API**:
        - Styles are **strictly scoped** to the component.
        - Global styles **cannot affect** the component, and vice versa.
    - **How it Works**:
        - Angular attaches a **shadow root** to the component's host element.
        - Template and styles are rendered in the **shadow tree**.
    - **Key Features**:
        - Guarantees **style isolation** for the component.
        - Affects event propagation, `<slot>` API behavior, and browser developer tools.
 
    #### **ViewEncapsulation.None**
    - This mode **disables all style** encapsulation for the component. Any styles associated with the component behave as global styles.

    - **Caution**: Understand the implications before using Shadow DOM, as it impacts rendering and interaction.