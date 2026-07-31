Perfect. Welcome to **Module 5**.

Up until now, every Angular application we've built has lived inside **one component**. That's fine for learning, but it's not how real Angular applications are built.

Real applications are made up of **many small components** that work together.

This module teaches you **how components communicate**.

***

# Angular Master Course

# Module 5 — Component Communication

## Lesson 5.1 — Parent and Child Components

### Progress

```text
✅ Module 1 — Project Setup

✅ Module 2 — Components

✅ Module 3 — Templates & Data Binding

✅ Module 4 — Directives

✅ Module 4A — Modern Angular Control Flow

🟨 Module 5 — Component Communication

    🟨 Lesson 5.1 Parent and Child Components
    ⬜ Lesson 5.2 @Input
    ⬜ Lesson 5.3 @Output
    ⬜ Lesson 5.4 EventEmitter
```

***

# 📌 Version Note

Everything in this lesson works in both **older Angular** and **modern Angular**.

Whether you use standalone components or NgModules, the concept of **parent and child components** is exactly the same.

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what a parent component is.
* Explain what a child component is.
* Understand how Angular applications are built from many components.
* Recognize parent–child relationships in an Angular project.
* Prepare for using `@Input()` and `@Output()`.

***

# Part 1 — Think Bigger Than One Component

So far, we've built pages like this:

```
App Component

┌─────────────────────┐
│     AppComponent    │
│                     │
│  Title              │
│  Button             │
│  List               │
│                     │
└─────────────────────┘
```

Everything lives inside one component.

This works.

But imagine building:

* Facebook
* YouTube
* Amazon
* Gmail

Would you put **everything** into one component?

Of course not.

It would become thousands of lines long and impossible to maintain.

***

# Part 2 — The Lego Analogy

Imagine building a Lego city.

You don't build one giant Lego piece.

Instead, you build many small pieces:

* Houses
* Cars
* Roads
* Trees
* People

Then you assemble them into a city.

Angular works exactly the same way.

Instead of one giant component, you build many small ones.

***

# Part 3 — Example

Imagine a YouTube homepage.

```
YouTube Page

────────────────────────────

Header

Sidebar

Video List

Footer
```

Angular would not create one huge component.

Instead:

```
AppComponent

├── HeaderComponent
├── SidebarComponent
├── VideoListComponent
└── FooterComponent
```

Each piece has one responsibility.

***

# Another Example

Imagine an online shopping website.

```
AppComponent

├── NavbarComponent
├── SearchBarComponent
├── ProductListComponent
├── ShoppingCartComponent
└── FooterComponent
```

Each component focuses on one job.

***

# Part 4 — Parent Component

A **parent component** is a component that **contains another component**.

Example:

```html
<app-header></app-header>

<app-product-list></app-product-list>

<app-footer></app-footer>
```

The component containing these tags is the **parent**.

Think of it as the component that organizes the page.

***

# Part 5 — Child Component

A **child component** is a component that is placed **inside another component's template**.

Example:

```html
<app-product-card></app-product-card>
```

If this appears inside `ProductListComponent`, then:

```
ProductListComponent

└── ProductCardComponent
```

The product list is the parent.

The product card is the child.

***

# Part 6 — Visualizing the Hierarchy

Imagine this application:

```
AppComponent

├── HeaderComponent
├── DashboardComponent
│
│     ├── StatisticsComponent
│     ├── ChartComponent
│     └── RecentOrdersComponent
│
└── FooterComponent
```

Notice something.

A component can be:

* a **child** of another component
* and **also a parent** of other components.

For example:

```
DashboardComponent
```

is

* child of `AppComponent`
* parent of `StatisticsComponent`
* parent of `ChartComponent`
* parent of `RecentOrdersComponent`

So "parent" and "child" are **relationships**, not permanent roles.

***

# Part 7 — How Angular Renders Components

Suppose `app.component.html` contains:

```html
<h1>My Store</h1>

<app-product-list></app-product-list>
```

Angular sees:

```
<app-product-list>
```

and replaces it with the template of `ProductListComponent`.

If `ProductListComponent` contains:

```html
<app-product-card></app-product-card>

<app-product-card></app-product-card>

<app-product-card></app-product-card>
```

Angular renders:

```
My Store

Product Card

Product Card

Product Card
```

Each custom tag represents another Angular component.

***

# Part 8 — A Family Tree

Think of Angular as a family tree.

```
Grandparent

↓

Parent

↓

Child

↓

Grandchild
```

Exactly the same idea.

```
AppComponent

↓

DashboardComponent

↓

ChartComponent

↓

LegendComponent
```

Components form a tree.

That's why you'll often hear the term:

> **Component Tree**

***

# Part 9 — Real Example

Imagine you're building a Landlord Management System (one of the project ideas we've discussed).

Instead of one huge component, you might organize it like this:

```
AppComponent

├── NavbarComponent
├── DashboardComponent
│
├── TenantListComponent
│      ├── TenantCardComponent
│      ├── TenantCardComponent
│      └── TenantCardComponent
│
├── PaymentHistoryComponent
│
└── FooterComponent
```

Notice how each component has a single responsibility.

This makes the application easier to understand, test, and maintain.

***

# Part 10 — Why This Matters

Right now, parent and child components don't exchange information.

They're simply arranged in a hierarchy.

In the next lessons, you'll learn how they communicate.

```
Parent

↓

Pass data

↓

Child
```

using:

```
@Input()
```

Then you'll learn how a child can send information back:

```
Child

↓

Send event

↓

Parent
```

using:

```
@Output()
```

Everything in this module builds on the idea of the component tree.

***

# Common Beginner Mistakes

## ❌ Thinking components are pages

A page can contain many components.

For example, a dashboard page may include:

* Navbar
* Sidebar
* Chart
* Table
* Footer

Each of those can be its own component.

***

## ❌ Making one huge component

Beginners often put everything into `AppComponent`.

Professional Angular applications break the UI into small, reusable pieces.

***

## ❌ Thinking "parent" and "child" are fixed

A component can be both.

For example:

```
AppComponent

↓

DashboardComponent

↓

ChartComponent
```

Here:

* `DashboardComponent` is a **child** of `AppComponent`.
* `DashboardComponent` is also a **parent** of `ChartComponent`.

***

# 💼 Real-World Developer Notes

One of the hardest habits for new Angular developers is deciding **when to create a new component**.

A common guideline is:

> If a part of the UI has its own responsibility, could be reused, or makes the current component much longer, consider extracting it into its own component.

For example, if every tenant in your landlord system is displayed the same way, don't repeat the HTML 20 times. Create a `TenantCardComponent` and reuse it for every tenant.

This keeps your code cleaner and makes future changes much easier.

***

# Mini Challenge

Imagine you're building an **Online Book Store**.

Break it into components.

One possible answer is:

```
AppComponent

├── NavbarComponent
├── SearchComponent
├── BookListComponent
│     ├── BookCardComponent
│     ├── BookCardComponent
│     └── BookCardComponent
├── ShoppingCartComponent
└── FooterComponent
```

Now try a different application, such as a **Food Delivery App** or a **Student Management System**, and sketch its component tree on paper. Don't worry about being perfect—the goal is to start thinking in components.

***

# Quick Review

Without looking back:

1. What is a parent component?
2. What is a child component?
3. Can a component be both a parent and a child?
4. Why do Angular applications use many small components instead of one large one?
5. What is a component tree?

***

# Lesson Summary

Today you learned:

* ✅ What parent and child components are.
* ✅ How Angular applications are organized into a component tree.
* ✅ Why breaking the UI into components is important.
* ✅ That parent and child describe relationships, not permanent roles.
* ✅ How this prepares you for component communication.

***

# Roadmap Progress

```
Module 5 — Component Communication

✅ Lesson 5.1 Parent and Child Components
⬜ Lesson 5.2 @Input
⬜ Lesson 5.3 @Output
⬜ Lesson 5.4 EventEmitter
```

***

# 🎯 Mental Model

Think of an Angular application like a company.

* The **CEO** doesn't do every job.
* There are managers.
* Managers have teams.
* Teams have individual employees.

The company is organized as a hierarchy.

Angular is similar:

```
AppComponent
    ↓
DashboardComponent
    ↓
TenantListComponent
    ↓
TenantCardComponent
```

Each component has a specific responsibility and works together to build the complete application.

***

## 📌 Looking Ahead

In **Lesson 5.2 — `@Input()`**, we'll make this hierarchy come alive.

For the first time, you'll see a parent component **pass real data** to a child component, such as a tenant's name, rent amount, or payment status. That lesson is where component communication truly begins.
