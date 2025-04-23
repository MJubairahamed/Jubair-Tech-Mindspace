# Angular Services

### **Dependency Injection (DI)** 
- DI in Angular decouples class dependencies and centralizes creation logic.
- Services are injected via constructors using the DI framework.
- Angular manages the lifecycle, scoping, and injection of dependencies.
- The `@Injectable` decorator and DI hierarchy are key to effective use.

---

## Key Points to Understand about DI

| Key Concept | Description |
|-------------|-------------|
| **Provider** | Tells Angular how to create or supply a dependency (usually a service). |
| **Injector** | A container that holds and manages service instances. Each component has access to an injector. |
| **Hierarchy** | Angular uses a **hierarchical DI system** — services can be singleton or scoped to components depending on where they're provided. |
| **Tree-shakable** | Services provided in `root` are singleton and available app-wide; unused services can be tree-shaken during build. |
| **Injection Tokens** | Used to inject values or objects that don’t have a class type (e.g., strings, configs). |
| **Constructor Injection** | Angular injects dependencies via class constructors.


## Simple Example — Creating and Injecting a Service

### 1. **Create a Service**

```bash
ng generate service UserService
```

### 1. **Service with HTTP Call (using Promise)**

```ts
// user.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root' // Singleton service
})
export class UserService {
  constructor(private http: HttpClient) {}

  getUserById(id: number): Promise<any> {
    return this.http.get(`https://api.example.com/users/${id}`).toPromise();
  }
}
```
### 2. **Component Injecting and Using the Service**

```ts
// user.component.ts
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-user',
  template: `<div *ngIf="user">Welcome, {{ user.name }}</div>`
})
export class UserComponent implements OnInit {
  user: any;

  constructor(private userService: UserService) {}

  async ngOnInit() {
    try {
      this.user = await this.userService.getUserById(1);
    } catch (err) {
      console.error('Error fetching user:', err);
    }
  }
}
```
### 3. **Required Configuration**

Make sure `HttpClientModule` is imported once in your root module:

```ts
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule } from '@angular/common/http';
import { AppComponent } from './app.component';
import { UserComponent } from './user.component';

@NgModule({
  declarations: [AppComponent, UserComponent],
  imports: [BrowserModule, HttpClientModule],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

###  Notes for Senior Devs:
- `.toPromise()` is deprecated in RxJS 7+. For future-proof code, consider using `firstValueFrom()` or `lastValueFrom()`:
  ```ts
  import { firstValueFrom } from 'rxjs';
  return firstValueFrom(this.http.get(...));
  ```
- Stick to **Observables** unless interop with `async/await` or Promise-based APIs is specifically needed.
- Promises can't be cancelled—consider Observables for cancellable streams or reactive patterns.


Sure! Here's the same example rewritten to use **Observables**.

###  **Service with HTTP Call (Observables):**

### `user.service.ts`

```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  constructor(private http: HttpClient) {}

  getUserById(id: number): Observable<any> {
    return this.http.get(`https://api.example.com/users/${id}`);
  }
}
```

### `user.component.ts`

```ts
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-user',
  template: `<div *ngIf="user">Welcome, {{ user.name }}</div>`
})
export class UserComponent implements OnInit {
  user: any;

  constructor(private userService: UserService) {}

  ngOnInit() {
    this.userService.getUserById(1).subscribe({
      next: (data) => this.user = data,
      error: (err) => console.error('Error fetching user:', err)
    });
  }
}
```
