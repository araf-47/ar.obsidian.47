Excellent! 🎉

You've reached the final lesson of **Module 4**.

By the end of this lesson, you'll have learned the core built-in directives that every Angular developer uses daily.

Here's what you've completed so far:

* ✅ `*ngIf` — Conditionally create/remove elements.
* ✅ `*ngFor` — Repeat elements.
* ✅ `ngClass` — Dynamically apply CSS classes.

Now we'll learn the last one:

* ✅ `ngStyle` — Dynamically apply **inline CSS styles**.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.7 — `ngStyle`

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* ✅ Lesson 4.4 — `*ngFor`
* ✅ Lesson 4.5 — Attribute Directives
* ✅ Lesson 4.6 — `ngClass`
* 🟨 Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what `ngStyle` does.
* Apply inline CSS styles dynamically.
* Bind one or many CSS properties.
* Understand when to use `ngStyle` versus `ngClass`.
* Know the best practices for styling in Angular.

***

# Prerequisites

You should already understand:

* ✅ CSS
* ✅ Property Binding (`[]`)
* ✅ `ngClass`

***

# Part 1 — Motivation

Imagine you're building a weather application.

When the temperature is high:

```text
Temperature: 38°C
```

The text should become **red**.

When it's cold:

```text
Temperature: 12°C
```

The text should become **blue**.

You could create CSS classes like:

```css
.hot {
  color: red;
}

.cold {
  color: blue;
}
```

and use `ngClass`.

But what if the color comes directly from the database?

Example:

```typescript
temperatureColor = "#FF5733";
```

You don't know the color beforehand.

Creating a CSS class for every possible color isn't practical.

That's where `ngStyle` shines.

***

# Part 2 — What is `ngStyle`?

### Definition

> `ngStyle` is an **attribute directive** that dynamically sets one or more **inline CSS styles** on an element.

It does **not**:

* Create elements
* Remove elements
* Repeat elements

It simply changes style properties on an existing element.

***

# Part 3 — Basic Syntax

Component:

```typescript
export class App {

  textColor = 'blue';

}
```

Template:

```html
<p [ngStyle]="{ color: textColor }">
  Hello Angular
</p>
```

Output:

The paragraph appears in **blue**.

Now change:

```typescript
textColor = 'green';
```

Angular immediately updates the text color.

***

# Part 4 — Your First Hands-on Exercise

## Step 1

`app.ts`

```typescript
export class App {

  isHot = true;

}
```

***

## Step 2

`app.html`

```html
<h2>Today's Weather</h2>

<p
  [ngStyle]="{
    color: isHot ? 'red' : 'blue'
  }">
  Temperature
</p>
```

***

## Step 3

Run the application.

Now change:

```typescript
isHot = false;
```

The text changes from **red** to **blue**.

***

# Part 5 — Multiple Styles

You can set several styles at once.

```html
<p
  [ngStyle]="{
    color: 'white',
    backgroundColor: 'green',
    fontSize: '24px'
  }">

  Success

</p>
```

Angular applies all three styles.

***

# Part 6 — Dynamic Values

Styles don't have to be fixed.

Component:

```typescript
fontSize = 20;

favoriteColor = 'purple';
```

Template:

```html
<p
  [ngStyle]="{
    fontSize: fontSize + 'px',
    color: favoriteColor
  }">

  Angular

</p>
```

When the component values change, Angular updates the styles automatically.

***

# Part 7 — `style`, `[style]`, and `[ngStyle]`

Just like `class` and `ngClass`, there are several ways to apply styles.

## Plain `style`

```html
<p style="color:red">
  Hello
</p>
```

Always red.

Never changes.

***

## Property Binding

```html
<p [style.color]="textColor">
  Hello
</p>
```

Only the `color` property is dynamic.

This is great when you're changing **one** style.

***

## `ngStyle`

```html
<p
  [ngStyle]="{
    color: textColor,
    fontSize: fontSize + 'px',
    backgroundColor: bgColor
  }">
```

Use this when several styles are dynamic.

***

# Part 8 — `ngClass` vs. `ngStyle`

This is one of the most common interview questions.

## `ngClass`

Changes CSS classes.

Example:

```html
<p [ngClass]="{
  error: hasError
}">
```

The CSS class controls the appearance.

***

## `ngStyle`

Changes CSS properties directly.

Example:

```html
<p [ngStyle]="{
  color: 'red'
}">
```

No CSS class is needed.

***

## Which should you use?

**Prefer `ngClass`** when:

* The styles are predefined.
* You already have CSS classes.
* Multiple elements share the same styling.

**Use `ngStyle`** when:

* Style values are dynamic.
* Values come from user input, an API, or calculations.
* You only need to change one or two properties.

***

# Part 9 — Real-World Examples

## Progress Bar

```html
<div
  [ngStyle]="{
    width: progress + '%'
  }">
</div>
```

***

## User Font Size Preference

```html
<p
  [ngStyle]="{
    fontSize: userFontSize + 'px'
  }">
```

***

## Theme Color

```html
<div
  [ngStyle]="{
    backgroundColor: themeColor
  }">
```

***

## Product Card

```html
<div
  [ngStyle]="{
    borderColor: product.color
  }">
```

***

# Under the Hood

Suppose you write:

```html
<p
  [ngStyle]="{
    color: 'green',
    fontSize: '24px'
  }">
```

Angular evaluates the object and updates the element's inline style.

Conceptually, it performs actions like:

```text
element.style.color = 'green'

element.style.fontSize = '24px'
```

It doesn't recreate the element—it simply updates its style properties.

***

# Common Beginner Mistakes

## ❌ Forgetting the square brackets

Wrong:

```html
<p ngStyle="...">
```

Correct:

```html
<p [ngStyle]="{ color: 'red' }">
```

***

## ❌ Forgetting CSS units

Wrong:

```typescript
fontSize = 20;
```

```html
fontSize: fontSize
```

This produces an invalid CSS value.

Correct:

```html
fontSize: fontSize + 'px'
```

***

## ❌ Using `ngStyle` for everything

If your styles are already defined in CSS classes, prefer `ngClass`.

This keeps your HTML cleaner and your styles easier to maintain.

***

# Mini Challenge

Build a "User Profile" card.

Component:

```typescript
isPremium = true;

fontSize = 22;
```

Requirements:

* If `isPremium` is true:

  * Text color should be **gold**.
* Otherwise:

  * Text color should be **gray**.
* Font size should come from the `fontSize` variable.

Try solving it before checking the examples.

***

# Quick Review

Without looking back:

1. What does `ngStyle` do?
2. Is it a structural or attribute directive?
3. What is the difference between `[style.color]` and `[ngStyle]`?
4. When would you choose `ngClass` instead?
5. Why do numeric CSS values often need `'px'` appended?

***

# Lesson Summary

Today you learned:

* ✅ What `ngStyle` is.
* ✅ How to dynamically change inline styles.
* ✅ Single and multiple style bindings.
* ✅ The difference between `style`, `[style]`, and `[ngStyle]`.
* ✅ When to use `ngStyle` versus `ngClass`.

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
* ✅ Lesson 4.6 — `ngClass`
* ✅ Lesson 4.7 — `ngStyle`

⭐ **Appendix (Modern Angular Notes)** *(after the core roadmap)*

* ⬜ `@if`
* ⬜ `@for`
* ⬜ Reading old vs. new Angular syntax
* ⬜ Migration overview

***

# 🎯 Mental Model

Imagine an HTML element as a person getting dressed.

* **`class`** is like giving them a predefined outfit:

  * "Wear the **student uniform**."
  * "Wear the **admin uniform**."

  That's what `ngClass` does—it chooses **which outfit (CSS class)** to wear.

* **`ngStyle`** is like adjusting individual pieces of clothing:

  * Make the shirt **blue**.
  * Increase the hat size.
  * Add a red scarf.

  You're changing individual style properties directly instead of selecting a complete outfit.

***

# 📚 Module 4 Complete! 🎉

Congratulations! You've completed one of the most important modules in Angular.

Here's what you can now do:

* ✅ Decide **whether** an element exists (`*ngIf`).
* ✅ Repeat elements from data (`*ngFor`).
* ✅ Understand the difference between **structural** and **attribute** directives.
* ✅ Dynamically apply CSS classes (`ngClass`).
* ✅ Dynamically apply inline styles (`ngStyle`).

These concepts appear in almost every Angular application you'll build.

## What's Next?

Before we jump into the next major module, I'd recommend spending 30–60 minutes building a **small practice project** that combines everything from Modules 1–4. For example, a simple student list or to-do application using components, data binding, `*ngIf`, `*ngFor`, `ngClass`, and `ngStyle`. It will reinforce everything you've learned so far and make the upcoming topics—services, routing, and HTTP—much easier to understand.
