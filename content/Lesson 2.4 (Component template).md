Excellent. This lesson is where you'll finally understand **what a template really is**.

Most beginners think:

> "A template is just an HTML file."

That's only **partially** true.

A template is **much more powerful than normal HTML**, and understanding this difference is one of the keys to learning Angular.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.4 — Component Template

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * 🟨 Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you will understand:

* What a template is.
* How a template differs from ordinary HTML.
* How a template connects to a component.
* What Angular does with templates.
* The difference between **external** and **inline** templates.

***

# First Question

Open your project.

Open:

```text
src/app/app.html
```

You are looking at your component's template.

Now ask yourself:

> **Why isn't the HTML written inside the TypeScript class?**

Why do we have two separate files?

***

# Separation of Responsibilities

Angular keeps different responsibilities in different places.

| File       | Responsibility |
| ---------- | -------------- |
| `app.ts`   | Logic          |
| `app.html` | User Interface |
| `app.css`  | Styling        |

Think of it like building a house.

* The **architect** designs the layout.
* The **electrician** installs wiring.
* The **painter** paints the walls.

Each has a different job.

Angular follows the same idea.

***

# What Is a Template?

A **template** is the HTML that defines what the user sees for a component.

For example:

```html
<h1>Hello Angular</h1>

<p>Welcome!</p>
```

This is a template.

But here's the important part:

Angular **doesn't treat it as ordinary HTML**.

Angular first **reads** the template.

Then it **processes** Angular-specific syntax.

Then it creates the final HTML shown in the browser.

***

# Ordinary HTML vs Angular Template

Imagine writing this in a normal HTML file:

```html
<h1>{{ title }}</h1>
```

A browser would literally display:

```text
{{ title }}
```

because HTML doesn't understand those curly braces.

Angular does.

Angular sees:

```html
<h1>{{ title }}</h1>
```

and says:

> "I need to replace `title` with the value from the component."

This feature is called **interpolation**, and we'll study it in Module 3.

For now, the important idea is:

> A template is **HTML plus Angular features**.

***

# How Does Angular Connect the Template?

Remember the metadata?

```typescript
@Component({
    templateUrl: './app.html'
})
```

This line tells Angular:

> "The user interface for this component is in `app.html`."

When Angular creates the component:

1. It creates the class.
2. It loads the HTML template.
3. It combines them.
4. It displays the result.

You can visualize it like this:

```text
Component Class
       │
       │
templateUrl
       │
       ▼
app.html
       │
       ▼
Rendered UI
```

***

# The Template Is Not Static

Suppose your component contains:

```typescript
export class App {
    title = "Angular Course";
}
```

and your template contains:

```html
<h1>{{ title }}</h1>
```

Angular combines them.

The browser eventually receives something equivalent to:

```html
<h1>Angular Course</h1>
```

Notice something:

The HTML changed **without you editing the HTML file**.

That's because Angular generated the final output.

***

# External Templates

This is what you're currently using.

```typescript
@Component({
    templateUrl: './app.html'
})
```

The HTML lives in its own file.

Advantages:

* Easier to read.
* Better organization.
* Large templates stay manageable.
* Most common approach in real projects.

This is the recommended style for almost all applications.

***

# Inline Templates

Angular also allows the HTML to be written directly inside the decorator.

Example:

```typescript
@Component({
    template: `
        <h1>Hello Angular</h1>
        <p>Welcome!</p>
    `
})
```

Instead of:

```typescript
templateUrl: './app.html'
```

we use:

```typescript
template: `...`
```

***

# Which One Should You Use?

For small examples:

Inline templates are acceptable.

For real applications:

Use external templates.

Imagine writing 500 lines of HTML inside a TypeScript file.

It quickly becomes difficult to read and maintain.

That's why Angular CLI creates separate HTML files by default.

***

# What Happens Internally?

Suppose you have:

```typescript
@Component({
    templateUrl: './app.html'
})
```

Angular performs these steps:

```text
Reads app.ts

↓

Finds templateUrl

↓

Opens app.html

↓

Compiles the template

↓

Links it to the component

↓

Displays it
```

This process happens automatically.

***

# A Real-World Analogy

Think of a restaurant.

The **chef** prepares the food.

The **waiter** serves it.

The **menu** describes it.

In Angular:

* The **component class** is the chef (it prepares the data).
* The **template** is the waiter (it presents the data to the user).
* The **user** only sees the final result.

The waiter doesn't cook.

The chef doesn't serve.

Each has a clear responsibility.

***

# Modern Angular Note

Open your `app.html`.

You'll probably notice it's quite large and contains Angular's default welcome page.

For learning purposes, you can replace it with something much simpler.

For example:

```html
<h1>Welcome to Angular!</h1>

<p>This is my first Angular application.</p>
```

Save the file.

If `ng serve` is running, the browser updates automatically.

Congratulations—you've just edited your first Angular template.

***

# Common Beginner Misconceptions

### ❌ "A template is just HTML."

Not quite.

It's HTML **plus Angular template syntax**.

***

### ❌ "The template stores data."

It doesn't.

The component class stores the data.

The template displays it.

***

### ❌ "The browser understands Angular syntax."

It doesn't.

Angular processes the template before the browser displays the final HTML.

***

### ❌ "Inline templates are better because everything is in one file."

Not for most real projects.

External templates are easier to maintain and are the standard approach in larger applications.

***

# Hands-on Exercise

Let's make a visible change.

1. Open:

```text
src/app/app.html
```

2. Replace the default content with:

```html
<h1>Welcome to Angular!</h1>

<p>I built this application.</p>
```

3. Save the file.

4. Observe the browser update automatically.

5. Now change the text again.

6. Save once more.

Notice how Angular rebuilds the application and refreshes the view.

***

# Quick Review

Try answering these without looking back:

1. What is a template?
2. How is an Angular template different from ordinary HTML?
3. What does `templateUrl` do?
4. What is the difference between an external template and an inline template?
5. Does the component class or the template store the data?

***

# Lesson Summary

Today you learned:

* ✅ What a template is.
* ✅ Why Angular separates logic from the UI.
* ✅ How `templateUrl` connects a component to its HTML.
* ✅ The difference between external and inline templates.
* ✅ That Angular processes templates before displaying them.
* ✅ That templates display data—they don't own it.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ✅ Lesson 2.4 — Component Template
  * ⬜ Lesson 2.5 — Component Styles
  * ⬜ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

## Before we move on, one important clarification

Earlier, I intentionally avoided explaining **`{{ title }}`** in detail.

You saw it several times in this lesson, but I only described it as "Angular syntax."

That was deliberate.

According to our roadmap, **data binding belongs in Module 3**, not Module 2. So I wanted you to recognize that templates can contain Angular expressions without diving into how they work just yet.

In the next lesson (**2.5 – Component Styles**), we'll complete the three fundamental pieces of every component:

* **TypeScript** → the logic
* **HTML Template** → the view
* **CSS Styles** → the appearance

Once those three pieces are clear, you'll have a complete mental model of what an Angular component is before we start generating our own components with the Angular CLI.
