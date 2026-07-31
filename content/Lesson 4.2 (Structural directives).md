Now we begin the heart of Module 4.

Lesson 4.1 answered **"What is a directive?"**

Lesson 4.2 answers:

> **"What exactly is a structural directive, and how is it different from other directives?"**

This lesson is mostly conceptual. By the end, `*ngIf` and `*ngFor` will feel natural instead of looking like magic.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.2 — Structural Directives

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* 🟨 Lesson 4.2 — Structural Directives
* ⬜ Lesson 4.3 — `*ngIf`
* ⬜ Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Define a structural directive.
* Explain how structural directives change the DOM.
* Distinguish between hiding an element and removing it.
* Understand why Angular provides structural directives.
* Be ready to learn `*ngIf` and `*ngFor`.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Data Binding
* ✅ What a directive is

***

# Part 1 — Motivation

Let's build a simple shopping application.

Initially, your page looks like this:

```html
<h1>Shopping Cart</h1>

<p>Your cart is empty.</p>
```

Now imagine the user adds an item.

Should the message still be shown?

No.

The message should disappear.

Now another requirement:

> Display every item in the shopping cart.

If there are three products:

* Laptop
* Mouse
* Keyboard

Should you manually write:

```html
<li>Laptop</li>
<li>Mouse</li>
<li>Keyboard</li>
```

What if there are 500 products?

You need Angular to generate the HTML automatically.

This is exactly why structural directives exist.

***

# Part 2 — What Is a Structural Directive?

### Definition

> A **structural directive** is a directive that changes the structure of the DOM by creating, removing, or repeating elements.

Notice the keyword:

**Structure**

Structure means:

* Which elements exist?
* How many elements exist?
* Where do they appear?

Structural directives answer these questions.

***

# Part 3 — ==What Is the DOM==?

Before we continue, we need to understand one important term.

**DOM** stands for:

> **Document Object Model**

When the browser reads HTML, it doesn't work directly with the text.

Instead, it creates an object tree in memory.

Suppose you have:

```html
<body>
    <h1>Angular</h1>

    <p>Hello</p>

    <button>Save</button>
</body>
```

The browser builds something like:

```text
body
├── h1
├── p
└── button
```

This tree is called the **DOM**.

Angular doesn't manipulate raw HTML text after the page loads—it works with this DOM structure.

***

# Part 4 — Changing the Structure

Imagine the user is **not** logged in.

DOM:

```text
body
├── h1
├── button(Login)
└── p
```

Now the user logs in.

Angular decides:

> Remove the Login button.

The DOM becomes:

```text
body
├── h1
└── p
```

The button isn't merely invisible.

It no longer exists in the DOM.

That is a structural change.

***

# Part 5 — Hiding vs. Removing

This is one of the most important ideas in Angular.

Suppose you have this button:

```html
<button>Delete</button>
```

There are two possibilities.

## Option 1 — Hide It

The button still exists.

It simply isn't visible.

Think of putting a cloth over a chair.

The chair is still in the room.

***

## Option 2 — Remove It

The button no longer exists.

Think of taking the chair out of the room.

There is nothing to interact with because it isn't there anymore.

Structural directives do the second one.

They **remove** or **create** elements.

***

# Visual Comparison

### Hidden

```text
Room

Chair (covered)

Table
```

The chair still exists.

***

### Removed

```text
Room

Table
```

The chair is gone.

***

# Part 6 — The Three Main Jobs of Structural Directives

Structural directives usually perform one of these actions.

## 1. Create Elements

Example:

```text
Show the Welcome message after login.
```

Angular creates the element when needed.

***

## 2. Remove Elements

Example:

```text
Hide the Admin Panel for regular users.
```

Angular removes the panel from the DOM.

***

## 3. Repeat Elements

Example:

```text
Products

Laptop

Mouse

Keyboard
```

Angular repeats the same HTML template for every product.

***

# Part 7 — Structural vs. Attribute Directives

Let's compare them side by side.

| Structural Directive      | Attribute Directive            |
| ------------------------- | ------------------------------ |
| Creates elements          | Doesn't create elements        |
| Removes elements          | Doesn't remove elements        |
| Repeats elements          | Doesn't repeat elements        |
| Changes the DOM structure | Changes appearance or behavior |

***

## Example

Structural:

```text
Should this button exist?
```

Attribute:

```text
Should this button be blue?
```

See the difference?

One changes the **existence** of the button.

The other changes **how it looks**.

***

# Part 8 — The Structural Directives You'll Learn

In Angular, the two most common structural directives are:

### `*ngIf`

Used for:

```text
Show it

or

Don't show it
```

***

### `*ngFor`

Used for:

```text
Repeat this HTML
```

You'll master both in the next two lessons.

***

# Under the Hood

Suppose you write:

```html
<button *ngIf="isLoggedIn">
    Logout
</button>
```

Angular doesn't simply "hide" the button.

It evaluates the condition:

```text
isLoggedIn ?

↓

true

↓

Create button
```

or

```text
false

↓

Do not create button
```

This is why structural directives are powerful—they determine the actual structure of the page.

***

# Hands-on Thought Exercise

You don't need to code yet.

For each situation, decide whether Angular needs to create/remove elements or simply change their appearance.

### Situation 1

Display a "No products found" message only when the product list is empty.

***

### Situation 2

Make overdue tasks appear in red.

***

### Situation 3

Display every student in a classroom list.

***

### Situation 4

Increase the font size of a selected paragraph.

***

Think before reading the answers.

***

### Answers

1. Structural
2. Attribute
3. Structural
4. Attribute

***

# Common Beginner Mistakes

## ❌ Thinking "hidden" and "removed" are the same

They are not.

Hidden:

* Exists in the DOM.
* Just not visible.

Removed:

* Doesn't exist in the DOM.

***

## ❌ Thinking structural directives change data

They don't.

They change how Angular renders the template.

***

## ❌ Thinking structural directives only hide things

They can also:

* create,
* remove,
* repeat elements.

***

# Mini Challenge

Imagine you're building a university portal.

Which directive category would you expect to use?

1. Show the "Exam Results" section only after grades are published.
2. Display every enrolled course.
3. Highlight failed courses in red.
4. Increase the font size of the selected course.

Try to answer before moving to the next lesson.

***

# Quick Review

Without looking back:

1. What is a structural directive?
2. What does DOM stand for?
3. What three main jobs do structural directives perform?
4. What is the difference between hiding and removing an element?
5. Name the two most common structural directives.

***

# Lesson Summary

Today you learned:

* ✅ What structural directives are.
* ✅ Why Angular needs them.
* ✅ What the DOM is.
* ✅ The difference between hiding and removing elements.
* ✅ How structural directives differ from attribute directives.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ⬜ Lesson 4.3 — `*ngIf`
* ⬜ Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

⭐ **Appendix (Modern Angular Notes)**

* `@if`
* `@for`
* Reading old vs. new Angular syntax
* Migration overview

***

## 🎯 Mental Model

Here's the mental model I want you to carry into Lesson 4.3:

Imagine your HTML is a **movie script**.

A structural directive is the **director**.

The script might contain a scene, but the director decides:

* "Cut this scene."
* "Repeat this scene three times."
* "Don't film this scene unless the actor arrives."

Similarly, your template describes *possible* UI elements, but **structural directives decide which ones actually become part of the final page**.

In the next lesson, you'll learn your first structural directive, `*ngIf`, which gives Angular the ability to answer one simple but powerful question:

> **"Should this element exist?"**
