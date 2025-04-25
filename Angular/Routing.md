# Routing Concepts

### What is Routing?
- The Angular Router enables navigation from one view to the next as users perform application tasks.

### How to enable Routing in Angular?
- The appRoutes is the const which holds the array of routes. The approutes will be the Routes type from angular.
- Add RouterModule in import and Pass the above routes in to the RouterModule.forRoot(appRoutes) method.
- Then at last add the <router-outlet>  directive.

### How to create Child Routing?
- In app.routing.module.ts add the children similar to following code.
```ts {path: 'profile', component: ProfileComponent,
        children: [
            {path: 'accounts',   component: AccountsComponent},
            {path: 'personalinfo',component: PersonalInfoComponent}
        ]
    }
``` 
- Children data type is array so we can declare similar to Routes array.
- One Important point to note , Add <router-outlet> tag in the profile html. Then only Angular identify and plugin the child code. 

### What is RouterLink?
- It is another option to route the page from one to another.
- Ex:  `<a routerLink="/home">Home</a>`
- The / is used to absolute path otherwise it. We can add the without "/" for nested route which relative path.

### What is RouterLinkActive and RouterLinkActiveOptions?
- RouterLinkActive is used to enable the selected tabs as active.
- RouterLinkActiveOptions is used to fix or change the default active tab behavior. routerLinkActiveOptions="{exact: true}".

### What is ActivatedRoute?
- An ActivatedRoute is an object that contains information about route parameters, query parameters and URL fragments.
- Inject ActivatedRoute in the constructor.
- Example:
```TS
    this.activatedRoute.queryParams.subscribe(params => {

    this.openAccountOrchId = params['goalID'];

    });
```
### How to pass parameter to Routes ?
- By adding ":"  in path which tell angular that what given after the colon is parameter.
- Ex: `{path: 'user/:id', component : UserComponent}`
- id token in the path is a placeholder. That creates a slot in the path for a Route Parameter. In this case, the router will insert the id of a user into that slot. 

### How to Fetch the params value reactively?
- This mean based on some action or service response (Async) value the URL parameter might get changed.so that data object should be updated accordingly.
- This approach is used to get the updated user object If the params modified with in the component.
- Ex:
```TS
    this.route.params

    .subscribe((params:Params)=> {

    this.user.id = params['id'];

    });
```
 
### How to add queryparam in route?
- We can add query param in routerLink as like follows
- `<a [routerLink]="['/server']" [queryParams]="{Pin: '1234'} fargment='loading' href="#"></a>`
- Fargment is used to add '#' after the query param.
- Query Param through component like follows,
- `This.router.navigate(['/server',id,'edit'],{queryParams: {Pin:'123'}, fargment='loading'});`

### How to fetch queryparam in route?
- Need to inject the ActivatedRoute in constructor.
- There are 2 approach to fetch the query param similar to params
- Snapshot - this.route.snapshot.queryparams;
- Observables
    - `this.route.queryparams.subscribe();`
    - `this.route.fargment.subscribe();`

### What is queryParamHandling?
- It is a property used to retain the query param by using preserved or  override with new through merged property
- `this.router.navigate(['edit'], {relativeTo, this.route, queryParamHandling:'Preserved');`

### How to implement wild card redirect?
- Wild card Redirect is used to navigate to the error page. ** is the wildcard key which will parse the  router top to bottom.
- So Important point to note is wild entry should use in the last routing array.
- `{path:'**',redirectTo: '/error'}`

### What are Route Guards?
- Angular’s route guards are interfaces which can tell the router whether or not it should allow navigation to a requested route.
- There are five different types of guards and each of them is called in a particular sequence. The router’s behavior is modified differently depending on which guard is used.
- The guards are:
    - CanActivate
    - CanActivateChild
    - CanDeactivate - guard used to protect navigate away from the current page.
    - CanLoad
    - Resolve

### How to implement CanActivate to route guard?
- Create a guard service which should implement the CanActivate Interface.
- Implement the CanActivate method with following param "routea: ActivatedRouteSnapshot" & "state: RouterStateSnapShot".
- CanActivate method will return boolean.
- So in app.routing.modules, Add the following to guard the each routing canActivate: [AccessGuard]

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

