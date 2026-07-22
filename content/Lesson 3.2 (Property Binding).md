Perfect. Now that you understand **interpolation**, we can move to the next type of data binding.

One thing to remember throughout Module 3:

| Binding Type     | Data Flow                   |
| ---------------- | --------------------------- |
| Interpolation    | Component → Template (Text) |
| Property Binding | Component → DOM Property    |
| Event Binding    | Template → Component        |
| Two-Way Binding  | Both Directions             |

Notice how we're building the complete picture one piece at a time.

***

# Angular Master Course

# Module 3 — Templates & Data Binding

## Lesson 3.2 — Property Binding (`[]`)

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* 🟨 Lesson 3.2 — Property Binding (`[]`)
* ⬜ Lesson 3.3 — Event Binding (`()`)
* ⬜ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what property binding is.
* Distinguish between interpolation and property binding.
* Understand the syntax of property binding.
* Bind values to common DOM properties.
* Know when to use property binding instead of interpolation.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Interpolation (`{{ }}`)

***

# Part 1 — Why Do We Need Property Binding?

Suppose you have this component:

```typescript
export class App {
  imageUrl = 'https://picsum.photos/300';
}
```

You want to display the image.

Can you write this?

```html
<img>{{ imageUrl }}</img>
```

No.

Why?

Because the image URL doesn't belong **inside** the `<img>` element.

It belongs to the image's **`src` property**.

Angular needs another way to bind values to element properties.

That way is **property binding**.

***

# What Is Property Binding?

**Definition:**

> Property binding allows you to bind a value from your component to a property of a DOM element.

General syntax:

```html
[property]="expression"
```

Whenever you see:

```text
[]
```

think:

> **Component → HTML Element Property**

The data flows in one direction.

***

# Interpolation vs Property Binding

Let's compare them.

### Interpolation

```typescript
title = "Angular";
```

```html
<h1>{{ title }}</h1>
```

Result:

```html
<h1>Angular</h1>
```

Interpolation places text **inside** an element.

***

### Property Binding

```typescript
imageUrl = "https://picsum.photos/300";
```

```html
<img [src]="imageUrl">
```

Result:

Angular assigns the value to the image's `src` property.

***

# Visual Comparison

Interpolation:

```text
Component

title

↓

Text Node

↓

<h1>Angular</h1>
```

Property Binding:

```text
Component

imageUrl

↓

src Property

↓

<img>
```

***

# Part 2 — HTML Attributes vs DOM Properties

This topic confuses almost every beginner.

Let's clear it up.

When you write:

```html
<input type="text">
```

`type="text"` is an **HTML attribute**.

When the browser loads the page, it creates an object representing that input.

That object has **properties** such as:

* `value`
* `disabled`
* `checked`
* `hidden`
* `id`

Angular property binding updates these **properties**.

For now, you don't need to memorize the technical distinction.

Just remember:

> Property binding updates the **live DOM object**, not the original HTML text.

***

# Part 3 — Common Examples

## Example 1 — Image Source

Component:

```typescript
export class App {
  imageUrl = 'https://picsum.photos/250';
}
```

Template:

```html
<img [src]="imageUrl" alt="Random Image">
```

Angular sets:

```text
img.src = imageUrl
```

***

## Example 2 — Disable a Button

Component:

```typescript
export class App {
  isDisabled = true;
}
```

Template:

```html
<button [disabled]="isDisabled">
  Save
</button>
```

Result:

The button is disabled.

Now change:

```typescript
isDisabled = false;
```

The button immediately becomes clickable.

***

## Example 3 — Input Value

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

The input displays:

```text
Araf
```

But if the user types:

```text
John
```

The component variable **does not change**.

Why?

Because property binding is **one-way**.

We'll solve this in Lesson **3.4** with two-way binding.

***

## Example 4 — Checkbox

Component:

```typescript
export class App {
  accepted = true;
}
```

Template:

```html
<input type="checkbox" [checked]="accepted">
```

If `accepted` is `true`, the checkbox starts checked.

***

## Example 5 — Hide an Element

Component:

```typescript
export class App {
  isHidden = false;
}
```

Template:

```html
<p [hidden]="isHidden">
  This text may disappear.
</p>
```

Change:

```typescript
isHidden = true;
```

The paragraph becomes hidden.

***

# Part 4 — Can Interpolation Do the Same Thing?

Sometimes you'll see:

```html
<img src="{{ imageUrl }}">
```

Angular often supports this.

However, the recommended style is:

```html
<img [src]="imageUrl">
```

Why?

Because:

* It's clearer.
* It directly binds the DOM property.
* It works consistently with all property bindings.

### Rule of Thumb

* **Display text** → Interpolation.
* **Set an element property** → Property binding.

***

# Part 5 — How Angular Processes Property Binding

Suppose you have:

```html
<button [disabled]="isDisabled">
```

Angular conceptually performs:

```text
Read component

↓

Evaluate isDisabled

↓

Find button element

↓

Set button.disabled

↓

Render the result
```

Whenever `isDisabled` changes, Angular updates the button automatically.

You don't need to manually manipulate the DOM.

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

  imageUrl = 'https://picsum.photos/250';

  isDisabled = true;

  username = 'Araf';

  accepted = true;

  isHidden = false;

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
<h1>Property Binding Demo</h1>

<img [src]="imageUrl" alt="Random Image">

<br><br>

<button [disabled]="isDisabled">
  Save
</button>

<br><br>

<input [value]="username">

<br><br>

<label>
  <input type="checkbox" [checked]="accepted">
  Accept Terms
</label>

<p [hidden]="isHidden">
  This paragraph is visible.
</p>
```

***

## Step 3

Save the files.

Observe:

* The image loads.
* The button is disabled.
* The input contains your username.
* The checkbox is checked.
* The paragraph is visible.

Now experiment:

```typescript
isDisabled = false;

accepted = false;

isHidden = true;
```

Save after each change.

Watch Angular update the page automatically.

***

# Common Beginner Mistakes

## ❌ Forgetting the square brackets

Wrong:

```html
<img src="imageUrl">
```

The browser treats `"imageUrl"` as plain text.

Correct:

```html
<img [src]="imageUrl">
```

***

## ❌ Quoting the variable

Wrong:

```html
<button [disabled]="'isDisabled'">
```

This passes the string `"isDisabled"`.

Correct:

```html
<button [disabled]="isDisabled">
```

***

## ❌ Expecting two-way behavior

This:

```html
<input [value]="username">
```

does **not** update `username` when the user types.

It only displays the component's value.

***

# Quick Review

Without looking back:

1. What is property binding?
2. What syntax does property binding use?
3. Which direction does the data flow?
4. When should you use property binding instead of interpolation?
5. Does changing the input field update the component when using `[value]`?

***

# Lesson Summary

Today you learned:

* ✅ What property binding is.
* ✅ The `[]` syntax.
* ✅ How property binding differs from interpolation.
* ✅ How Angular updates DOM properties.
* ✅ Common DOM properties such as `src`, `disabled`, `checked`, `value`, and `hidden`.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ⬜ Lesson 3.3 — Event Binding (`()`)
* ⬜ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

## 📌 A Small Improvement to Our Course

From this lesson onward, whenever we introduce new Angular syntax, I'll also point out **how it relates to plain HTML and JavaScript**. That comparison makes it much easier to understand *why* Angular has a particular feature instead of just memorizing its syntax.

For example, today you learned that `[disabled]` doesn't invent a new HTML feature—it lets Angular control the existing `disabled` property of the DOM element. Understanding that connection will make future topics like directives and forms much more intuitive.
