## Angular Overview Cheatsheet


### 1. **Angular Basics**
- **What is Angular?**: A platform and framework for building single-page client applications using HTML and TypeScript.
-   **Components**: Core building blocks of Angular applications. Define logic and view.
-   **Modules**: Containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities.
-   **Templates**: HTML along with Angular-specific syntax for dynamic views.

### 2. **Data Binding**
-   **Interpolation**: `{{ expression }}` used for embedding dynamic values in HTML.
-   **Property Binding**: `[property]="expression"` used to bind component properties to HTML elements.
-   **Event Binding**: `(event)="handler"` used to bind component methods to events in HTML elements.
-   **Two-way Binding**: `[(ngModel)]="property"` used to synchronize data between the model and the view.

### 3. **Directives**
- **Directives** are a fundamental feature that allow you to extend the behavior of HTML elements and **reuse common functionality across multiple components**.
- **Component Directives**
	-   **Definition**: These are the most common type of directives. They are essentially Angular components.
	-   **Purpose**: To control a patch of the screen called a view.
	-   **Usage**: Created using the `@Component` decorator.
 - **Structural Directives**
	-   **Definition**: These directives change the structure of the DOM by adding or removing elements.
	-   **Common Directives**: `*ngIf`, `*ngFor`, `*ngSwitch`.
-   **Attribute Directives**
	-   **Definition**: These directives change the appearance or behavior of an element, component, or another directive.
	-   **Common Directives**: `ngClass`, `ngStyle`, `[ngModel]`.

### 4. **Decorators**

 - Decorators are special functions that attach metadata to classes, properties, methods, and parameters.
 - **Class Decorators**
	-	Class decorators are used to declare a class and provide metadata for the class.
	-	**Example: `@Component` and `@NgModule`**
 - **Property Decorators**
	- Property decorators are used to declare metadata for properties inside a class.
	- **Example: `@Input` and `@Output`**
-  **Method Decorators**
	 - Method decorators are used to declare metadata for methods inside a
	   class.
	  - **Example: `@HostListener`**
- **Parameter Decorators**
	- Parameter decorators are used to declare metadata for parameters inside a class constructor.
	- **Example: `@Inject`**

### 5. **Services and Dependency Injection**
-   **Services**: Used to share data or logic across components.
-   **Dependency Injection**: Design pattern to pass dependencies (services) to components and other services.

### 6. **Routing and Navigation**
-   **RouterModule**: Configures routes in Angular.
-   **Routes**: Defines how the application should navigate between different components.
-   **RouterLink**: Directive for navigation links.
-   **ActivatedRoute**: Provides information about the route associated with a component.
-  **Wildcard Route**
	-   **Purpose**: To handle navigation to undefined or non-existent routes.
	-   **Configuration**: The wildcard route is defined using the path `**` and should be the last route in the routing configuration, as Angular routes are evaluated in the order they are defined.
- **Routing Guards**
	- **Def:** Routing guards are used to control access to routes in an Angular application. There are several types of routing guards.
	-   **CanActivate**: Determines if a route can be activated.
	-   **CanActivateChild**: Determines if child routes can be activated.
	-   **CanDeactivate**: Determines if a route can be deactivated.
	-   **CanLoad**: Determines if a module can be loaded.
	- **Usage:** These guards implement interfaces and define methods to provide control over route navigation. They are typically used for authentication, authorization, and preventing unsaved changes from being lost.

### 7. **Forms**
-   **Template-driven Forms**: simpler and more suited for smaller forms with basic validation.
	-  **FormsModule**: Import `FormsModule` from `@angular/forms` in your module to use template-driven forms.
	-   **ngModel**: Binds form controls to properties in the component.
	-   **ngForm**: Automatically tracks the state of the form and its controls.
	-  **Two-Way Data Binding**: Use `[(ngModel)]` to bind form controls to component properties.
	-   **Validation**: Angular provides built-in validation directives (`required`, `minlength`, etc.) and custom validators.
-   **Reactive Forms**: Use a more robust, scalable, and testable approach with FormBuilder, FormGroup, and FormControl.
	-  **ReactiveFormsModule**: Import `ReactiveFormsModule` from `@angular/forms` in your module to use reactive forms.
	-   **FormControl**: Represents a single form control.
	-   **FormGroup**: Represents a group of form controls.
	-   **FormBuilder**: A service that simplifies the creation of form groups and controls.

### 8. **HTTP Client**
-   **HttpClientModule**: Provides mechanisms to communicate with backend services over HTTP.
-   **HttpClient**: Service for making HTTP requests (GET, POST, PUT, DELETE).
- **HTTP Interceptor**
	-  **Purpose**: Interceptors sit between the application and the backend server, allowing you to intercept and modify HTTP requests and responses.
	-   **Usage**: Commonly used for adding authentication tokens, handling errors, and logging HTTP traffic.
	- **Registration in module**:
    providers: [ { 
        provide: HTTP_INTERCEPTORS, 
        useClass: AuthInterceptor, 
        multi: true // This is crucial to allow multiple interceptors 
        }],

### 9. **Lifecycle Hooks**

 -  **ngOnChanges**
    -   **When it’s called**: Invoked before `ngOnInit` and whenever one or more data-bound input properties change.
    -   **Usage**: Use it to act upon changes to input properties from a parent component.
    -   **Signature**: `ngOnChanges(changes: SimpleChanges): void`
    
  -  **ngOnInit**
	    -   **When it’s called**: Called once, after the first `ngOnChanges`.
	    -   **Usage**: Initialize the component, set up logic that relies on input properties, and fetch data.
	    -   **Signature**: `ngOnInit(): void`
    
   - **ngDoCheck**
	    -   **When it’s called**: Called during every change detection run, immediately after `ngOnChanges` and `ngOnInit`.
	    -   **Usage**: Detect and act upon changes that Angular doesn't detect automatically.
	    -   **Signature**: `ngDoCheck(): void`
    
-    **ngAfterContentInit**
	    -   **When it’s called**: Called once after Angular projects external content into the component’s view (ng-content).
	    -   **Usage**: Respond after Angular projects external content into the component.
	    -   **Signature**: `ngAfterContentInit(): void`
    
-    **ngAfterContentChecked**
	    -   **When it’s called**: Called after every check of the component's or directive's content.
	    -   **Usage**: Act upon changes in the projected content.
		   -   **Signature**: `ngAfterContentChecked(): void`
    
-    **ngAfterViewInit**
	    -   **When it’s called**: Called once after Angular initializes the component’s views and child views.
	    -   **Usage**: Initialize logic that depends on the component’s view or child views being fully initialized.
	    -   **Signature**: `ngAfterViewInit(): void`
    
-    **ngAfterViewChecked**
	    -   **When it’s called**: Called after every check of the component's views and child views.
	    -   **Usage**: Respond after Angular checks the component's views and child views.
	    -   **Signature**: `ngAfterViewChecked(): void`
    
-    **ngOnDestroy**
	    -   **When it’s called**: Called just before Angular destroys the component or directive.
	    -   **Usage**: Clean up logic, unsubscribe from observables, detach event handlers to avoid memory leaks.
	    -   **Signature**: `ngOnDestroy(): void`

### 10. **Pipes**

-   **Built-in Pipes**: `DatePipe`, `CurrencyPipe`, `UpperCasePipe`, etc., used for transforming data in templates.
-   **Custom Pipes**: User-defined pipes for specific transformations.

### 11. **Angular CLI**

-   **Commands**: `ng generate`, `ng serve`, `ng build`, etc., used for generating components, services, etc., and for serving and building the application.
