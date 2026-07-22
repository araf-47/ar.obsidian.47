Excellent. This is one of the most exciting lessons in Angular.

Until now, your component has been **sending data to the UI**.

Now we'll reverse the direction.

The **user** will interact with the page, and your **TypeScript code** will respond.

This is how buttons, forms, menus, and almost every interactive web application works.

***

# Angular Master Course

# Module 3 — Templates & Data Binding

## Lesson 3.3 — Event Binding (`()`)

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* 🟨 Lesson 3.3 — Event Binding (`()`)
* ⬜ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what event binding is.
* Understand how Angular responds to user actions.
* Use the event binding syntax `()`.
* Call component methods from the template.
* Pass the event object to a method.
* Know the difference between property binding and event binding.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Interpolation
* ✅ Property Binding

***

# Part 1 — Why Do We Need Event Binding?

Imagine this button:

```html
<button>Click Me</button>
```

It appears on the screen.

But...

What happens when you click it?

Nothing.

HTML creates the button, but **it doesn't tell your Angular component that the button was clicked**.

You need a way to connect a user's action to your TypeScript code.

That connection is **event binding**.

***

# What Is Event Binding?

**Definition:**

> Event binding allows your component to respond to events that occur in the template.

General syntax:

```html
(event)="method()"
```

Whenever you see:

```text
()
```

think:

> **Template → Component**

The data flows from the UI back to your TypeScript code.

***

# Visual Flow

```text
User

↓

Button Click

↓

Angular

↓

Component Method
```

Unlike property binding:

```text
Component

↓

HTML
```

Event binding goes the opposite direction.

***

# Your First Event Binding

Component:

```typescript
export class App {

  sayHello() {
    alert('Hello, Angular!');
  }

}
```

Template:

```html
<button (click)="sayHello()">
  Click Me
</button>
```

What happens?

1. The user clicks the button.
2. Angular detects the `click` event.
3. Angular calls `sayHello()`.
4. The alert appears.

***

# The `click` Event

`click` is one of many events supported by HTML.

Some common events are:

| Event        | Triggered When                              |
| --------- | ------------------------------------------- |
| `click`      | User clicks an element                      |
| `dblclick`   | User double-clicks                          |
| `input`      | User changes an input's value               |
| `change`     | Value is committed (depends on the element) |
| `keyup`      | A key is released                           |
| `keydown`    | A key is pressed                            |
| `mouseenter` | Mouse enters an element                     |
| `mouseleave` | Mouse leaves an element                     |

Angular listens for these events using the same event names.

***

# Calling Component Methods

Suppose you have:

```typescript
export class App {

  save() {
    console.log('Saved!');
  }

}
```

Template:

```html
<button (click)="save()">
  Save
</button>
```

Each click runs:

```typescript
save()
```

Notice that the method is defined in the component, not in the HTML.

Remember our rule:

> **The template describes what should happen. The component contains the logic.**

***

# Updating Component Data

Instead of showing an alert, let's update a variable.

Component:

```typescript
export class App {

  count = 0;

  increase() {
    this.count++;
  }

}
```

Template:

```html
<h2>{{ count }}</h2>

<button (click)="increase()">
  Increase
</button>
```

When the button is clicked:

```text
0

↓

1

↓

2

↓

3
```

Angular automatically updates the page.

Notice what happened:

* Event binding called the method.
* The method changed the variable.
* Interpolation displayed the new value.

You've now used **two different kinds of data binding together**.

***

# Passing the Event Object

Sometimes you want information about the event itself.

Angular provides a special variable:

```text
$event
```

Example:

```html
<input (input)="onInput($event)">
```

Component:

```typescript
onInput(event: Event) {
  console.log(event);
}
```

When the user types, Angular passes the browser's event object to your method.

The event object contains information such as:

* Which element triggered the event.
* The event type.
* Keyboard or mouse information (depending on the event).

We'll use `$event` more often later in the course.

***

# Property Binding vs Event Binding

This is an important comparison.

### Property Binding

```html
<button [disabled]="isDisabled">
```

Direction:

```text
Component

↓

Button
```

***

### Event Binding

```html
<button (click)="save()">
```

Direction:

```text
Button

↓

Component
```

A simple way to remember:

* `[]` **sets** something.
* `()` **reacts** to something.

***

# Hands-on Exercise

## Step 1

Open:

```text
src/app/app.ts
```

Replace the class with:

```typescript
export class App {

  count = 0;

  increase() {
    this.count++;
  }

  reset() {
    this.count = 0;
  }

}
```

***

## Step 2

Open:

```text
src/app/app.html
```

Replace the contents with:

```html
<h1>Event Binding Demo</h1>

<h2>Count: {{ count }}</h2>

<button (click)="increase()">
  Increase
</button>

<button (click)="reset()">
  Reset
</button>
```

***

## Step 3

Save the files.

Try:

* Clicking **Increase** several times.
* Clicking **Reset**.

Observe:

* The component variable changes.
* Angular updates the page automatically.

***

# Extra Exercise

Add another method:

```typescript
decrease() {
  this.count--;
}
```

Then add another button:

```html
<button (click)="decrease()">
  Decrease
</button>
```

Now you have a simple counter application.

***

# Common Beginner Mistakes

## ❌ Forgetting the parentheses

Wrong:

```html
<button click="increase()">
```

This is plain HTML, not Angular event binding.

Correct:

```html
<button (click)="increase()">
```

***

## ❌ Writing `this` in the template

Wrong:

```html
<button (click)="this.increase()">
```

Templates don't use `this`.

Correct:

```html
<button (click)="increase()">
```

***

## ❌ Expecting a method to run automatically

This:

```html
(click)="increase()"
```

only runs when the event occurs.

It does not execute when the page loads.

***

# Quick Review

Without looking back:

1. What is event binding?
2. What syntax does event binding use?
3. Which direction does the data flow?
4. What is `$event`?
5. Why doesn't the template contain the actual business logic?

***

# Lesson Summary

Today you learned:

* ✅ What event binding is.
* ✅ The `()` syntax.
* ✅ How to call component methods.
* ✅ How to update component data from user actions.
* ✅ How interpolation and event binding work together.
* ✅ How to access the event object using `$event`.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ✅ Lesson 3.3 — Event Binding (`()`)
* ⬜ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

## 🔍 A Note About Browser Events

One important point to understand is that Angular **doesn't invent events like `click`, `input`, or `keyup`**. These are standard browser (DOM) events.

Angular's job is to provide a clean, declarative way to listen for them:

```html
<button (click)="increase()">
```

instead of manually writing JavaScript like:

```javascript
button.addEventListener('click', () => {
  // ...
});
```

This is a recurring pattern in Angular: it builds on standard web technologies rather than replacing them. As you continue learning, you'll often see Angular provide a more structured and maintainable way to work with features that already exist in HTML, CSS, and JavaScript.
