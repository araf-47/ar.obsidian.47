Excellent. We've now reached one of the most important lessons in the entire course.

Many beginners think this lesson is just "how to run Angular." It isn't.

This lesson explains **what actually happens when you type `ng serve`**, which is the foundation for understanding Angular's development workflow.

***

# Angular Master Course

# Module 1 — Angular Introduction

## Lesson 1.4 — Running & Building an Angular Application

### Progress

* 🟩 Module 1 — Angular Introduction

  * ✅ Lesson 1.1 — What is Angular?
  * ✅ Lesson 1.2 — Installing Node.js, Angular CLI & Creating Your First Project
  * ✅ Lesson 1.3 — Angular Project Structure
  * 🟨 Lesson 1.4 — Running & Building an Angular Application

***

# Lesson Objective

By the end of this lesson, you'll understand:

* What `ng serve` actually does.
* What a development server is.
* What "build" means.
* The difference between development and production builds.
* What Angular compiles.
* What happens when you save a file.
* The purpose of the `dist/` folder.

***

# Before We Begin...

Let's answer a question.

You previously ran:

```bash
ng serve
```

and Angular printed something like:

```text
✔ Building...
Application bundle generation complete.

Local: http://localhost:4200
```

Most beginners think:

> "Okay... Angular is running."

But **what is actually running?**

Let's find out.

***

# The Journey of an Angular Application

Imagine you wrote:

```typescript
// app.ts

export class App {
    title = "Hello Angular";
}
```

Can Chrome run this file directly?

**No.**

Why?

Because browsers understand **JavaScript**, not **TypeScript**.

Angular projects contain:

* TypeScript
* HTML templates
* CSS
* Angular-specific syntax

Browsers only execute:

* HTML
* CSS
* JavaScript

So Angular must convert your project into something the browser understands.

That conversion is called a **build**.

***

# What Does "Build" Mean?

**Build** means:

> Transform your source code into files that a browser can execute.

Think of it like translating a book.

```text
TypeScript
        │
        ▼
Angular Compiler
        │
        ▼
JavaScript
```

Your browser never sees your original TypeScript files.

It receives compiled JavaScript.

***

# What Happens When You Run `ng serve`?

Let's break it down step by step.

```text
You
 │
 │ ng serve
 ▼
Angular CLI
 │
 ▼
Reads angular.json
 │
 ▼
Reads package.json
 │
 ▼
Compiles TypeScript
 │
 ▼
Processes HTML templates
 │
 ▼
Processes CSS
 │
 ▼
Bundles everything
 │
 ▼
Starts Development Server
 │
 ▼
Browser opens localhost:4200
```

Notice that several tasks happen before you ever see the page.

***

# What Is a Development Server?

When you run:

```bash
ng serve
```

Angular starts a **local web server**.

It serves your application from your own computer.

That's why the address is:

```text
http://localhost:4200
```

Let's decode that.

### `localhost`

Means:

> "This computer."

Instead of requesting a website from the internet, your browser requests it from your own machine.

***

### `4200`

This is the **port number**.

Think of a computer like a large office building.

* The IP address is the building.
* A port is an office inside the building.

Angular's development server listens on **port 4200** by default.

So your browser is saying:

> "Connect to the Angular server running on my own computer, office number 4200."

***

# Why Not Just Open `index.html`?

A common beginner question is:

> "Why can't I just double-click `index.html`?"

Because Angular is much more than static HTML.

It needs to:

* compile TypeScript,
* bundle modules,
* resolve imports,
* handle routing,
* process templates.

A plain HTML file can't do those things on its own.

The development server performs this work for you.

***

# What Is Bundling?

Your project might contain many files.

For example:

```text
app.ts
product.ts
user.ts
login.ts
dashboard.ts
```

Instead of sending hundreds of separate files to the browser, Angular combines and optimizes them into bundles.

```text
Many source files
        │
        ▼
Bundling
        │
        ▼
Optimized JavaScript bundles
```

This improves loading performance.

***

# What Happens When You Save a File?

Suppose you change:

```typescript
title = "Angular Course";
```

and press **Ctrl + S**.

Did you notice the browser updates almost immediately?

That's because `ng serve` watches your files.

The sequence looks like this:

```text
Save File
      │
      ▼
Angular detects the change
      │
      ▼
Rebuilds only what changed
      │
      ▼
Browser refreshes automatically
```

This is often called **live reload**. Modern Angular development tools may also preserve more application state than a full page refresh in some cases, but the key idea is that you see changes almost instantly.

***

# Development Build vs Production Build

This is one of the most important concepts.

## Development

Command:

```bash
ng serve
```

Purpose:

* Easy debugging.
* Fast rebuilds.
* Helpful error messages.
* Source maps.

Think of it as your workshop while you're building the application.

***

## Production

Command:

```bash
ng build
```

or

```bash
ng build --configuration production
```

Purpose:

* Optimized performance.
* Smaller bundle sizes.
* Faster loading.
* Minified code.
* Suitable for deployment.

Think of it as the finished product you deliver to users.

***

# What Is the `dist/` Folder?

When you build for production:

```bash
ng build
```

Angular creates a folder named:

```text
dist/
```

This folder contains the files you'll deploy to a web server.

Example:

```text
dist/
    index.html
    main.js
    styles.css
    assets/
```

Notice something?

No TypeScript.

Only browser-ready files.

Your web server (such as Apache, Nginx, or another hosting platform) serves the contents of this folder—not your source code.

***

# Development vs Production

| Development       | Production           |
| -------------- | -------------------- |
| `ng serve`        | `ng build`           |
| For developers    | For users            |
| Fast rebuilds     | Optimized output     |
| Easy debugging    | Better performance   |
| Runs on localhost | Deployed to a server |

***

# Common Beginner Mistakes

### ❌ Closing the terminal

If you stop the terminal running `ng serve`, the development server stops too.

Your browser will no longer be able to load the application.

***

### ❌ Editing files inside `dist/`

Never edit them manually.

They are generated automatically.

Make changes in `src/` and rebuild.

***

### ❌ Thinking `ng serve` is deployment

It isn't.

`ng serve` is only for local development.

Real users won't access your application through your development server.

***

### ❌ Assuming browsers understand TypeScript

They don't.

The build process converts TypeScript into JavaScript before it reaches the browser.

***

# Mental Model

Whenever you type:

```bash
ng serve
```

Imagine this pipeline:

```text
Your Code
     │
     ▼
Angular CLI
     │
     ▼
Build
     │
     ▼
Development Server
     │
     ▼
Browser
```

Whenever you type:

```bash
ng build
```

Imagine:

```text
Your Code
     │
     ▼
Angular Build Process
     │
     ▼
dist/
     │
     ▼
Deploy to Web Server
```

***

# Hands-on Exercise

Inside your project:

1. Start the development server:

   ```bash
   ng serve
   ```

2. Open the application in your browser.

3. Stop the server with:

   ```text
   Ctrl + C
   ```

4. Start it again.

5. Run:

   ```bash
   ng build
   ```

6. Find the `dist/` folder that was created.

7. Compare it with `src/`.

Ask yourself:

* Which one contains TypeScript?
* Which one is ready for deployment?

***

# Lesson Summary

Today you learned:

* ✅ What `ng serve` actually does.
* ✅ What a development server is.
* ✅ Why Angular needs a build process.
* ✅ Why browsers can't run TypeScript directly.
* ✅ The difference between development and production.
* ✅ What `ng build` creates.
* ✅ Why the `dist/` folder exists.

***

# 🎉 Module 1 Complete!

Congratulations—you've completed the introduction module.

### Roadmap Progress

* ✅ Module 1 — Angular Introduction

  * ✅ Lesson 1.1 — What is Angular?
  * ✅ Lesson 1.2 — Installing Node.js, Angular CLI & Creating Your First Project
  * ✅ Lesson 1.3 — Angular Project Structure
  * ✅ Lesson 1.4 — Running & Building an Angular Application

***

## What's Next?

Next, we begin **Module 2 — Components**.

This is where you'll write your first real Angular code and start building the UI.

You'll learn:

* What a component really is.
* Why Angular is built around components.
* How Angular creates and displays them.
* The anatomy of a component.

I consider **Module 2** the point where Angular truly begins. Everything we've done so far has been preparing the environment and building the mental model you'll need from here onward.
