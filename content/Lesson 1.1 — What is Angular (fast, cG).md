# Lesson 1.1 — What is Angular?

Today we will cover only:

* What Angular is
* Single Page Applications (SPA)
* Angular architecture overview
* Angular's evolution: NgModules → Standalone → Signals

***

## 1. Theory — What is Angular?

**Angular is a framework for building web applications.**

More specifically, Angular gives you a structured way to build applications using:

* **Components** — pieces of the UI
* **Templates** — HTML enhanced with Angular features
* **Services** — reusable application logic
* **Dependency Injection** — a way for Angular to provide objects your code needs
* **Routing** — moving between application views
* **Forms** — handling user input
* **HTTP tools** — communicating with backends
* **Signals and other reactive tools** — managing changing application state

Instead of manually connecting all these pieces yourself, Angular provides a framework for organizing them.

A simple way to think about it:

```text
Angular
   │
   ├── Components
   ├── Templates
   ├── Services
   ├── Routing
   ├── Forms
   ├── HTTP
   └── Reactive state
```

Angular is therefore much more than a collection of UI components.

It gives you an **application structure**.

***

## 2. How Angular works — Simple mental model

Imagine you are building a shopping application.

The screen might contain:

```text
Shopping App
│
├── Header
├── Product List
│   ├── Product
│   ├── Product
│   └── Product
├── Cart
└── Footer
```

In Angular, these pieces can be represented by **components**.

For example:

```text
AppComponent
│
├── HeaderComponent
├── ProductListComponent
│   └── ProductComponent
├── CartComponent
└── FooterComponent
```

Each component can have:

```text
Component
   │
   ├── TypeScript → behavior/data
   ├── HTML       → what appears on screen
   └── CSS        → appearance
```

For example:

```typescript
export class ProductComponent {
  productName = 'Laptop';
  price = 800;
}
```

and its template could display that information:

```html
<h2>{{ productName }}</h2>
<p>Price: {{ price }}</p>
```

Angular connects the TypeScript and HTML.

So you don't have to manually manipulate the page every time your application data changes.

***

# 3. Single Page Applications (SPA)

A **Single Page Application**, or **SPA**, is a web application where the browser initially loads an application page, and Angular then manages much of the application's navigation and UI changes without requiring a complete browser-page reload for every route.

For example:

```text
Browser
   │
   ▼
Angular Application
   │
   ├── Home
   ├── Products
   ├── Product Details
   └── About
```

You might navigate:

```text
/products
```

then:

```text
/products/25
```

then:

```text
/about
```

The application can change what is displayed while remaining within the same running application.

### Traditional website

A simplified model:

```text
Browser
   │
   ▼
Server
   │
   ▼
New HTML page
```

Navigate somewhere else:

```text
Browser
   │
   ▼
Server
   │
   ▼
Another HTML page
```

### Angular SPA

A simplified model:

```text
Browser
   │
   ▼
Angular Application
   │
   ├── Home view
   ├── Products view
   ├── About view
   └── ...
```

Angular can change the displayed component when the URL changes.

This is one of the jobs of **Angular Router**, which we will learn later.

### Important

SPA does **not** mean:

> "The application has only one screen."

It means the browser is generally running one client-side application that can change its displayed views without doing a full document reload for every navigation.

***

# 4. Angular Architecture Overview

You don't need to memorize the entire architecture yet.

For now, understand this basic picture:

```text
                 Angular Application
                         │
        ┌────────────────┼────────────────┐
        │                │                │
   Components         Services         Router
        │                │                │
        ▼                ▼                ▼
      UI            Application       Navigation
                    logic/state
```

Let's look at the major pieces.

### Components

Components represent parts of your application's UI.

```text
Component
   │
   ├── TypeScript
   ├── Template
   └── Styles
```

Example:

```text
ProductComponent
```

might display one product.

***

### Templates

Templates are HTML enhanced with Angular features.

For example:

```html
<h1>{{ title }}</h1>
```

Angular can connect this template to data from the component.

***

### Services

Services hold reusable logic that doesn't belong directly inside a UI component.

For example:

```text
ProductComponent
       │
       ▼
ProductService
       │
       ▼
Backend API
```

We'll learn services later.

***

### Router

The Router manages application navigation.

For example:

```text
/products
/products/10
/cart
```

Different URLs can display different components.

***

### Signals

Signals provide a way to represent reactive state.

For example:

```typescript
count = signal(0);
```

If the signal's value changes, Angular can know that the relevant UI needs to react to that change.

We'll study signals properly in Module 5.

***

# 5. Angular's Evolution

This part is important because you'll encounter **old Angular code** while learning from tutorials, Stack Overflow, GitHub projects, or older courses.

Angular itself has evolved.

A simplified timeline is:

```text
Older Angular
     │
     ▼
NgModules
     │
     ▼
Standalone
     │
     ▼
Signals and modern reactive APIs
```

Let's understand what changed.

***

## 5.1 🕰️ NgModules

Older Angular applications commonly organized functionality using **NgModules**.

You might see code like:

```typescript
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [ng directly insi
    BrowserModule
  ],
  bootstrap: [
    AppComponent
  ]
})
export class AppModule {}
```

The application had an `AppModule` that helped organize and bootstrap the application.

You may also see:

```text
AppModule
   │
   ├── Components
   ├── Directives
   ├── Pipes
   └── Other modules
```

This was an important part of older Angular architecture.

### Do you need to learn NgModules deeply?

**No.**

Your roadmap deliberately puts NgModules outside the main modern path.

You mainly need enough knowledge to **recognize and understand old Angular code**.

***

# 6. Standalone Angular

Modern Angular moved toward **standalone components**.

Instead of requiring components to belong to an NgModule, a component can be standalone.

For example:

```typescript
@Component({
  selector: 'app-product',
  standalone: true,
  template: `
    <h2>Product</h2>
  `
})
export class ProductComponent {}
```

The important idea is:

```text
Old approach:

Component
    ↓
NgModule
    ↓
Application


Modern approach:

Standalone Component
        ↓
Application
```

Standalone APIs make Angular's structure more direct.

You will see this much more clearly when we create your first project and examine its files.

### One important correction

Modern Angular components are standalone by default in current Angular versions, so you will often **not even need to write**:

```typescript
standalone: true
```

You'll learn the exact modern syntax when we reach components.

***

# 7. Signals

Signals represent another important evolution in Angular.

Before signals, Angular applications commonly relied heavily on Angular's change-detection mechanisms together with other reactive patterns.

Signals provide a simple way to represent **reactive state**.

For example:

```typescript
import { signal } from '@angular/core';

count = signal(0);
```

Think of it as:

```text
count
  │
  ▼
Reactive value
  │
  ├── Read it
  ├── Change it
  └── Angular can react to the change
```

You read a signal by calling it:

```typescript
count()
```

You can change it with:

```typescript
count.set(10);
```

Or update it based on its current value:

```typescript
count.update(value => value + 1);
```

Don't worry about understanding all of this yet.

**Signals have their own module later.**

For now, remember:

> A signal is Angular's modern way of representing reactive state.

***

# 8. Putting the evolution together

You can think about Angular's evolution like this:

```text
                 ANGULAR
                    │
          ┌─────────┴─────────┐
          │                   │
     Application           Reactive
      structure              state
          │                   │
     ┌────┴────┐              │
     │         │              │
  NgModules  Standalone     Signals
   🕰️          Modern       Modern
```

The important distinction for your learning path is:

| Concept    | Your focus                    |
| ---------- | ----------------------------- |
| NgModules  | 🕰️ Recognize old code        |
| Standalone | ✅ Main approach               |
| Signals    | ✅ Main modern state approach  |
| Components | ✅ Main Angular building block |
| Templates  | ✅ Main UI mechanism           |

You don't need to memorize Angular's history.

You need to understand **why the modern code you are about to learn looks different from older tutorials.**

***

# 9. Common Mistakes

### Mistake 1: Thinking Angular is just a UI library

Angular is a **full web application framework**.

It provides structure for things such as components, routing, forms, HTTP communication, dependency injection, and application state.

***

### Mistake 2: Thinking SPA means one screen

SPA means the application can navigate between different views without requiring a complete browser document reload for every navigation.

An SPA can have dozens of screens.

***

### Mistake 3: Learning old Angular first

You don't need to build your foundation around:

```text
NgModules
*ngIf
*ngFor
@Input
@Output
constructor injection
```

Your main path is modern Angular.

We'll still learn enough legacy syntax to read existing code.

***

### Mistake 4: Thinking signals are components

They aren't.

A component is a UI building block.

A signal is a way of representing reactive state.

For example:

```text
Component
   │
   └── contains/uses
          │
          ▼
       Signal
```

***

# 10. Hands-on Exercise

Don't write a full Angular application yet.

Instead, explain this architecture in your own words:

```text
Angular Application
        │
        ├── AppComponent
        │       │
        │       └── ProductComponent
        │
        ├── ProductService
        │
        └── Router
```

Answer these **four questions**:

1. What is the job of a **component**?
2. What is the job of a **service**?
3. What does the **Router** handle?
4. What is a **signal** used for?

Keep each answer to **1–2 sentences**.

***

# 11. Quick Review

### Question 1

What is Angular?

> **A.** A programming language
> **B.** A web application framework
> **C.** A database
> **D.** A web browser

**Correct answer: B — A web application framework.**

***

### Question 2

What does SPA stand for?

> **A.** Server Programming Application
> **B.** Single Page Application
> **C.** Simple Programming Architecture
> **D.** Single Program API

**Correct answer: B — Single Page Application.**

***

### Question 3

Which is the main approach in your roadmap?

> **A.** NgModules
> **B.** Standalone Angular
> **C.** JSP
> **D.** jQuery

**Correct answer: B — Standalone Angular.**

***

### Question 4

What is a signal primarily used for?

> **A.** Storing reactive state
> **B.** Creating database tables
> **C.** Defining CSS
> **D.** Creating URLs

**Correct answer: A — Signals represent reactive state that Angular can react to.**

***

### Question 5

Why are you learning NgModules?

> **A.** They are the main modern Angular architecture
> **B.** They replace TypeScript
> **C.** Mainly so you can recognize and understand older Angular code
> **D.** They are required for every modern component

**Correct answer: C — NgModules are mainly legacy knowledge in this roadmap.**

***

## Progress

**Completed:** Lesson 1.1 — What is Angular?

**Next:** **Lesson 1.2 — Installing Node.js, installing Angular CLI, and creating your first Angular project.**
