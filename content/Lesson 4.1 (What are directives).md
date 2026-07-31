Perfect. From this point onward, **Module 4 officially begins**. We'll ignore the previous partial lessons and treat this as the canonical version. If you ever come back weeks or months later and say:

> "Continue from Module 4, Lesson 4.3."

I'll know exactly where we are.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.1 — What are Directives?

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* 🟨 Lesson 4.1 — What are Directives?
* ⬜ Lesson 4.2 — Structural Directives
* ⬜ Lesson 4.3 — `*ngIf`
* ⬜ Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Define what a directive is.
* Explain why Angular needs directives.
* Understand the three categories of directives.
* Distinguish between components and other directives.
* Build the mental model needed for the rest of Module 4.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Data Binding (`{{}}`, `[]`, `()`, `[()]`)
* ✅ Pipes

***

# Part 1 — Motivation: Why Do Directives Exist?

Let's imagine you're building a simple dashboard.

Your HTML might look like this:

```html
<h1>Dashboard</h1>

<button>Save</button>

<p>Welcome Araf</p>
```

Everything looks fine.

But now your client asks:

> "Only show the **Save** button if the user has permission."

A little later they ask:

> "Display every product in our inventory."

Then:

> "Highlight overdue tasks in red."

Then:

> "Hide the admin panel for normal users."

Notice something?

The HTML itself isn't enough anymore.

HTML can describe **what exists**, but it cannot easily describe **dynamic behavior** like:

* Show this.
* Hide that.
* Repeat this.
* Change this style.
* React to changing data.

Angular solves these problems using **directives**.

***

# Part 2 — What Is a Directive?

### Definition

> **A directive is an instruction that tells Angular how to create, modify, or manage an HTML element.**

Think of HTML as a blueprint.

```text
House Blueprint

Door

Window

Roof
```

The blueprint only describes the house.

Now imagine giving instructions to the builders:

```text
Paint this wall.

Remove this window.

Build another room.

Change the roof color.
```

Those instructions are like **directives**.

The HTML provides the structure.

The directive tells Angular what to do with that structure.

***

# Part 3 — Angular Without Directives

Suppose you write:

```html
<button>Login</button>
```

The browser simply creates a button.

Nothing more.

Angular can do much more.

Imagine writing:

```html
<button *ngIf="isLoggedIn">
    Logout
</button>
```

Now Angular asks:

> Is `isLoggedIn` true?

If yes:

Create the button.

If no:

Don't create it at all.

That's far beyond what plain HTML can do.

This is the power of directives.

***

# Part 4 — Three Types of Directives

Angular has **three categories** of directives.

***

## 1. Components

Surprise!

A component is actually a **special kind of directive**.

When you write:

```typescript
@Component({
  selector: 'app-user',
  templateUrl: './user.html'
})
```

Angular creates a directive that also has:

* a template
* styles
* logic

Think of a component as:

> **A directive with its own view (template).**

***

## 2. Structural Directives

Structural directives change the **structure** of the DOM.

They answer questions like:

* Should this element exist?
* How many copies should exist?

Examples:

* `*ngIf`
* `*ngFor`

We'll study these next.

***

## 3. Attribute Directives

Attribute directives **do not** create or remove elements.

Instead, they change:

* appearance
* behavior
* CSS classes
* styles

Examples:

* `ngClass`
* `ngStyle`

***

# Part 5 — A Simple Analogy

Imagine a classroom.

The desks represent HTML elements.

### Structural Directive

The teacher says:

> Remove three desks.

Now fewer desks exist.

***

Another instruction:

> Add five more desks.

Now more desks exist.

The classroom layout changed.

***

### Attribute Directive

Instead, the teacher says:

> Paint all desks blue.

The desks are still there.

Only their appearance changed.

***

# Visual Summary

```text
HTML Element

↓

Directive

↓

Angular decides what to do
```

Examples:

```text
Element

↓

Show it
```

```text
Element

↓

Hide it
```

```text
Element

↓

Repeat it
```

```text
Element

↓

Change its color
```

***

# Part 6 — Where Have You Already Seen Directives?

Even before Module 4, you've already used Angular directives without realizing it.

For example:

```html
<input [(ngModel)]="username">
```

`ngModel` is a directive.

Another example:

```html
<div [ngClass]="...">
```

`ngClass` is a directive.

The `@Component` decorator defines a component, and that component is a special type of directive.

So directives are not something completely new—they've been part of Angular all along.

Module 4 simply focuses on understanding them in depth.

***

# Under the Hood

Angular doesn't read your HTML like a normal browser.

It first analyzes your template.

Whenever Angular encounters a directive, it asks:

> "Does this directive need to create elements?"

> "Does it need to remove anything?"

> "Does it need to update classes?"

Then Angular builds the final DOM that the browser displays.

This is one reason Angular applications can remain synchronized with your component data.

***

# Hands-on Exercise

No coding yet.

Instead, look at each situation below and decide whether you think a directive is needed.

### Situation 1

Show a message only when a user is logged in.

Needs a directive?

✅ Yes.

***

### Situation 2

Display 50 products.

Needs a directive?

✅ Yes.

***

### Situation 3

Change a button to red when an error occurs.

Needs a directive?

✅ Yes.

***

### Situation 4

Display:

```html
<h1>Hello</h1>
```

Needs a directive?

❌ No.

Plain HTML is enough.

***

# Common Beginner Mistakes

### ❌ Thinking directives are HTML

They're not.

Directives are Angular features that work **with** HTML.

***

### ❌ Thinking every directive creates elements

Only **structural directives** create or remove elements.

***

### ❌ Thinking components and directives are unrelated

==Every component is a directive==.

Not every directive is a component.

***

# Mini Challenge

For each situation, identify whether you think you'll eventually use a **structural directive** or an **attribute directive**.

1. Hide the login button after the user signs in.
2. Display every student in a class list.
3. Make overdue tasks appear in red.
4. Increase the font size of a selected item.

Don't worry if you can't answer all of them yet—we'll revisit these after Lessons 4.2 through 4.7.

***

# Quick Review

Without looking back:

1. What is a directive?
2. Why does Angular need directives?
3. What are the three categories of directives?
4. Which type of directive is a component?
5. What is the main difference between structural and attribute directives?

***

# Lesson Summary

Today you learned:

* ✅ What a directive is.
* ✅ Why directives exist.
* ✅ The three categories of directives.
* ✅ That components are special directives.
* ✅ The high-level difference between structural and attribute directives.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ⬜ Lesson 4.2 — Structural Directives
* ⬜ Lesson 4.3 — `*ngIf`
* ⬜ Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

⭐ **Appendix (Modern Angular Notes)**

* `@if`
* `@for`
* Reading old vs. new syntax
* Migration overview

***

## 🎯 Mental Model to Remember

Up to this point, you can think of Angular like this:

* **Components** store data and logic.
* **Templates** describe the UI.
* **Data binding** connects data with the UI.
* **Directives** tell Angular **how the UI itself should behave**.

That's the key idea to carry into the rest of Module 4.

***

### 📚 Instructor's Note

One thing I'll do throughout the rest of this module is compare Angular features with plain HTML, CSS, and JavaScript whenever it helps. The goal isn't just to memorize `*ngIf` or `ngClass`, but to understand **what problem they solve** and **why Angular provides them**. That understanding will make it much easier to learn future topics like routing, forms, and services because you'll see Angular as an extension of the web platform rather than a completely separate technology.
