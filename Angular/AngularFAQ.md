# Angular FAQ's

### **Difference between Promise and Observables in angular**

- In Angular (and JavaScript/TypeScript in general), **Promises** and **Observables** are both used for handling asynchronous operations—but they differ significantly in terms of functionality, flexibility, and use cases. Here's a clear comparison:

| Feature | **Promise** | **Observable** |
|--------|-------------|----------------|
| Library | Built-in JavaScript (ES6) | Provided by RxJS (used in Angular) |
| Value Emission | Emits a **single** value | Emits **multiple** values over time |
| Execution | Executes immediately when created | Executes only when subscribed |
| Cancellability | Cannot be cancelled | Can be cancelled using `unsubscribe()` |
| Operators | Limited (`then`, `catch`) | Rich set of RxJS operators (`map`, `filter`, `retry`, etc.) |
| Laziness | Eager (starts right away) | Lazy (starts on subscription) |
| Error Handling | `.catch()` handles errors | Powerful error handling via RxJS (`catchError`, `retry`, etc.) |
| Use Case | Suitable for one-time async tasks like HTTP requests | Ideal for streams, event handling, real-time data |
| Composition | Limited chaining | Advanced chaining and transformation using operators |

### Example

**Promise:**
```typescript
getData(): Promise<any> {
  return fetch('api/data').then(res => res.json());
}
```

**Observable (Angular Way):**
```typescript
getData(): Observable<any> {
  return this.http.get<any>('api/data');
}
```

### **What is DDependency Injection (DI) in angular?**
- Dependency Injection (DI) in Angular is a design pattern where a class requests dependencies from external sources rather than creating them itself. It's a core concept in Angular that promotes loose coupling, modularity, and testability. 
- Instead of a component creating its dependencies, such as services, Angular's DI framework provides these dependencies when the component is instantiated. This is achieved through **injectors and providers**. 
- **Injectors** are responsible for creating and managing dependencies, while **providers** configure how these dependencies are created. 

### What is @ViewChild and @ViewChildren? 
- ViewChild or ViewChildren is used to  get the local reference of you template inside your component to change the behavior &  appearance of the template.  
- syntax:  static param is introduced from Angular 8 only `@ViewChild('nameInput',{static:false}) nameInputRef: ElementRef; `

### What is @ViewChild and @ContentChild? 
## @ViewChild

- Access a child component, directive, or DOM element from the **same component's template**.
- Use it when you want to interact with elements/components **defined inside the template** (view DOM).

### Example:
```ts
@ViewChild('myInput') inputRef!: ElementRef;

ngAfterViewInit() {
  console.log(this.inputRef.nativeElement.value);
}
```
```html
<input #myInput type="text" value="Angular Dev" />
```
## @ContentChild

- Access content projected into a component using `<ng-content>`.
- Use when you’re writing a component that receives content **from its parent**, like a wrapper or layout component.

### Example:
```ts
@ContentChild('projectedContent') contentRef!: ElementRef;

ngAfterContentInit() {
  console.log(this.contentRef.nativeElement.textContent);
}
```
```html
<custom-wrapper>
  <p #projectedContent>This is projected content</p>
</custom-wrapper>
```
###  Quick Comparison

| Feature        | `@ViewChild`                | `@ContentChild`              |
|----------------|-----------------------------|------------------------------|
| **Target**     | Inside component's own view | Content passed via `<ng-content>` |
| **Lifecycle Hook** | `ngAfterViewInit()`        | `ngAfterContentInit()`        |
| **Use Case**   | Access template refs, child components | Access slotted/projection content |

### What is @ViewChildren and @ContentChildren? 

## @ViewChildren 

- **What:** Used to **query multiple elements, directives, or components** present in the **same view (template)**.
- **When to Use:** When you want to access or manipulate **multiple DOM elements** or **child components** inside the template.

### Example

```ts
@ViewChildren('inputRef') inputs!: QueryList<ElementRef>;

ngAfterViewInit() {
  this.inputs.forEach(input => console.log(input.nativeElement.value));
}
```
```html
<input #inputRef type="text" value="One" />
<input #inputRef type="text" value="Two" />
```
## @ContentChildren
- Used to **query multiple projected elements** passed into a component using `<ng-content>`.
- When building **reusable components** (like tabs, cards, modals) that accept child components/content from outside.

### Example
```ts
@ContentChildren(HighlightDirective) highlights!: QueryList<HighlightDirective>;

ngAfterContentInit() {
  this.highlights.forEach(dir => dir.highlight('yellow'));
}
```
```html
<app-highlight-wrapper>
  <p appHighlight>Projected 1</p>
  <div appHighlight>Projected 2</div>
</app-highlight-wrapper>
```
## Summary Table

| Feature             | `@ViewChildren`                          | `@ContentChildren`                         |
|---------------------|-------------------------------------------|---------------------------------------------|
| **Scope**            | Same component's template               | Projected content (`<ng-content>`)         |
| **Lifecycle Hook**   | `ngAfterViewInit()`                     | `ngAfterContentInit()`                     |
| **Type**             | `QueryList<T>`                          | `QueryList<T>`                             |
| **Common Use Case**  | Manipulating multiple DOM elements or directives inside a component's template | Working with slotted components like tabs, accordions, content wrappers |
