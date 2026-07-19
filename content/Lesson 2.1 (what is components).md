Excellent. Welcome to **Module 2**.

If Module 1 was about **preparing the workshop**, Module 2 is where we actually start **building**.

I'd even say this is the most important module in the course. If you truly understand components, then Angular becomes much easier. If you don't, almost every later topic (services, routing, forms, etc.) will feel confusing because **everything in Angular revolves around components**.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.1 — What is a Component?

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * 🟨 Lesson 2.1 — What is a Component?
  * ⬜ Lesson 2.2 — Component Metadata
  * ⬜ Lesson 2.3 — Component Selector
  * ⬜ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you should be able to answer:

* What is a component?
* Why does Angular use components?
* How does Angular think about a web page?
* What are the parts of a component?
* Why are components reusable?

***

# Before Angular...

Imagine you're building an online shopping website.

The home page might look like this:

```text
------------------------------------------------
Logo

Navigation Bar

-----------------------------------------------

Featured Products

-----------------------------------------------

Categories

-----------------------------------------------

Latest Offers

-----------------------------------------------

Footer
```

Without components, you might write one very large HTML file containing everything.

As the application grows, this file becomes harder to manage.

Imagine adding:

* User Profile
* Shopping Cart
* Notifications
* Product Reviews
* Search Bar
* Sidebar
* Chat Widget

Soon, a single file could grow to thousands of lines.

This quickly becomes difficult to read, maintain, and reuse.

***

# Angular's Solution

Angular asks a different question:

> "Why treat the whole page as one unit?"

Instead, it encourages you to split the page into **small, independent pieces**.

Like this:

```text
Application
│
├── Header
├── Navigation
├── Search Bar
├── Product List
├── Product Card
├── Shopping Cart
├── Footer
```

Each piece becomes a **component**.

***

# So, What Is a Component?

A component is a **self-contained part of the user interface** that combines:

* its own logic,
* its own template (HTML),
* and its own styles (CSS).

In simple terms:

> A component is a reusable building block of an Angular application.

***

# Think of LEGO Bricks

This analogy is used often because it fits well.

Imagine building a castle.

You don't carve the castle from one giant block.

Instead, you assemble many LEGO bricks.

```text
Castle

↓

Many LEGO Bricks

↓

Each brick has its own purpose.
```

Angular works the same way.

```text
Application

↓

Many Components

↓

Each component has one responsibility.
```

For example:

```text
Application
│
├── HeaderComponent
├── MenuComponent
├── ProductComponent
├── CartComponent
├── FooterComponent
```

Together they form the complete application.

***

# ==Why Components==?

Suppose you have a navigation bar.

Without components:

You might copy the same HTML into:

* Home
* Products
* About
* Contact
* Dashboard

Now imagine the company changes its logo.

You would need to update every copy.

With a component:

```text
Navigation Component

↓

Used everywhere

↓

Change it once

↓

Every page updates
```

That's the power of reuse.

***

# What Does a Component Contain?

A component usually consists of three parts.

```text
Component

├── Logic
├── Template
└── Styles
```

Let's look at each one.

***

## 1. Logic

This is the TypeScript code.

It answers questions like:

* What data should be displayed?
* What happens when a button is clicked?
* What should happen when the component starts?

For example:

```typescript
title = "Angular Course";
```

***

## 2. Template

This is the HTML.

It describes **what the user sees**.

Example:

```html
<h1>{{ title }}</h1>
```

The template doesn't store the data—it displays it.

***

## 3. Styles

This is the CSS for that component.

Example:

```css
h1 {
    color: blue;
}
```

These styles are associated with the component, helping keep the UI organized.

***

# One Component = One Job

A good component should have **one primary responsibility**.

For example:

✅ Login Form

✅ Navigation Bar

✅ Product Card

✅ Footer

Instead of:

❌ Login + Cart + Profile + Dashboard + Settings all in one component.

This idea is related to the **Single Responsibility Principle**, a software design guideline that encourages each unit of code to have one clear purpose.

***

# Real Example

Imagine YouTube.

Can you identify the components?

```text
YouTube

│

├── Header

├── Search Bar

├── Sidebar

├── Video List

├── Video Card

├── Comments

├── Suggested Videos

└── Footer
```

Each of those could be implemented as a separate Angular component.

***

# Components Can Contain Other Components

This is one of Angular's strengths.

Imagine:

```text
App Component

│

├── Header Component

├── Sidebar Component

│      ├── Menu Item

│      ├── Menu Item

│      └── Menu Item

├── Dashboard Component

│      ├── Statistics Card

│      ├── User List

│      └── Chart

└── Footer Component
```

Notice something?

Components can be nested inside other components.

This creates a **component tree**, where larger components are built from smaller ones.

***

# The Root Component

Every Angular application starts with one special component.

It is called the **root component**.

Think of it as the top of the tree.

```text
Root Component

│

├── Header

├── Home

│      ├── Products

│      ├── Categories

│      └── Reviews

└── Footer
```

Every other component ultimately connects back to the root.

In your project, the root component was created automatically when you ran `ng new`.

We'll inspect it in the next lessons.

***

# Mental Model

Don't think:

> "A component is just an HTML file."

Instead, think:

```text
Component

=

HTML

+

TypeScript

+

CSS

+

Behavior

+

Reusable UI
```

That's much closer to how Angular sees it.

***

# Common Beginner Misconceptions

### ❌ "A component is only HTML."

No. HTML is just one part.

The component also includes logic and styles.

***

### ❌ "Every page is one component."

Usually, a page is composed of **many** components working together.

***

### ❌ "Components cannot communicate."

They can. In Module 5, you'll learn how parent and child components exchange data and events.

***

### ❌ "I should make one giant component."

A better practice is to divide your application into small, focused, reusable components.

***

# Hands-on Exercise

Without writing any code yet, choose a website you use often (for example: YouTube, Facebook, Amazon, Daraz, GitHub).

Draw or list the components you think it contains.

For example:

```text
GitHub

├── Navigation Bar
├── Repository Header
├── File List
├── README Viewer
├── Right Sidebar
└── Footer
```

This exercise helps you start seeing user interfaces the way Angular developers do.

***

# Quick Review

Try answering these without looking back:

1. What is a component?
2. Why does Angular use components instead of one large page?
3. What are the three main parts of a component?
4. Why are reusable components useful?
5. What is the root component?

***

# Lesson Summary

Today you learned:

* ✅ What a component is.
* ✅ Why Angular is component-based.
* ✅ The three main parts of a component.
* ✅ Why components are reusable.
* ✅ That components can contain other components.
* ✅ That every Angular application has a root component.

***

## Roadmap Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ⬜ Lesson 2.2 — Component Metadata
  * ⬜ Lesson 2.3 — Component Selector
  * ⬜ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

## A small improvement to our roadmap

Starting with the next lesson, we'll spend much more time **inside the actual code**. Rather than showing isolated snippets, I'll use the files that `ng new` generated in **your own project**. That way, every concept you learn is tied directly to code you can open, edit, and run on your Debian laptop. This makes the lessons much more practical and helps bridge the gap between theory and real Angular development.
