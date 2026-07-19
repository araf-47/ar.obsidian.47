Excellent. This is the lesson where Angular starts to feel a little "magical." After today, you'll understand **how Angular knows where to place a component on the page**.

This topic confuses many beginners because they see tags like `<app-root>` and assume they're built into HTML. They aren't.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.3 — Component Selector

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * 🟨 Lesson 2.3 — Component Selector
  * ⬜ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you will understand:

* What a selector is.
* Why Angular needs selectors.
* How Angular finds a component.
* Where the selector is used.
* Why `<app-root>` is not an HTML tag.
* How Angular renders a component.

***

# Let's Start with a Mystery

Open your browser and inspect your Angular application.

You'll see something like this:

```html
<body>
  <app-root></app-root>
</body>
```

or, after Angular has rendered the page:

```html
<body>
  <app-root>
      ... lots of HTML ...
  </app-root>
</body>
```

Now ask yourself:

> **Where did `<app-root>` come from?**

Did HTML invent it?

No.

Did JavaScript invent it?

No.

It came from Angular.

***

# What Is a Selector?

A selector is simply the **HTML tag name** that Angular uses to represent a component.

For example:

```typescript
@Component({
    selector: 'app-root'
})
```

This tells Angular:

> "Whenever you find `<app-root>`, display this component there."

Think of the selector as the **address** of the component.

***

# Think of a Mailing Address

Imagine someone wants to deliver a package.

Without an address:

📦 ❌ Delivery impossible.

With an address:

```text
House 25
Road 7
City
```

The delivery person knows exactly where to go.

A selector works the same way.

Without a selector:

Angular wouldn't know where to place the component.

***

# Where Is the Selector Used?

Remember your component?

```typescript
@Component({
    selector: 'app-root'
})
export class App {

}
```

Now let's look at another important file.

Open:

```text
src/index.html
```

You'll see something like:

```html
<body>
  <app-root></app-root>
</body>
```

Notice something?

The selector appears here.

This is **not** a coincidence.

Angular starts by reading `index.html`, finds `<app-root>`, and says:

> "I know which component belongs here."

***

# The Rendering Process

Let's visualize what happens.

### Step 1

Angular reads:

```html
<app-root></app-root>
```

***

### Step 2

It searches for a component whose selector is:

```text
app-root
```

***

### Step 3

It finds:

```typescript
@Component({
    selector: 'app-root'
})
```

***

### Step 4

Angular creates an instance of that component.

***

### Step 5

It loads:

* the component class,
* its template,
* its styles.

***

### Step 6

The browser displays the result.

The complete process looks like this:

```text
index.html

↓

<app-root>

↓

Angular searches

↓

selector: app-root

↓

Creates App Component

↓

Loads HTML

↓

Loads CSS

↓

Shows UI
```

This is the first step in building the entire component tree.

***

# Can We Create Our Own Selectors?

Absolutely.

Suppose you build a navigation component.

```typescript
@Component({
    selector: 'app-navbar'
})
```

Angular now recognizes:

```html
<app-navbar></app-navbar>
```

Likewise, a footer component:

```typescript
@Component({
    selector: 'app-footer'
})
```

can be used as:

```html
<app-footer></app-footer>
```

Over time, your application becomes a collection of custom HTML elements.

***

# Why Use the Prefix `app-`?

You might wonder:

> Why not just call it `navbar`?

Technically, you could choose another unique prefix, but Angular projects use prefixes to avoid conflicts with existing or future HTML elements.

By default, Angular CLI generates components with the `app-` prefix.

For example:

```html
<app-header>

<app-sidebar>

<app-product>

<app-footer>
```

Many companies customize this prefix:

```html
<amazon-header>

<google-menu>

<company-dashboard>
```

The important point is consistency and uniqueness.

***

# Components Inside Components

Imagine you have this structure:

```text
App Component

│

├── Header

├── Sidebar

├── Dashboard

└── Footer
```

The template of the root component might look like:

```html
<app-header></app-header>

<app-sidebar></app-sidebar>

<app-dashboard></app-dashboard>

<app-footer></app-footer>
```

Each of those tags corresponds to another Angular component.

Angular replaces each custom tag with the appropriate rendered component.

This is how large applications are built from small pieces.

***

# HTML vs Angular Elements

A common point of confusion:

HTML provides elements like:

```html
<div>

<p>

<button>

<img>
```

Angular lets **you create your own elements**.

For example:

```html
<app-login>

<app-cart>

<app-user-profile>

<app-order-history>
```

These are not built into the browser.

Angular understands them because you've defined components with matching selectors.

***

# What Happens If the Selector Doesn't Exist?

Imagine `index.html` contains:

```html
<app-home></app-home>
```

but no component has:

```typescript
selector: 'app-home'
```

Angular won't know what to render there.

The application will either fail to compile or report an error because the element isn't associated with a known component.

***

# Mental Model

Think of a selector as the connection between HTML and a component.

```text
HTML Tag

↓

Selector

↓

Angular Component

↓

Template

↓

Browser
```

Or even more simply:

```text
Selector

=

Component's HTML Name
```

***

# Common Beginner Misconceptions

### ❌ "`<app-root>` is an HTML tag."

No.

It's a custom element defined by your Angular component.

***

### ❌ "The selector creates the component."

No.

The selector identifies where the component should be used.

Angular creates the component when it encounters that selector during rendering.

***

### ❌ "Selectors must start with `app-`."

No.

That's just the default prefix created by Angular CLI.

You can configure a different prefix when creating a project.

***

### ❌ "Selectors only appear in `index.html`."

Only the **root component's** selector appears in `index.html`.

Other component selectors are usually used inside the templates of other components.

For example:

```text
index.html
    │
    ▼
<app-root>
    │
    ▼
app.html
    │
    ├── <app-header>
    ├── <app-sidebar>
    └── <app-footer>
```

***

# Hands-on Exercise

Let's make a tiny change so you can see the selector in action.

1. Open `src/index.html`.
2. Find:

```html
<app-root></app-root>
```

3. Don't change it—just observe that it matches:

```typescript
selector: 'app-root'
```

4. Now open `src/app/app.html` and notice that this is the content Angular places inside `<app-root>`.

The goal is to connect these three pieces:

* `index.html`
* `selector: 'app-root'`
* `app.html`

***

# Quick Review

Try answering these without looking back:

1. What is a selector?
2. Why does Angular need selectors?
3. Where is the root component's selector used?
4. Is `<app-root>` a standard HTML tag?
5. What happens when Angular finds a matching selector?

***

# Lesson Summary

Today you learned:

* ✅ What a selector is.
* ✅ How Angular finds components.
* ✅ Why `<app-root>` exists.
* ✅ How Angular connects HTML to components.
* ✅ That components are represented by custom HTML elements.
* ✅ How selectors help build a component tree.

***

## Roadmap Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ⬜ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

## One small correction to keep us aligned with modern Angular

In the previous lesson, we looked at the `@Component` decorator. Now you've seen how the `selector` property fits into the startup process.

The complete startup flow is now:

```text
Browser
    │
    ▼
index.html
    │
    ▼
<app-root>
    │
    ▼
Angular looks for:
selector: 'app-root'
    │
    ▼
Creates the root component
    │
    ▼
Loads app.html
    │
    ▼
Displays your application
```

This mental model is worth remembering because we'll keep expanding it as we add more components in the next lessons. Understanding this flow will make topics like routing and component communication much easier later.
