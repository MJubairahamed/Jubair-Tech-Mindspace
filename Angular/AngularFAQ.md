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