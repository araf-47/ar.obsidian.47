Here's the merged roadmap and a matching master instruction. LandLord is gone, modern Angular is the main path, and legacy syntax gets one short lesson at the end of its topic.

***

# Angular Master Roadmap (Fast Track, Modern First)

**Philosophy:** Short and fast. Modern Angular (standalone, signals, `@if`/`@for`, `inject()`) is the primary way. Legacy syntax is covered briefly so you can read old code.

***
### Master instruction:
- 🍉 [[Master Instruction (Angular Fast Track Roadmap)]].
***
# Module 0 — TypeScript Essentials

### Lesson 0.1

* What is TypeScript?
* Why Angular uses TypeScript
* Installing TypeScript
* Compiling `.ts` files

### Lesson 0.2

* Variables
* Primitive types
* Type inference
* `any`
* `unknown`

### Lesson 0.3

* Arrays
* Tuples
* Enums
* Union types
* Objects

### Lesson 0.4

* Functions
* Optional parameters
* Default parameters
* Rest parameters
* Arrow functions

### Lesson 0.5

* Interfaces
* Type aliases

### Lesson 0.6

* Classes
* Constructors
* Properties
* Methods

### Lesson 0.7

* Access modifiers
* `readonly`
* Getters & setters

### Lesson 0.8

* Inheritance
* Abstract classes

### Lesson 0.9

* Generics

### Lesson 0.10

* Modules
* `import`
* `export`

***

# Module 1 — Angular Introduction

### Lesson 1.1

* What is Angular?
* Single Page Applications
* Angular architecture overview
* Evolution: NgModules → Standalone → Signals

### Lesson 1.2

* Installing Node.js
* Installing Angular CLI
* Creating the first project

### Lesson 1.3

* Modern project structure
  * `main.ts` and `bootstrapApplication()`
  * Root component
  * `app.config.ts`
  * `app.routes.ts`
  * `angular.json`
  * `tsconfig.json`

### Lesson 1.4

* Running the application
* Development server
* Build process

***

# Module 2 — Components

### Lesson 2.1

* What is a component?
* Component anatomy

### Lesson 2.2

* Component metadata
* Selector
* Standalone components and the `imports` array

### Lesson 2.3

* Component template
* Component styles

### Lesson 2.4

* Angular CLI component generation

### Lesson 2.5

* Component lifecycle
* `ngOnInit`
* `ngOnDestroy`

***

# Module 3 — Templates & Data Binding

### Lesson 3.1

* Interpolation
* Property binding

### Lesson 3.2

* Event binding
* Two-way binding

### Lesson 3.3

* Class binding
* Style binding

### Lesson 3.4

* Pipes
* Built-in pipes

***

# Module 4 — Modern Control Flow & Directives

### Lesson 4.1

* Why modern control flow?
* `@if` / `@else`

### Lesson 4.2

* `@for`
* `track`
* `@empty`
* `$index`, `$first`, `$last`

### Lesson 4.3

* `@switch` / `@case` / `@default`

### Lesson 4.4

* What are directives?
* Attribute directives
* `ngClass`
* `ngStyle`

### Lesson 4.5 (Legacy Reference)

* `*ngIf`
* `*ngFor`
* `*ngSwitch`
* Old vs modern syntax
* Migration

***

# Module 5 — Signals

### Lesson 5.1

* What is a signal?
* Why signals exist

### Lesson 5.2

* `signal()`
* Reading, `set()`, `update()`
* Using signals in templates

### Lesson 5.3

* `computed()`

### Lesson 5.4

* `effect()` (basics and cautions)

***

# Module 6 — Component Communication

### Lesson 6.1

* Parent and child components

### Lesson 6.2

* `input()` (modern)

### Lesson 6.3

* `output()` (modern)

### Lesson 6.4 (Legacy Reference)

* `@Input`
* `@Output`
* `EventEmitter`

***

# Module 7 — Forms

### Lesson 7.1

* Forms overview

### Lesson 7.2

* Template-driven forms

### Lesson 7.3

* Reactive forms
* `FormBuilder`

### Lesson 7.4

* Form validation

***

# Module 8 — Services & Dependency Injection

### Lesson 8.1

* What is a service?
* Creating services

### Lesson 8.2

* Dependency Injection
* `inject()` (modern)

### Lesson 8.3

* `providedIn: 'root'`
* Singleton services

### Lesson 8.4

* Sharing state with signals in services

### Lesson 8.5 (Legacy Reference)

* Constructor injection

***

# Module 9 — Routing

### Lesson 9.1

* Why routing?
* Creating routes

### Lesson 9.2

* `<router-outlet>`
* `routerLink`

### Lesson 9.3

* Route parameters

### Lesson 9.4

* Programmatic navigation

### Lesson 9.5

* Lazy loading (`loadComponent`)

***

# Module 10 — HTTP Communication & RxJS Basics

### Lesson 10.1

* What is an Observable?
* `subscribe()`

### Lesson 10.2

* `provideHttpClient()`
* `HttpClient`
* GET requests

### Lesson 10.3

* POST requests
* PUT requests
* DELETE requests

### Lesson 10.4

* `pipe()`
* `map`
* `catchError`

### Lesson 10.5

* `async` pipe
* `toSignal()`
* Avoiding memory leaks

### Lesson 10.6

* Consuming a public API

***

# Module 11 — Mini Project 1

## To-Do Application

Topics used:

* Components
* Data binding
* `@if` / `@for`
* Signals
* Forms
* A service

***

# Module 12 — Mini Project 2

Choose one:

* Weather App
* Movie Search
* Fake Store
* Pokémon Search

Topics used:

* Routing
* Services
* HTTP
* Forms
* Signals

***

# Module 13 — Angular Interview / Exam Revision

* Angular architecture
* Components
* Templates & modern control flow
* Signals
* Directives
* Data binding
* Services & DI
* Routing
* Forms
* HTTP & RxJS basics
* Angular CLI
* Common interview questions
* Common exam questions

***


***

**What changed from the two originals:**

* **Kept from the old one:** the short, granular lesson size and the 7-step lesson format.
* **Kept from the new one:** modern-first syntax, signals, `inject()`, and a small RxJS section so HTTP makes sense.
* **Dropped:** LandLord, testing, interceptors, guards, Material, SSR, NX and the other advanced modules.

Tell me whether you want to keep the 7-step format as is, and then we can start the next lesson.

