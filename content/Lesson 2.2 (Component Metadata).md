Excellent. From this lesson onward, we'll spend most of our time in **real Angular code**.

I also want to establish an important rule for the rest of the course:

> **We will learn using the code that Angular CLI actually generated, not simplified or imaginary examples.**

Why?

Because when you open your project, I want you to recognize every file we're discussing.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.2 — Component Metadata

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * 🟨 Lesson 2.2 — Component Metadata
  * ⬜ Lesson 2.3 — Component Selector
  * ⬜ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you will understand:

* What metadata is.
* What a decorator is.
* What `@Component` does.
* How Angular discovers a component.
* The purpose of each property inside `@Component`.
* Why Angular cannot work without metadata.

***

# Before We Open the Code...

Let's ask a question.

Imagine you create this TypeScript class:

```typescript
export class AppComponent {
    title = 'Hello Angular';
}
```

Now ask yourself:

> **How does Angular know this class is supposed to be displayed on the screen?**

The answer is:

**It doesn't.**

To Angular, this is just another TypeScript class.

It could just as easily represent:

* a Student,
* a Product,
* a Car,
* or anything else.

Angular needs a way to distinguish an ordinary class from a component.

That's where **metadata** comes in.

***

# What Is Metadata?

The word **metadata** means:

> **Data about data.**

That sounds abstract, so let's use a real-world example.

Imagine you have a passport.

The passport contains information **about you**:

* Name
* Date of birth
* Nationality
* Passport number

The passport isn't you—it describes you.

Metadata works the same way.

A class contains your program logic.

Metadata contains information **about that class**.

***

# In Angular

Without metadata:

```typescript
export class AppComponent {

}
```

Angular sees:

> "Just a class."

With metadata:

```typescript
@Component({
    ...
})
export class AppComponent {

}
```

Angular sees:

> "Ah! This is a component."

That one addition completely changes how Angular treats the class.

***

# What Is a Decorator?

This is our first small TypeScript detour.

Remember when we said we'd only learn the TypeScript needed for Angular?

This is one of those moments.

A **decorator** is a special TypeScript feature that **adds information or behavior to a class, method, property, or parameter**.

Angular uses decorators extensively.

For components, the decorator is:

```typescript
@Component(...)
```

You don't need to know how decorators are implemented internally yet.

For now, think of them as **labels** that tell Angular how to use something.

***

# Your First Real Angular Component

Open your project.

Navigate to:

```text
src/app/
```

In a modern Angular project, you'll likely see:

```text
app.ts
app.html
app.css
app.config.ts
app.routes.ts
```

Open:

```text
app.ts
```

You should see something similar to this:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  imports: [],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
  protected title = 'hello-angular';
}
```

> **Note:** If your project uses an older Angular version, the filenames and class names may differ (for example, `app.component.ts` and `AppComponent`). The concepts are exactly the same.

***

# Let's Read It Line by Line

## Line 1

```typescript
import { Component } from '@angular/core';
```

This imports the `Component` decorator from Angular.

Without this import, TypeScript wouldn't know what `@Component` means.

Think of it as saying:

> "I want to use Angular's Component decorator in this file."

***

## The Decorator

```typescript
@Component({
    ...
})
```

This is the metadata.

It tells Angular:

* this class is a component,
* how to display it,
* which HTML it uses,
* which CSS it uses,
* and more.

Everything inside the curly braces is configuration.

***

# The Configuration Object

Let's look at it:

```typescript
@Component({
  selector: 'app-root',
  imports: [],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
```

This is simply a JavaScript/TypeScript object.

Each property gives Angular a piece of information.

***

## `selector`

```typescript
selector: 'app-root'
```

This tells Angular:

> "What HTML tag represents this component?"

Later you'll write:

```html
<app-root></app-root>
```

Angular replaces that tag with your component.

We'll study selectors in the next lesson.

***

## `imports`

```typescript
imports: []
```

Modern Angular uses **standalone components**.

Instead of putting everything into an `NgModule`, each standalone component declares the Angular features and other standalone components it needs directly in its `imports` array.

Right now it's empty because the default starter component doesn't use additional standalone directives or components.

Later, you'll see entries like:

```typescript
imports: [
    CommonModule,
    FormsModule
]
```

or other standalone components.

We'll cover this in more depth when we learn directives and forms.

***

## `templateUrl`

```typescript
templateUrl: './app.html'
```

This tells Angular:

> "The HTML for this component is in another file."

Angular reads that file and uses it as the component's view.

If you open:

```text
app.html
```

you're looking at this component's template.

***

## `styleUrl`

```typescript
styleUrl: './app.css'
```

This tells Angular:

> "The CSS for this component is in this file."

Open:

```text
app.css
```

and you're editing only this component's styles.

***

# The Class

Below the metadata is the class itself:

```typescript
export class App {
    protected title = 'hello-angular';
}
```

This is where your application's logic lives.

Notice something interesting:

The class doesn't mention HTML or CSS.

That's because the metadata already connected them.

You can think of it like this:

```text
@Component
        │
        ├── HTML
        ├── CSS
        └── Configuration
                │
                ▼
        TypeScript Class
```

The decorator acts as the bridge between Angular and your class.

***

# Why Doesn't Angular Read Every Class?

Imagine your project has 200 TypeScript classes.

Some represent:

* Users
* Products
* Orders
* Utilities
* Services
* Components

Angular can't assume every class is a UI component.

The `@Component` decorator clearly identifies which classes should be treated as components.

***

# Mental Model

When Angular starts your application, it doesn't just scan for classes.

It looks for classes marked with:

```typescript
@Component(...)
```

Only then does Angular know:

* this is a component,
* here's its HTML,
* here's its CSS,
* here's its selector,
* here's how to create it.

***

# Common Beginner Misconceptions

### ❌ "The decorator creates the component."

Not exactly.

The class **is** the component.

The decorator provides Angular with the information it needs to use that class as a component.

***

### ❌ "The decorator is optional."

It isn't.

Without `@Component`, Angular won't recognize the class as a component.

***

### ❌ "The HTML lives inside the class."

It doesn't.

The class and the template are separate files (unless you choose to write an inline template, which we'll discuss later).

***

### ❌ "The `imports` array is the same as JavaScript `import` statements."

No.

These are different things:

* `import { Component } from '@angular/core';` is a TypeScript import that brings code into the file.
* `imports: []` is Angular metadata that tells a standalone component which Angular features or other standalone components it can use in its template.

***

# Hands-on Exercise

Open:

```text
src/app/app.ts
```

Without changing anything yet:

1. Find the `@Component` decorator.
2. Identify:

   * `selector`
   * `imports`
   * `templateUrl`
   * `styleUrl`
3. Open:

   * `app.html`
   * `app.css`
4. Confirm that the metadata points to those files.

The goal is simply to connect the dots between the metadata and the files in your project.

***

# Quick Review

Try answering these from memory:

1. What is metadata?
2. What is a decorator?
3. Why does Angular need the `@Component` decorator?
4. What does `templateUrl` specify?
5. What is the difference between the TypeScript `import` statement and the `imports` property inside `@Component`?

***

# Lesson Summary

Today you learned:

* ✅ What metadata is.
* ✅ What decorators are.
* ✅ Why Angular uses `@Component`.
* ✅ How Angular recognizes components.
* ✅ The purpose of `selector`, `imports`, `templateUrl`, and `styleUrl`.
* ✅ How the decorator connects the TypeScript class to its HTML and CSS.

***

## Roadmap Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ⬜ Lesson 2.3 — Component Selector
  * ⬜ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

### One correction to something you may encounter elsewhere

Many older tutorials will show:

```typescript
styleUrls: ['./app.component.css']
```

(an array)

while your modern project uses:

```typescript
styleUrl: './app.css'
```

(a single string)

Both are valid in their respective Angular versions and project styles. Since we're following the modern Angular CLI output, we'll use `styleUrl` throughout the course, and I'll point out older syntax only when it's useful for understanding legacy code or exam questions.
