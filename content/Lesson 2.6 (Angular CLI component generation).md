Perfect. This lesson is one of the most practical in Module 2 because you'll start **building** instead of just reading code.

After this lesson, you should never create Angular components manually unless you have a very specific reason. In professional Angular development, the **Angular CLI** is the standard way to generate components.

***

# Angular Master Course

# Module 2 — Components

## Lesson 2.6 — Angular CLI Component Generation

### Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ✅ Lesson 2.4 — Component Template
  * ✅ Lesson 2.5 — Component Styles
  * 🟨 Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# Lesson Objective

By the end of this lesson, you will understand:

* Why Angular CLI generates components instead of creating them manually.
* How to generate a component.
* What files Angular CLI creates.
* How Angular updates your project automatically.
* How to use your new component.

***

# Why Not Create Components Manually?

Imagine you want to create a component called **Header**.

Without the Angular CLI, you'd need to:

1. Create a TypeScript file.
2. Create an HTML file.
3. Create a CSS file.
4. Add the `@Component` decorator.
5. Write the selector.
6. Connect the template.
7. Connect the stylesheet.
8. Export the class.
9. Import the component into another component.

That's a lot of repetitive work.

Instead, Angular CLI does all of it for you.

***

# The Angular CLI Command

Open your terminal inside your Angular project.

Run:

```bash
ng generate component header
```

or the shorter version:

```bash
ng g c header
```

Both commands do exactly the same thing.

Most Angular developers use the shorter version.

***

# What Happens?

The CLI prints something similar to:

```text
CREATE src/app/header/header.ts
CREATE src/app/header/header.html
CREATE src/app/header/header.css
```

Depending on your Angular version and project configuration, you may also see updates to existing files.

***

# Open the `src/app` Folder

Before:

```text
src/app

app.ts
app.html
app.css
app.config.ts
app.routes.ts
```

After running the command:

```text
src/app

app.ts
app.html
app.css

header/
    header.ts
    header.html
    header.css

app.config.ts
app.routes.ts
```

Notice that Angular created a dedicated folder for the new component.

This organization keeps larger projects manageable.

***

# Let's Examine the Generated Component

Open:

```text
src/app/header/header.ts
```

You'll see something similar to:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  imports: [],
  templateUrl: './header.html',
  styleUrl: './header.css'
})
export class Header {

}
```

Does this look familiar?

It should!

It's the same structure we studied in Lessons 2.2 through 2.5.

The CLI simply generated it for you.

***

# The HTML File

Open:

```text
header.html
```

You'll usually see a very small starter template or it may even be empty, depending on the Angular CLI version.

Replace its contents with:

```html
<h2>My Header Component</h2>

<p>This component was generated using Angular CLI.</p>
```

***

# The CSS File

Open:

```text
header.css
```

Add:

```css
h2 {
    color: darkgreen;
}
```

***

# The TypeScript File

Right now, it doesn't do much.

```typescript
export class Header {

}
```

That's okay.

We'll begin adding logic in later modules.

***

# But Wait...

You generated a component.

Why don't you see it in the browser?

Because Angular created it...

**But nothing is using it yet.**

Remember Lesson 2.3?

A component appears only when another template uses its selector.

***

# Using the Component

Look at the selector:

```typescript
selector: 'app-header'
```

To display it, open:

```text
src/app/app.html
```

Add:

```html
<app-header></app-header>
```

Save.

If everything is configured correctly, your new component should appear.

***

# How Does Angular Know About It?

This is where modern Angular differs from older Angular.

Your generated component is a **standalone component**.

To use one standalone component inside another, you must import it.

Open:

```text
app.ts
```

Add the import:

```typescript
import { Header } from './header/header';
```

Then update the `imports` array:

```typescript
@Component({
  selector: 'app-root',
  imports: [Header],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
```

Now Angular knows that the `App` component is allowed to use `<app-header>` in its template.

> **Important:** In older Angular tutorials, components were typically declared inside an `NgModule`. In modern standalone Angular, you import components directly into the component that uses them.

***

# The Component Tree Is Growing

Before:

```text
App
```

After:

```text
App

│

└── Header
```

As your application grows:

```text
App

├── Header

├── Sidebar

├── Dashboard

├── Footer
```

Eventually, you'll have dozens of small, reusable components.

***

# Useful CLI Options

Here are a few options you'll encounter later.

### Generate inside a folder

```bash
ng g c components/navbar
```

Result:

```text
src/app/components/navbar/
```

***

### Skip the CSS file

```bash
ng g c header --skip-css
```

Useful for projects using another styling approach.

***

### Create an inline template

```bash
ng g c header --inline-template
```

Instead of generating `header.html`, Angular places the template directly inside the TypeScript file.

***

### Create inline styles

```bash
ng g c header --inline-style
```

Instead of generating `header.css`, Angular places the styles directly in the component decorator.

***

# Why Use the CLI?

Imagine creating 100 components.

Manually:

```text
Create file

Write decorator

Write selector

Create HTML

Create CSS

Import files

Repeat...
```

With the CLI:

```bash
ng g c product-card
```

Done.

This saves time and reduces mistakes.

***

# Common Beginner Misconceptions

### ❌ "Generating a component automatically displays it."

No.

You still need to use its selector in another template and import the standalone component where it's used.

***

### ❌ "I should manually create component files."

You can, but Angular CLI is the recommended and standard approach.

***

### ❌ "The generated component already contains business logic."

No.

The CLI generates the structure.

You add the functionality.

***

### ❌ "The `imports` array is optional."

For standalone components, it isn't.

If `App` uses `<app-header>`, then `Header` must appear in the `imports` array of `App`.

***

# Hands-on Exercise

Let's build your first custom component.

### Step 1

Generate it:

```bash
ng g c header
```

***

### Step 2

Open:

```text
header.html
```

Replace it with:

```html
<h2>Welcome!</h2>

<p>This is my first custom component.</p>
```

***

### Step 3

Open:

```text
header.css
```

Add:

```css
h2 {
    color: purple;
}
```

***

### Step 4

Open:

```text
app.ts
```

Import the component:

```typescript
import { Header } from './header/header';
```

Update:

```typescript
imports: [Header]
```

***

### Step 5

Open:

```text
app.html
```

Add:

```html
<app-header></app-header>
```

***

### Step 6

Save everything.

You should now see your custom component rendered in the browser.

***

# Quick Review

Answer these without looking back:

1. Why is Angular CLI preferred for creating components?
2. What command generates a component?
3. What files are created?
4. Why doesn't a newly generated component appear automatically?
5. What must you do before using a standalone component in another component's template?

***

# Lesson Summary

Today you learned:

* ✅ How to generate components with Angular CLI.
* ✅ What files Angular CLI creates.
* ✅ How standalone components are imported.
* ✅ How to display a generated component.
* ✅ Why Angular CLI is the standard tool for creating components.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* 🟩 Module 2 — Components

  * ✅ Lesson 2.1 — What is a Component?
  * ✅ Lesson 2.2 — Component Metadata
  * ✅ Lesson 2.3 — Component Selector
  * ✅ Lesson 2.4 — Component Template
  * ✅ Lesson 2.5 — Component Styles
  * ✅ Lesson 2.6 — Angular CLI Component Generation
  * ⬜ Lesson 2.7 — Component Lifecycle (`ngOnInit`)

***

# 📌 A Note About Hallucinations and Accuracy

Since you mentioned at the beginning of this course that you wanted a **strict syllabus** to keep us on track, here's an important note.

Everything in today's lesson is based on the **current standalone Angular architecture** (Angular 17+ and later), not the older `NgModule` approach that many tutorials still teach. I'll continue following this modern approach consistently unless I explicitly say, "This is how older Angular worked."

That way, if you ever need to reset me by pasting the roadmap and saying, "We're at Lesson 2.6," I can resume from the correct place without drifting into outdated Angular patterns.
