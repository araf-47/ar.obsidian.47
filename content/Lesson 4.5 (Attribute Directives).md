Excellent! 🎉

You've now completed the two most important **structural directives**:

* ✅ `*ngIf` → Controls **whether an element exists**.
* ✅ `*ngFor` → Controls **how many copies of an element exist**.

Now we'll move to the second major category of directives.

Unlike structural directives, **attribute directives never add or remove elements**. They only change the appearance or behavior of elements that already exist.

This distinction is one of the most important concepts in Angular.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.5 — Attribute Directives

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* ✅ Lesson 4.4 — `*ngFor`
* 🟨 Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what an attribute directive is.
* Distinguish attribute directives from structural directives.
* Understand when to use each type.
* Recognize common built-in attribute directives.
* Prepare for `ngClass` and `ngStyle`.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Data Binding
* ✅ Structural Directives (`*ngIf`, `*ngFor`)

***

# Part 1 — Motivation

Imagine you're building a student portal.

You have this button:

```html
<button>Submit Assignment</button>
```

The teacher now asks:

> "When the assignment has already been submitted, make the button green."

Notice what **didn't** change:

* The button still exists.
* The button is still clickable.
* The button is still in the same place.

Only its **appearance** changes.

Now another request:

> "Disable the button after submission."

Again:

The button still exists.

Only its **behavior** changes.

This is exactly what attribute directives are for.

***

# Part 2 — What Is an Attribute Directive?

### Definition

> An **attribute directive** changes the appearance or behavior of an existing HTML element without changing the structure of the DOM.

Unlike structural directives, attribute directives **never**:

* create elements,
* remove elements,
* repeat elements.

Instead, they modify elements that are already on the page.

***

# Part 3 — Structural vs. Attribute

Let's compare them.

Suppose we have:

```html
<button>Save</button>
```

### Structural Directive

Question:

> Should this button exist?

Possible answer:

No.

Angular removes the button.

***

### Attribute Directive

Question:

> The button exists. How should it look or behave?

Possible answers:

* Blue
* Disabled
* Bold
* Larger font
* Add a CSS class

The button remains in the DOM.

***

# Visual Comparison

## Structural

Before:

```text
Page

Button
```

After removal:

```text
Page
```

The button no longer exists.

***

## Attribute

Before:

```text
Gray Button
```

After:

```text
Blue Button
```

Same button.

Different appearance.

***

# Part 4 — Common Attribute Directives

Angular provides several built-in attribute directives.

You'll learn these next.

### `ngClass`

Changes CSS classes dynamically.

Example idea:

```text
If score >= 50

↓

Green text

Else

↓

Red text
```

***

### `ngStyle`

Changes inline CSS styles dynamically.

Example idea:

```text
If dark mode

↓

Black background

White text
```

***

### `ngModel`

You've already used this one!

```html
<input [(ngModel)]="username">
```

`ngModel` synchronizes the input field with your component data.

It doesn't create or remove the `<input>`.

It changes its behavior.

***

# Part 5 — Real-World Examples

## Online Store

Out-of-stock products appear gray.

The product card still exists.

Only the styling changes.

***

## Todo Application

Completed tasks appear with a line through them.

The task isn't removed.

Only its appearance changes.

***

## Navigation Menu

The current page is highlighted.

The navigation link still exists.

Only its CSS class changes.

***

## Form Validation

An invalid input field gets a red border.

The input still exists.

Only its style changes.

***

# Part 6 — Under the Hood

Suppose Angular encounters:

```html
<button [ngClass]="{ active: isSelected }">
  Save
</button>
```

Angular does **not** ask:

> "Should I create this button?"

Instead, it asks:

> "Should I add the `active` CSS class to this button?"

The button stays where it is.

Only its classes change.

Similarly:

```html
<div [ngStyle]="{ color: 'red' }">
```

Angular updates the style of the `<div>`.

It doesn't replace or recreate the element.

***

# Part 7 — Structural and Attribute Together

These two kinds of directives often work together.

Example:

```html
<button
  *ngIf="isLoggedIn"
  [ngClass]="{ admin: isAdmin }">
  Dashboard
</button>
```

What happens here?

1. `*ngIf` decides **whether the button exists**.
2. If it exists, `ngClass` decides **which CSS classes it should have**.

Think of it as a two-step process:

* Step 1: **Existence**
* Step 2: **Appearance**

***

# Hands-on Thought Exercise

For each situation, decide which type of directive fits best.

### Situation 1

Show the "Admin Panel" only for administrators.

***

### Situation 2

Make overdue tasks appear in red.

***

### Situation 3

Display every student in a class.

***

### Situation 4

Highlight the selected menu item.

***

### Answers

1. Structural
2. Attribute
3. Structural
4. Attribute

***

# Common Beginner Mistakes

## ❌ Thinking attribute directives change the DOM structure

They don't.

==They modify elements that already exist==.

***

## ❌ Confusing CSS with directives

CSS always changes appearance.

Angular attribute directives decide **when and how** those styles or behaviors should be applied.

***

## ❌ Thinking attribute directives replace CSS

They don't.

They usually **work together** with CSS.

For example:

* CSS defines a class named `.active`.
* `ngClass` decides when to apply `.active`.

***

# Mini Challenge

Imagine you're building a music player.

For each feature, identify the correct directive type.

1. Hide the "Play" button while music is already playing.
2. Highlight the currently playing song.
3. Display every song in the playlist.
4. Make favorite songs appear in gold.

Try answering before looking at your notes.

***

# Quick Review

Without looking back:

1. What is an attribute directive?
2. Does an attribute directive change the DOM structure?
3. What is the main difference between structural and attribute directives?
4. Name three built-in attribute directives.
5. Can structural and attribute directives be used together?

***

# Lesson Summary

Today you learned:

* ✅ What attribute directives are.
* ✅ How they differ from structural directives.
* ✅ Common built-in attribute directives.
* ✅ Real-world use cases.
* ✅ How structural and attribute directives work together.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* ✅ Lesson 4.4 — `*ngFor`
* ✅ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

⭐ **Appendix (Modern Angular Notes)**

* `@if`
* `@for`
* Reading old vs. new Angular syntax
* Migration overview

***

# 🎯 Mental Model

Imagine you're building a house.

* **Structural directives** are the construction crew. They decide:

  * Should there be a room here?
  * Should we add another window?
  * Should we remove this wall?

* **Attribute directives** are the interior designers. They decide:

  * What color should the walls be?
  * Which furniture should be highlighted?
  * Should this light be dimmed?

The construction crew changes the **structure** of the house.

The interior designers change the **appearance and behavior** of what has already been built.

Keep this distinction in mind, because in the next lesson you'll learn **`ngClass`**, your first attribute directive, and you'll finally start controlling CSS classes dynamically from Angular.
