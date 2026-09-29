# Angular Master Roadmap — Modern Integrated Edition (Reviewer Improved)

**Philosophy:** Learn the conceptual foundation first, practice modern Angular as the primary implementation, learn legacy patterns to read existing code.

***
- 🍉 [[Master instruction for Angular Roadmap (arfcV2.2)]].
***

# Module 0 — TypeScript Essentials (Angular-Focused)

## Lesson 0.1 — TypeScript Fundamentals

* What is TypeScript?
* Why Angular uses TypeScript
* Installing TypeScript
* Compiling `.ts` files

## Lesson 0.2 — Basic Types

* Variables and type annotations
* Primitive types (string, number, boolean)
* Type inference
* `any` and `unknown`

## Lesson 0.3 — Advanced Types

* Union types
* Intersection types
* Optional properties
* Null/undefined handling
* Type narrowing
* Type assertions

## Lesson 0.4 — Collections & Generics

* Arrays
* Tuples
* Generics
* Generic constraints

## Lesson 0.5 — Objects & Interfaces

* Objects
* Interfaces
* Type aliases
* When to use interface vs type

## Lesson 0.6 — Functions

* Function signatures
* Optional and default parameters
* Rest parameters
* Arrow functions
* Function overloading

## Lesson 0.7 — Classes

* Classes and constructors
* Properties and methods
* Access modifiers (public, private, protected)
* `readonly`
* Getters and setters
* Static members

## Lesson 0.8 — Inheritance & Advanced OOP

* Inheritance
* `super` keyword
* Generics in classes
* Type parameters

## Lesson 0.9 — Utility Types (Critical for Angular)

* `Partial<T>`
* `Pick<T, K>`
* `Omit<T, K>`
* `Record<K, V>`
* `Readonly<T>`

## Lesson 0.10 — Modules & Imports/Exports

* ES6 modules
* `import` and `export`
* Named vs default exports
* Re-exporting with `export *`

***

# Module 1 — Angular Fundamentals

## Lesson 1.1 — What is Angular?

* Single Page Application (SPA) concept
* Angular as a frontend framework
* Angular architecture overview
* Component-based architecture
* Evolution context (NgModules → Standalone → Signals)

## Lesson 1.2 — Setup & Modern Project Structure

* Installing Node.js and npm
* Installing Angular CLI
* Creating a standalone project
* Modern project structure
  * `src/main.ts` (bootstrapping entry point)
  * `src/app/app.component.ts` (root component)
  * `src/app/app.routes.ts` (routing configuration)
  * `angular.json` (CLI configuration)
  * `tsconfig.json` (TypeScript configuration)

## Lesson 1.3 — Modern Bootstrap Pattern

* `bootstrapApplication()` (modern way)
* Provider configuration
* Understanding providers
* Legacy bootstrapping (NgModule) for reference

## Lesson 1.4 — Development & Production

* Development server
* Hot module replacement (HMR)
* Production build
* Bundle optimization

***

# Module 2 — Components & Component Communication

## Lesson 2.1 — Component Fundamentals

* What is a component?
* Component parts (selector, template, styles, logic)
* Single Responsibility Principle
* Component tree architecture

## Lesson 2.2 — Standalone Components

* Creating standalone components
* `standalone: true` flag
* `imports` array
* When to use standalone

## Lesson 2.3 — Component Lifecycle

* Component lifecycle hooks
* `ngOnInit` (most important)
* `ngOnDestroy` (cleanup)
* `ngOnChanges` (input changes)
* Other lifecycle hooks

## Lesson 2.4 — Component Inputs

* `@Input()` decorator
* Parent to child communication
* Input properties
* Input validation

## Lesson 2.5 — Component Outputs & Events

* `@Output()` decorator
* `EventEmitter`
* Child to parent communication
* Event passing

## Lesson 2.6 — Signal-Based Inputs/Outputs (Preview)

* `input()` function
* `output()` function
* Modern alternative to decorators

## Lesson 2.7 — Generating Components

* `ng generate component` (CLI)
* Understanding generated files
* Modifying boilerplate

## Lesson 2.8 — Component Encapsulation

* View encapsulation
* Style scoping
* DOM projection

***

# Module 3 — Templates & Modern Control Flow

## Lesson 3.1 — Data Binding Fundamentals

* String interpolation `{{ }}`
* Property binding `[ ]`
* Event binding `( )`
* Two-way binding `[( )]`
* Attribute binding

## Lesson 3.2 — Class & Style Binding

* `[class]` binding
* `[class.name]` binding
* `[ngClass]` (legacy reference)
* `[style]` binding
* `[ngStyle]` (legacy reference)

## Lesson 3.3 — Modern Control Flow: @if

* `@if` / `@else` / `@else if`
* Conditional rendering
* Performance benefits over `*ngIf`
* Legacy `*ngIf` (reference only)

## Lesson 3.4 — Modern Control Flow: @for

* `@for` loop syntax
* `track` function (critical)
* Loop context variables
* Performance optimization with track
* Legacy `*ngFor` (reference only)

## Lesson 3.5 — Modern Control Flow: @switch

* `@switch` / `@case` / `@default`
* Multi-way conditionals
* Legacy `*ngSwitch` (reference only)

## Lesson 3.6 — Template Variables & References

* Local template variables `#variable`
* `$index`, `$first`, `$last`, `$even`, `$odd`
* Template reference variables
* `ViewChild` decorator

## Lesson 3.7 — Pipes

* What are pipes?
* Built-in pipes (currency, date, uppercase, lowercase, json, slice)
* Chaining pipes
* Custom pipes (overview)

***

# Module 4 — Signals & Reactive State

## Lesson 4.1 — Introduction to Signals

* What is a Signal?
* Why Signals exist (explicit change tracking)
* Signal vs plain properties
* Mental model and benefits

## Lesson 4.2 — Creating & Using Signals

* Creating signals: `signal(initialValue)`
* Reading values: `signal()`
* Setting values: `signal.set(value)`
* Updating values: `signal.update(fn)`

## Lesson 4.3 — Signals in Components

* Using signals in component class
* Reading in templates: `{{ signal() }}`
* Updating with event handlers
* Reactive rendering

## Lesson 4.4 — Computed Signals

* `computed()` function
* Automatic dependency tracking
* Memoization (caching)
* Derived values and composition

## Lesson 4.5 — Effects (Side Effects with Caution)

* What is `effect()`?
* Proper use cases (localStorage, logging, DOM APIs)
* Anti-patterns with effects
* Why NOT to use effects for data loading

## Lesson 4.6 — Arrays & Immutability

* Signals with arrays
* Immutable updates
* `.set()` with spread operator
* `.update()` pattern

## Lesson 4.7 — Signals in Services (Preview)

* Services managing state with Signals
* Exposing signals to components
* Computed derived values in services

***

# Module 5 — Directives & Pipes

## Lesson 5.1 — Understanding Directives

* Types of directives
* Structural directives
* Attribute directives
* Components as directives

## Lesson 5.2 — Built-in Attribute Directives

* `[ngClass]`
* `[ngStyle]`
* Common attribute patterns

## Lesson 5.3 — Creating Custom Directives

* `@Directive()` decorator
* Modifying element behavior
* `ElementRef` and `Renderer2`
* Directive inputs and outputs

## Lesson 5.4 — Creating Custom Pipes

* `@Pipe()` decorator
* `PipeTransform` interface
* Transform logic
* Using custom pipes in templates

## Lesson 5.5 — Advanced Pipe Concepts

* Stateful pipes
* Pure vs impure pipes
* Performance considerations

***

# Module 6 — Forms: Three Approaches

## Lesson 6.1 — Forms Overview

* Three form approaches
* When to use each
* Form state and validation
* Submission handling

## Lesson 6.2 — Template-Driven Forms

* `FormsModule` and `ngModel`
* Two-way binding in forms
* Form validation (built-in validators)
* Pros and cons
* When to use

## Lesson 6.3 — Reactive Forms

* `ReactiveFormsModule` and `FormBuilder`
* `FormGroup` and `FormControl`
* Form structure in component
* Validators configuration
* Advanced validation

## Lesson 6.4 — Signal Forms (Modern, v21+)

* Signal-based form API
* Strong typing
* Integration with Signals
* When to use Signal Forms

## Lesson 6.5 — Form Validation

* Built-in validators
* Custom validators
* Cross-field validation
* Showing validation errors
* Dynamic validation

## Lesson 6.6 — Dynamic Forms

* Building forms programmatically
* Adding/removing fields at runtime
* Complex form structures

***

# Module 7 — Services & Dependency Injection

## Lesson 7.1 — What is a Service?

* Service concept
* Business logic encapsulation
* Shared data management
* Testability and reusability

## Lesson 7.2 — Creating Services (Modern `inject()`)

* `@Injectable()` decorator
* `inject()` function (modern way)
* Constructor injection (legacy reference)
* Dependency requirements

## Lesson 7.3 — Dependency Injection Scopes

* `providedIn: 'root'` (singleton)
* `providedIn: ComponentName` (component-scoped)
* `providers: []` in component (local)
* Choosing the right scope

## Lesson 7.4 — Services with Signals (State Management)

* Services managing UI state with Signals
* Exposing signals to components
* `computed()` in services
* Separation of concerns

## Lesson 7.5 — Advanced Service Patterns

* Service inheritance
* Factory services
* Interceptor services (preview)

***

# Module 8 — RxJS Essentials for Angular (NEW — CRITICAL)

## Lesson 8.1 — Understanding Observables

* What is an Observable?
* Observables vs Promises vs Signals
* Asynchronous streams concept
* When to use Observables

## Lesson 8.2 — Creating & Subscribing

* Creating observables
* `subscribe()` method
* next, error, complete callbacks
* Subscription object

## Lesson 8.3 — Preventing Memory Leaks

* Unsubscribe in `ngOnDestroy`
* `async` pipe in templates
* `takeUntil()` operator
* Subscription management patterns

## Lesson 8.4 — The `pipe()` Operator

* Chaining operators
* Operator composition
* Pipeline concept

## Lesson 8.5 — Common Operators: Transformation

* `map()` — transform values
* `filter()` — keep matching values
* `tap()` — perform side effects

## Lesson 8.6 — Common Operators: Stream Control

* `switchMap()` — replace stream
* `mergeMap()` — merge streams
* `concatMap()` — serialize streams

## Lesson 8.7 — Common Operators: Error Handling

* `catchError()` — handle errors
* `retry()` — retry failed requests
* Error propagation

## Lesson 8.8 — Common Operators: Utility

* `debounceTime()` — wait before emitting
* `throttleTime()` — limit frequency
* `distinct()` — remove duplicates
* `take()` — limit number of emissions

## Lesson 8.9 — Converting Observables to Signals

* `toSignal()` function
* Observable in template with async pipe
* When to convert vs keep as Observable

## Lesson 8.10 — Observables in Services

* HTTP returning Observables
* Service exposing Observables
* Proper subscription patterns
* Combining with Signals

***

# Module 9 — HTTP & API Communication

## Lesson 9.1 — HttpClient Fundamentals

* Setting up HttpClient
* Making requests (GET, POST, PUT, DELETE)
* Request/response types
* URL parameters and options

## Lesson 9.2 — GET Requests

* Fetching data
* Type-safe responses
* Query parameters

## Lesson 9.3 — POST Requests

* Creating resources
* Sending data
* Request body typing

## Lesson 9.4 — PUT & DELETE Requests

* Updating resources
* Deleting resources
* Response handling

## Lesson 9.5 — HTTP Error Handling

* Error types
* `catchError()` operator
* User-friendly error messages
* Retry logic

## Lesson 9.6 — Functional HTTP Interceptors (Modern)

* What are interceptors?
* Request modification
* Response transformation
* Error handling globally
* Functional interceptor syntax (modern)
* Class-based interceptors (legacy reference)

## Lesson 9.7 — Consuming Public APIs

* Finding and using APIs
* Authentication headers
* CORS considerations
* API documentation

## Lesson 9.8 — Service-Based HTTP Architecture

* Encapsulating HTTP calls in services
* Exposing Observables vs Signals
* Error handling in services
* Combining multiple requests

***

# Module 10 — Routing

## Lesson 10.1 — Route Configuration

* Defining routes
* Route file structure
* Path configuration
* Component mapping

## Lesson 10.2 — Router Outlet & Navigation

* `<router-outlet>` component
* `routerLink` directive
* Programmatic navigation with `Router`
* Navigation options and parameters

## Lesson 10.3 — Route Parameters

* Path parameters (`:id`)
* Extracting parameters in components
* `ActivatedRoute` service
* Query parameters

## Lesson 10.4 — Lazy Loading

* Code splitting with lazy loading
* `loadComponent`
* `loadChildren` for feature routes
* Performance benefits

## Lesson 10.5 — Functional Route Guards (Modern)

* What are guards?
* `CanActivateFn` — protecting routes
* `CanDeactivateFn` — confirmation on exit
* `CanMatchFn` — route matching logic
* Redirecting with `UrlTree`
* Class-based guards (legacy reference)

## Lesson 10.6 — Programmatic Navigation

* Using `Router.navigate()`
* Route parameters in navigation
* Query parameters
* Fragment navigation

## Lesson 10.7 — Advanced Routing

* Child routes
* Auxiliary routes
* Route resolvers (data preloading)
* Route reuse strategies

***

# Module 11 — Mini Project 1: Todo Application

**Objectives:** Apply Modules 0-10

**Scope:** 4-6 hours

**Features:**
* Add, complete, delete todos
* Filter (all, active, completed)
* Persist to localStorage
* Count completed (computed)
* Modern control flow (@if, @for)
* Signals for state
* Service managing todo logic
* Standalone components

**Technologies:**
* Standalone components
* Signals + computed
* @if, @for control flow
* FormsModule for input
* localStorage via effect()
* Basic component testing

**Deliverables:**
* TodoListComponent
* TodoItemComponent
* TodoService
* One unit test

***

# Module 12 — Mini Project 2: Real API Project (LandLord Angular Frontend)

**Objectives:** Apply all concepts with real backend API

**Scope:** 6-8 hours

**Context:** Your Spring Boot backend already exists. Build the Angular frontend.

**Features:**
* Authentication service & login
* Protected routes with guards
* List properties (GET)
* Create property (POST with form)
* Edit property (PUT)
* Delete property (DELETE)
* Pagination
* Error handling
* Loading states
* Search/filter properties
* JWT token management
* Token refresh logic

**Architecture:**
* Shared services (auth, property, api)
* Auth module (login, signup)
* Properties module (list, detail, form)
* Route guards (functional)
* HTTP interceptors (functional)
* Reactive forms
* RxJS operators (switchMap, catchError, debounceTime)

**Technologies:**
* HttpClient + RxJS
* Signals in services + components
* Reactive forms with validation
* Functional route guards
* Functional HTTP interceptors
* toSignal() for Observable conversion
* Component communication
* Modern control flow
* Full CRUD operations

***

# Module 13 — Testing Throughout

## Lesson 13.1 — Testing Fundamentals

* Testing frameworks (Jasmine, Karma)
* Test structure (describe, it, expect)
* Setup and teardown

## Lesson 13.2 — Component Testing

* Testing component logic
* Testing event handlers
* Testing data binding
* Testing with Signals

## Lesson 13.3 — Service Testing

* Testing service methods
* Testing Signal state
* DI in tests

## Lesson 13.4 — HTTP Testing

* `HttpTestingController`
* Mocking HTTP requests
* Testing error handling
* Request expectations

## Lesson 13.5 — Integration Testing

* Testing component + service
* Multiple components together
* Router testing

## Lesson 13.6 — Testing Observables & RxJS

* Testing Observable streams
* Testing with operators
* Marble testing (advanced)

## Lesson 13.7 — Testing Forms

* Template-driven form testing
* Reactive form testing
* Validation testing

***

# Module 14 — Authentication & Authorization

## Lesson 14.1 — Authentication Concepts

* What is authentication vs authorization?
* JWT tokens
* Token storage (localStorage vs sessionStorage)
* Security considerations

## Lesson 14.2 — Implementing Authentication

* Login service
* Token management
* Automatic token refresh
* Logout

## Lesson 14.3 — Authorization & Role-Based Access

* User roles
* Role-based component rendering
* Route-level authorization

## Lesson 14.4 — Protecting Routes

* Auth guards implementation
* Redirect to login
* Checking permissions

## Lesson 14.5 — Securing HTTP Requests

* Adding auth headers to requests
* Using interceptors for auth
* Token refresh on expiry

***

# Module 15 — Angular CDK, Material & Accessibility

## Lesson 15.1 — Introduction to Angular Material

* What is Angular Material?
* Installation and setup
* Theme configuration

## Lesson 15.2 — Material Components

* Buttons and inputs
* Cards and layouts
* Forms and input
* Dialogs and modals
* Tables and data grids
* Menus and navigation

## Lesson 15.3 — Angular CDK Overview

* Common utilities
* Drag and drop
* Overlay services
* Accessibility utilities

## Lesson 15.4 — Accessibility Fundamentals

* Semantic HTML
* ARIA attributes and labels
* Keyboard navigation
* Focus management

## Lesson 15.5 — Accessible Forms

* Form labels
* Error messages accessibility
* Validation feedback

## Lesson 15.6 — Testing Accessibility

* Accessibility testing tools
* Common accessibility issues
* Best practices

***

# Module 16 — Performance, Optimization & Deployment

## Lesson 16.1 — Performance Optimization

* Change detection strategies
* OnPush strategy
* Lazy loading components
* Code splitting

## Lesson 16.2 — Bundle Analysis

* Build output analysis
* Identifying large modules
* Tree-shaking unused code
* Production optimizations

## Lesson 16.3 — Rendering Strategies

* Client-side rendering (CSR)
* Server-side rendering (SSR)
* Static site generation (SSG)
* Hydration basics

## Lesson 16.4 — Production Build

* Building for production
* Environment configuration
* Build optimizations
* Source maps for debugging

## Lesson 16.5 — Deployment Platforms

* Vercel deployment
* Netlify deployment
* AWS hosting
* Docker containerization
* GitHub Pages

## Lesson 16.6 — Monitoring & Analytics

* Error tracking
* Performance monitoring
* User analytics

***

# Module 17 — Advanced Architecture & Patterns

## Lesson 17.1 — Smart vs Presentational Components

* Container components (smart)
* Presentational components (dumb)
* Data flow patterns
* When to use each

## Lesson 17.2 — Service-Oriented Architecture

* Service layers
* Separation of concerns
* Service composition
* Dependency management

## Lesson 17.3 — State Management Patterns

* State management with Signals
* State management with Observables
* Combining both approaches
* When to use external libraries (NgRx)

## Lesson 17.4 — Monorepo Architecture (NX)

* Monorepo concept
* NX workspace setup
* Shared libraries
* Application scaling

## Lesson 17.5 — Micro Frontends

* Micro frontend concept
* Module Federation
* Communication between apps
* Deployment strategies

## Lesson 17.6 — Performance Monitoring

* Custom performance tracking
* Analytics integration
* User experience metrics

***

# Module 18 — Interview Preparation & Revision

## Lesson 18.1 — Fundamentals Review

* Angular architecture
* Component-based design
* Dependency injection
* Services and modularity

## Lesson 18.2 — Modern Angular Patterns

* Standalone components
* Signals vs Observables
* Modern control flow (@if, @for, @switch)
* `inject()` function

## Lesson 18.3 — State Management Review

* Signals for UI state
* Services with Signals
* Observables for async operations
* Converting between them

## Lesson 18.4 — Forms & Validation

* Template-driven forms
* Reactive forms
* Signal Forms
* Validation strategies

## Lesson 18.5 — RxJS & Asynchronous Programming

* Observables
* Common operators
* Memory leak prevention
* Testing asynchronous code

## Lesson 18.6 — Routing & Navigation

* Route configuration
* Lazy loading
* Guards and protection
* Route parameters and query params

## Lesson 18.7 — HTTP & APIs

* HttpClient
* Error handling
* Interceptors
* Service architecture

## Lesson 18.8 — Testing Review

* Unit testing
* Integration testing
* E2E testing
* Test coverage

## Lesson 18.9 — Common Interview Questions & Answers

* Angular concepts
* Performance optimization
* Architecture decisions
* Real-world scenarios

## Lesson 18.10 — Coding Challenges

* Building small features
* Debugging exercises
* Architecture design tasks

***

# Progress Tracker

Update as you complete modules:

* ⬜ Module 0 — TypeScript Essentials
* ⬜ Module 1 — Angular Fundamentals
* ⬜ Module 2 — Components & Communication
* ⬜ Module 3 — Templates & Modern Control Flow
* ⬜ Module 4 — Signals & Reactive State
* ⬜ Module 5 — Directives & Pipes
* ⬜ Module 6 — Forms
* ⬜ Module 7 — Services & Modern DI
* ⬜ Module 8 — RxJS Essentials (NEW — CRITICAL)
* ⬜ Module 9 — HTTP & API Communication
* ⬜ Module 10 — Routing
* ⬜ Module 11 — Mini Project 1: Todo
* ⬜ Module 12 — Mini Project 2: LandLord
* ⬜ Module 13 — Testing Throughout
* ⬜ Module 14 — Authentication & Authorization
* ⬜ Module 15 — CDK, Material & Accessibility
* ⬜ Module 16 — Performance & Deployment
* ⬜ Module 17 — Advanced Architecture
* ⬜ Module 18 — Interview Prep & Revision

***

# Key Improvements Over Original

* ✓ Added critical Module 8: RxJS Essentials
* ✓ Balanced Signals vs Observables (not either/or)
* ✓ `effect()` taught cautiously (not for data loading)
* ✓ Modern patterns first (functional interceptors, guards)
* ✓ Signal Forms added to Module 6
* ✓ Testing integrated (Module 13)
* ✓ Authentication module (Module 14)
* ✓ Accessibility module (Module 15)
* ✓ Deployment & SSR (Module 16)
* ✓ Real project (LandLord) as Module 12
* ✓ Clean outline format (topics only, no code)

***

End of Reviewer-Improved Angular Roadmap
