Excellent.

You've now learned **what a component is** and **how to create one**.

Now we're going to answer one of the most important questions in Angular:

> **"When exactly does Angular create a component, and what if I want to run some code at that moment?"**

That's where the component lifecycle comes in.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.7 — Component Lifecycle (`ngOnInit`)

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ✅ Lesson 2.4 — Component Template
  * ✅ Lesson 2.5 — Component Styles
  * ✅ Lesson 2.6 — Angular CLI Component Generation
  * 🟨 Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you will understand:

* What a component lifecycle is.
* What `ngOnInit()` does.
* When `ngOnInit()` is called.
* Why Angular provides lifecycle hooks.
* When to use a constructor vs. `ngOnInit()`.

> **Scope Note:** Angular has several lifecycle hooks (`ngOnChanges`, `ngAfterViewInit`, `ngOnDestroy`, etc.). In this module, we'll focus only on **`ngOnInit()`**, because it's the one you'll use most often as a beginner.

***

# What Is a Lifecycle?

Everything has a lifecycle.

Think about a smartphone.

```text
Manufactured
      ↓
Turned On
      ↓
Used
      ↓
Turned Off
      ↓
Disposed
```

A component also has a lifecycle.

```text
Created
     ↓
Initialized
     ↓
Displayed
     ↓
Updated
     ↓
Destroyed
```

Angular lets us react to these stages.

***

# Why Does Angular Need Lifecycle Hooks?

Imagine a `UserProfile` component.

When it appears, you want to:

* Load user information.
* Display the user's name.
* Fetch profile data from an API.

When should that happen?

Not before the component exists.

Not after it's destroyed.

You need a specific moment:

> **"Run this code after the component has been created and initialized."**

Angular provides lifecycle hooks for exactly this purpose.

***

# The Most Common Hook: `ngOnInit()`

Angular calls:

```typescript
ngOnInit()
```

**once**, shortly after the component has been created and its input properties (which we'll learn later) have been initialized.

Think of it as Angular saying:

> "Your component is ready. You can perform your startup work now."

***

# Where Does It Go?

Suppose you have:

```typescript
export class Header {

}
```

To use `ngOnInit()`, first import the interface:

```typescript
import { Component, OnInit } from '@angular/core';
```

Then implement it:

```typescript
export class Header implements OnInit {

    ngOnInit(): void {

    }

}
```

The complete structure looks like:

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-header',
  imports: [],
  templateUrl: './header.html',
  styleUrl: './header.css'
})
export class Header implements OnInit {

  ngOnInit(): void {
    console.log('Header initialized');
  }

}
```

> The `implements OnInit` part isn't strictly required for Angular to call a correctly named `ngOnInit()` method, but it's considered a best practice because TypeScript checks that you've implemented the interface correctly.

***

# What Happens Internally?

When Angular encounters:

```html
<app-header></app-header>
```

it performs something like:

```text
Create component
       ↓
Set it up
       ↓
Call ngOnInit()
       ↓
Display the component
```

This all happens automatically.

***

# Let's See It

Open your `Header` component.

Inside:

```typescript
ngOnInit(): void {

}
```

Add:

```typescript
console.log('Header initialized');
```

Save.

Refresh the page.

Open your browser's Developer Tools (**F12 → Console**).

You should see:

```text
Header initialized
```

This confirms that Angular called your method.

***

# Does `ngOnInit()` Run More Than Once?

Normally:

**No.**

It runs **once for each component instance**.

For example:

```text
Header created

↓

ngOnInit()

↓

Displayed
```

If the component is destroyed and a new instance is created later (for example, by navigation or a conditional display), the new instance will have its own `ngOnInit()` call.

***

# Constructor vs. `ngOnInit()`

This is one of the most commonly asked Angular interview questions.

Let's compare them.

## Constructor

```typescript
constructor() {

}
```

Purpose:

* Initialize the class.
* Receive injected dependencies (we'll learn dependency injection in Module 5).

The constructor is a standard TypeScript/JavaScript feature—not something specific to Angular.

***

## `ngOnInit()`

```typescript
ngOnInit() {

}
```

Purpose:

* Run initialization logic after Angular has created and initialized the component.

Examples:

* Load data.
* Start API calls.
* Initialize component state.

***

# Easy Way to Remember

Think of building a new office.

### Constructor

The building is constructed.

Electricity, water, and furniture are still being prepared.

***

### `ngOnInit()`

The office opens.

Employees can begin working.

That's where your component should begin its startup work.

***

# A Simple Timeline

```text
Angular creates the component
          │
          ▼
Constructor runs
          │
          ▼
Angular initializes the component
          │
          ▼
ngOnInit() runs
          │
          ▼
User interacts with the component
```

For now, remember:

* **Constructor** → class setup.
* **`ngOnInit()`** → component initialization.

***

# Real Examples

Things that belong in `ngOnInit()`:

```typescript
// Load products

// Fetch users

// Read route parameters

// Initialize form values
```

Things that usually belong in the constructor:

```typescript
// Dependency Injection

constructor(private userService: UserService) {

}
```

We'll learn dependency injection and services in Module 5, so don't worry if that syntax looks unfamiliar.

***

# Common Beginner Misconceptions

### ❌ "`ngOnInit()` runs every time the page changes."

No.

It runs once for each component instance after Angular initializes it.

***

### ❌ "Everything should go into the constructor."

Not usually.

Initialization logic belongs in `ngOnInit()`.

***

### ❌ "`ngOnInit()` is mandatory."

No.

If your component doesn't need initialization work, you don't have to implement it.

***

### ❌ "The constructor is an Angular feature."

It isn't.

Constructors are part of TypeScript/JavaScript classes.

Angular simply calls them when it creates a component.

***

# Hands-on Exercise

Let's make the lifecycle visible.

## Step 1

Open:

```text
src/app/header/header.ts
```

Update it:

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-header',
  imports: [],
  templateUrl: './header.html',
  styleUrl: './header.css'
})
export class Header implements OnInit {

  ngOnInit(): void {
    console.log('Header component initialized!');
  }

}
```

***

## Step 2

Save the file.

***

## Step 3

Open the browser.

***

## Step 4

Press **F12**.

Open the **Console** tab.

***

## Step 5

Refresh the page.

You should see:

```text
Header component initialized!
```

Every time a new `Header` component is created, Angular calls `ngOnInit()`.

***

# Quick Review

Try answering these without looking back:

1. What is a component lifecycle?
2. When does `ngOnInit()` run?
3. Does `ngOnInit()` run every time change detection happens?
4. What is the main difference between a constructor and `ngOnInit()`?
5. Give two examples of work that belongs in `ngOnInit()`.

***

# Lesson Summary

Today you learned:

* ✅ What a component lifecycle is.
* ✅ Why Angular provides lifecycle hooks.
* ✅ When `ngOnInit()` is called.
* ✅ The difference between a constructor and `ngOnInit()`.
* ✅ How to use `ngOnInit()` in a real component.

***

# 🎉 Module 2 Complete!

Congratulations! You now understand the complete anatomy of an Angular component:

```text
Component

├── TypeScript (Logic)
├── HTML (Template)
├── CSS (Styles)
├── Metadata (@Component)
├── Selector
└── Lifecycle (ngOnInit)
```

That's a major milestone. Every Angular application is built from these building blocks.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ⬜ Module 3 — Templates & Data Binding
* ⬜ Module 4 — Directives
* ⬜ Module 5 — Services & Dependency Injection
* ⬜ Module 6 — Routing
* ⬜ Module 7 — HTTP & APIs
* ⬜ Module 8 — Forms

***

# One Important Update for Modern Angular

Angular has introduced newer reactive features, such as **signals**, and in some cases you may see developers using them instead of relying on lifecycle hooks like `ngOnInit()`. However:

* `ngOnInit()` is **still fully supported**.
* You'll encounter it in countless real-world projects.
* ==It's commonly expected in interviews and tutorials==.
* It's the right lifecycle hook to learn before moving on to more advanced Angular features.

So our roadmap is still following the right progression: first understand the classic component lifecycle, then later you'll be in a much better position to understand newer patterns.

***

## Next Module: Templates & Data Binding

This is where Angular becomes truly interactive.

So far, your templates have mostly contained static HTML.

In **Module 3**, you'll finally learn how to:

* Display values from your component in the UI.
* Respond to button clicks.
* Update the page automatically when data changes.
* Connect the TypeScript class and the HTML template together.

Many developers consider **data binding** to be the heart of Angular, and it's the foundation for everything that follows.
