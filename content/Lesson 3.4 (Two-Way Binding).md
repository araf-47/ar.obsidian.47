Excellent! You've now learned the three fundamental one-way communication mechanisms:

* **Interpolation (`{{ }}`)** → Display text.
* **Property Binding (`[]`)** → Send data from the component to the DOM.
* **Event Binding (`()`)** → Respond to user actions.

Now we're going to combine the last two into one of Angular's most popular features.

***

# Angular Master Course

# Module 3 — Templates & Data Binding

## Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ✅ Lesson 3.3 — Event Binding (`()`)
* 🟨 Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what two-way binding is.
* Understand why Angular provides `ngModel`.
* Use `[(ngModel)]` to synchronize data.
* Import the required Angular module for `ngModel`.
* Explain how two-way binding combines property binding and event binding.

***

# Prerequisites

You should already understand:

* ✅ Interpolation
* ✅ Property Binding
* ✅ Event Binding

***

# Part 1 — The Problem

Let's build a simple input box.

Component:

```typescript
export class App {
  username = 'Araf';
}
```

Template:

```html
<input [value]="username">
```

The browser shows:

```
Araf
```

Now type:

```
John
```

Question:

What is the value of `username`?

Still:

```typescript
username = "Araf";
```

Why?

Because **property binding only sends data from the component to the view**.

The user's typing doesn't travel back to the component.

***

# Can We Fix It Using Event Binding?

Yes.

We could write something like:

```html
<input
  [value]="username"
  (input)="onInput($event)">
```

And in the component:

```typescript
onInput(event: Event) {
  const input = event.target as HTMLInputElement;
  this.username = input.value;
}
```

This works.

But imagine doing this for every input field in your application.

It becomes repetitive.

Angular gives us a simpler solution.

***

# What Is Two-Way Binding?

**Definition:**

> Two-way binding keeps the component and the user interface synchronized.

If the component changes:

→ the UI updates.

If the user changes the UI:

→ the component updates.

Both stay in sync automatically.

***

# Visual Flow

```text
Component

⇅

Angular

⇅

Input Field
```

Data can move in **both directions**.

***

# The Syntax

Angular provides the `ngModel` directive.

Syntax:

```html
[(ngModel)]="username"
```

Notice the symbols:

```text
[()]
```

It looks like:

* `[]` (property binding)
* `()` (event binding)

combined together.

People often call this the **"banana in a box"** syntax because the parentheses look like a banana inside square brackets.

***

# Using `ngModel`

Component:

```typescript
export class App {
  username = 'Araf';
}
```

Template:

```html
<input [(ngModel)]="username">

<p>Hello {{ username }}</p>
```

What happens?

Initially:

```
Araf
```

If the user types:

```
John
```

Angular updates:

```typescript
username = "John";
```

Interpolation immediately displays:

```
Hello John
```

No extra code is required.

***

# How Does It Work Internally?

Conceptually, Angular treats:

```html
[(ngModel)]="username"
```

like a combination of:

```html
[value]="username"
```

and

```html
(input)="..."
```

You don't need to write the event-handling code yourself.

Angular handles it for you.

> **Note:** Internally, Angular expands `[(ngModel)]` into a property binding and a corresponding event binding specific to `ngModel`. Thinking of it as "property binding + event binding" is the right mental model for learning.

***

# Important: Import `FormsModule`

`ngModel` is **not available by default**.

If you're using a **standalone Angular application** (the default in modern Angular), open your `app.ts` (or the component where you're using `ngModel`) and import `FormsModule`.

Example:

```typescript
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
  username = 'Araf';
}
```

Without `FormsModule`, Angular won't recognize `ngModel`.

> In older Angular applications that use `NgModule`, `FormsModule` is imported into the application's module instead. Since you're learning modern Angular, we'll use the standalone approach.

***

# Hands-on Exercise

## Step 1

Open:

```
src/app/app.ts
```

Update it:

```typescript
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-root',
  imports: [FormsModule],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {

  username = 'Araf';

}
```

***

## Step 2

Open:

```
src/app/app.html
```

Replace the contents with:

```html
<h1>Two-Way Binding Demo</h1>

<input [(ngModel)]="username">

<p>Hello {{ username }}</p>
```

***

## Step 3

Save the files.

Try typing into the input.

Example:

```
Angular
```

The page should immediately update to:

```
Hello Angular
```

Notice:

You never wrote an event handler.

Angular synchronized everything automatically.

***

# Real-World Uses

You'll use two-way binding for:

* Login forms
* Registration forms
* Search boxes
* User profiles
* Settings pages
* Contact forms

Anywhere the user enters data.

***

# Common Beginner Mistakes

## ❌ Forgetting `FormsModule`

If you see an error like:

> `Can't bind to 'ngModel' since it isn't a known property...`

The first thing to check is whether you've imported `FormsModule`.

***

## ❌ Forgetting the brackets and parentheses

Wrong:

```html
(ngModel)="username"
```

Wrong:

```html
[ngModel]="username"
```

Correct:

```html
[(ngModel)]="username"
```

***

## ❌ Expecting `ngModel` to work on every element

`ngModel` is intended for **form controls**, such as:

* `<input>`
* `<textarea>`
* `<select>`

Using it on elements like `<div>` or `<h1>` doesn't make sense because those elements don't accept user input.

***

# Quick Review

Without looking back:

1. What problem does two-way binding solve?
2. What is the syntax for two-way binding?
3. Why is it called "two-way"?
4. Which Angular module is required for `ngModel`?
5. What happens when the user types into an input bound with `[(ngModel)]`?

***

# Lesson Summary

Today you learned:

* ✅ What two-way binding is.
* ✅ Why Angular provides `ngModel`.
* ✅ The `[(ngModel)]` syntax.
* ✅ How two-way binding keeps the UI and component synchronized.
* ✅ How to import `FormsModule` in a standalone Angular application.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ✅ Lesson 3.3 — Event Binding (`()`)
* ✅ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

## 🎯 Key Takeaway

If you remember only one thing from this lesson, remember this mapping:

* `{{ }}` → Display data.
* `[]` → Component → View.
* `()` → View → Component.
* `[()]` → Both directions.

These four binding mechanisms are the foundation of how Angular components communicate with the user interface. Once you're comfortable with them, the rest of Angular becomes much easier to understand.
