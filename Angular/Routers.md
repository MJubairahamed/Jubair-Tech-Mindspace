# Routing Concepts

### What is forRoot() and forChild()? 
 - `forRoot()` 
    - It is for the **root module to initialize routing and create the main Router**.
    - It ensures there's only one Router instance for your entire application, which is crucial for consistency. 
    - The `forRoot()` method supplies the **service providers and directives** needed for routing, and performs the initial navigation based on the current browser URL.
    - Example:
          ```TS 
            import { NgModule } from '@angular/core';
            import { RouterModule, Routes } from '@angular/router';
            import { HomeComponent } from './home/home.component';

            const routes: Routes = [];

            @NgModule({
            imports: [RouterModule.forRoot(routes)],
            exports: [RouterModule, HomeComponent, Headers]
            })
            export class AppRoutingModule { }
            ```
 - `forChild()` 
    - It is for **child modules to register routes using the existing Router**. 
    - It allows for lazy loading of modules without needing to reinitialize the Router.

### What is The <router-outlet> ?
 - The `<router-outlet>` tells the router where to display routed views.
 - The RouterOutlet is one of the router directives that became available to the AppComponent because AppModule imports AppRoutingModule which exported RouterModule.

### What is routerlink?
- Enables navigation between routes within a single-page application. 
- Creates clickable elements that trigger navigation to a specific route. 
```TS
    <nav>
        <a routerLink="/heroes">Heroes</a>
        <a [routerLink]="'/home'">Home</a>
    </nav>
```
### Different way to add router path in angular?
Absolutely! Here's the rephrased version in a **table format with thick borders**, showing the **type of routing** and the **description/example**.

| **🧭 Type of Routing** | **📌 Description / Example** |
|:----------------------:|:-----------------------------|
| **Basic Route Configuration** | `RouterModule.forRoot()` with a static array of routes.<br>`{ path: 'about', component: AboutComponent }` |
| **Lazy Loading Modules** | Loads modules on demand for better performance.<br>`{ path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }` |
| **Child / Nested Routes** | Define child routes inside a module.<br>`{ path: '', component: LayoutComponent, children: [...] }` |
| **Redirect and Wildcard Routes** | Redirect or handle unknown paths.<br>`{ path: '', redirectTo: '/home', pathMatch: 'full' }`<br>`{ path: '**', component: NotFoundComponent }` |
| **Route with Parameters** | Supports dynamic values.<br>`{ path: 'profile/:id', component: ProfileComponent }`<br>Access via `paramMap.get('id')` |
| **Query Parameters** | Add optional parameters.<br>Navigate with `this.router.navigate(['/search'], { queryParams: { q: 'test' } })` |
| **Route Guards** | Protect routes with `canActivate`, `canLoad`, etc.<br>`{ path: 'admin', component: AdminComponent, canActivate: [AuthGuard] }` |
| **Route Metadata / Data** | Pass static data to routes.<br>`{ path: 'dashboard', component: DashboardComponent, data: { title: 'Dashboard' } }`<br>Access via `route.snapshot.data['title']` |

