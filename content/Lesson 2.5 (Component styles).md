Excellent.

We're about to complete the **three pillars of every Angular component**.

So far you've learned:

* **TypeScript** → What the component does.
* **HTML** → What the user sees.

Now we'll learn:

* **CSS** → How it looks.

This lesson is much more important than just "adding colors." It introduces one of Angular's most useful features: **style encapsulation**. This is a feature that many beginners don't even realize Angular is providing.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.5 — Component Styles

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ✅ Lesson 2.4 — Component Template
  * 🟨 Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you'll understand:

* What component styles are.
* How Angular connects CSS to a component.
* Why Angular separates CSS into its own file.
* What style encapsulation is.
* The difference between component CSS and global CSS.

***

# First Question

Open your project.

Look at these three files:

```text
app.ts
app.html
app.css
```

We already know:

* `app.ts` → Logic
* `app.html` → UI

So...

> **Why doesn't Angular put the CSS inside `styles.css` for every component?**

That's the question we'll answer today.

***

# The Third Piece of a Component

A component has three parts:

```text
Component

├── TypeScript
│      Logic
│
├── HTML
│      Structure
│
└── CSS
       Appearance
```

Without CSS:

```html
<h1>Welcome</h1>
```

works.

But it isn't very attractive.

CSS controls things like:

* colors
* spacing
* fonts
* layout
* borders
* animations

***

# How Angular Connects the CSS

Open:

```typescript
@Component({
    selector: 'app-root',
    templateUrl: './app.html',
    styleUrl: './app.css'
})
```

Notice:

```typescript
styleUrl: './app.css'
```

Angular reads this and says:

> "These styles belong to this component."

***

# What Happens Internally?

Suppose your component looks like this:

```text
app.ts
```

```typescript
@Component({
    templateUrl: './app.html',
    styleUrl: './app.css'
})
```

Angular performs this process:

```text
Reads app.ts

↓

Finds app.html

↓

Finds app.css

↓

Compiles everything

↓

Creates one component
```

So your component isn't just the TypeScript class.

Angular combines:

* TypeScript
* HTML
* CSS

into one working unit.

***

# Try It Yourself

Replace the contents of `app.html` with:

```html
<h1>Angular Course</h1>

<p>Learning Components</p>
```

Now open:

```text
app.css
```

Add:

```css
h1 {
    color: blue;
}

p {
    font-size: 20px;
}
```

Save.

Your browser updates automatically.

Notice:

You only edited CSS.

You didn't touch:

* HTML
* TypeScript

This separation is one of Angular's strengths.

***

# Why Separate CSS?

Imagine a project with:

50 components.

If every CSS rule lived in one file:

```css
.header {}

.footer {}

.login {}

.dashboard {}

.profile {}

.products {}

.cart {}

.orders {}
```

After several months, the stylesheet could become difficult to navigate and maintain.

Instead:

```text
Header Component

↓

header.css
```

```text
Login Component

↓

login.css
```

```text
Product Component

↓

product.css
```

Each component manages its own appearance.

***

# Component CSS vs Global CSS

Angular has two places for CSS.

## Component CSS

Example:

```text
app.css
```

These styles belong to one component.

***

## Global CSS

Open:

```text
src/styles.css
```

This file affects the entire application.

Typical uses include:

* resetting browser defaults,
* defining application-wide fonts,
* setting common colors,
* utility classes.

Think of it as the stylesheet for the whole application.

***

# The Biggest Angular Feature Here

Now we reach something special.

## Style Encapsulation

Suppose you have:

### Header Component

```css
h1 {
    color: blue;
}
```

***

### Footer Component

```css
h1 {
    color: green;
}
```

Normally, in plain HTML/CSS, these rules could conflict because both target `h1`.

Angular prevents this by **encapsulating** component styles by default.

This means:

* the Header's styles affect the Header,
* the Footer's styles affect the Footer.

Each component gets its own styling "scope."

***

# How Does Angular Do This?

You don't need to memorize the implementation, but it's useful to understand the idea.

When Angular builds your application, it transforms the HTML and CSS behind the scenes.

You might write:

```html
<h1>Header</h1>
```

Angular internally generates something conceptually like:

```html
<h1 _ngcontent-abc123>
```

and updates the CSS to match that generated attribute.

The result is that styles from one component don't accidentally apply to another.

> The exact attribute names are generated automatically and may look different in your browser's Developer Tools. You should never write them yourself.

***

# Why Is This Useful?

Imagine building:

```text
Dashboard

├── Header

├── Menu

├── Sidebar

├── Reports

├── Settings

├── Footer
```

Each team can style their component independently.

Nobody accidentally changes someone else's design.

This becomes especially valuable in large applications.

***

# Inline Styles

Just like templates can be inline...

Styles can be too.

Example:

```typescript
@Component({
    styles: [`
        h1 {
            color: blue;
        }
    `]
})
```

Instead of:

```typescript
styleUrl: './app.css'
```

Again...

For real projects,

**external CSS files are the preferred approach.**

***

# Modern Angular Note

Your project uses:

```typescript
styleUrl: './app.css'
```

Older tutorials often show:

```typescript
styleUrls: ['./app.component.css']
```

Notice:

Modern Angular:

```typescript
styleUrl
```

Older Angular:

```typescript
styleUrls
```

Both serve the same purpose—linking a component to its stylesheet.

***

# Mental Model

Every component is now complete.

```text
Component

│

├── Logic
│      app.ts
│
├── UI
│      app.html
│
└── Appearance
       app.css
```

Angular combines all three.

***

# Common Beginner Misconceptions

### ❌ "All CSS should go into `styles.css`."

No.

Most component-specific styles belong in the component's own stylesheet.

Use `styles.css` for application-wide styles.

***

### ❌ "Component CSS affects the whole application."

By default, Angular scopes component styles so they apply only to that component.

***

### ❌ "Inline CSS is more professional."

Not usually.

External CSS files are cleaner and easier to maintain.

***

### ❌ "Style encapsulation means components can never share styles."

Not quite.

Global styles, shared style files, and CSS frameworks can still provide consistent styling across components.

Encapsulation simply prevents accidental leakage of component-specific styles.

***

# Hands-on Exercise

1. Open:

```text
app.html
```

Replace it with:

```html
<h1>Angular Components</h1>

<p>This paragraph belongs to my first component.</p>

<button>Click Me</button>
```

***

2. Open:

```text
app.css
```

Experiment with:

```css
h1 {
    color: darkblue;
}

p {
    font-size: 20px;
}

button {
    background: royalblue;
    color: white;
    padding: 10px;
    border: none;
    border-radius: 6px;
}
```

3. Save.

4. Observe how only this component changes.

***

# Quick Review

Answer these without looking back:

1. What is the purpose of `styleUrl`?
2. What is the difference between component CSS and global CSS?
3. Why does Angular separate CSS into component files?
4. What is style encapsulation?
5. Why is style encapsulation useful in large applications?

***

# Lesson Summary

Today you learned:

* ✅ How Angular connects CSS to a component.
* ✅ The difference between component and global styles.
* ✅ Why Angular separates styling into individual files.
* ✅ What style encapsulation is.
* ✅ How Angular keeps component styles isolated by default.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ✅ Lesson 2.4 — Component Template
  * ✅ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

## Before we move to Lesson 2.6

We're at an interesting point.

So far, we've studied the **component that Angular created for us** (`App`). In the next lesson, we'll stop examining the starter project and begin creating **our own components** using the Angular CLI.

This is where you'll see why the CLI is so valuable. Instead of manually creating a TypeScript file, an HTML file, a CSS file, updating imports, and wiring everything together, you'll generate a complete, ready-to-use component with a single command—and then we'll inspect every file it creates so you understand exactly what the CLI did for you.
