Excellent! This is one of my favorite lessons because **understanding the project structure** will make everything else in Angular much easier. Instead of seeing a bunch of mysterious files, you'll know why each one exists.

***

# Angular Master Course

# Module 1 — Angular Introduction

## Lesson 1.3 — Understanding the Angular Project Structure

### Progress

* 🟩 Module 1 — Angular Introduction

  * ✅ Lesson 1.1 — What is Angular?
  * ✅ Lesson 1.2 — Installing Node.js, Angular CLI & Creating Your First Project
  * 🟨 Lesson 1.3 — Angular Project Structure
  * ⬜ Lesson 1.4 — Running & Building an Angular Application

***

# Lesson Objective

By the end of this lesson, you should be able to:

* Explain the purpose of every important file and folder.
* Know which files you'll edit frequently.
* Know which files you should rarely touch.
* Understand how Angular starts your application.

***

# First, Let's Look at the Project

After creating your project, you'll see something similar to this:

```text
hello-angular/
│
├── .angular/
├── .vscode/
├── node_modules/
│
├── public/
├── src/
│
├── .editorconfig
├── .gitignore
├── angular.json
├── package.json
├── package-lock.json
├── README.md
├── tsconfig.json
└── ...
```

Don't panic.

You will **not** work with all of these every day.

In fact, most Angular developers regularly use only a handful of them.

***

# Think of It Like a House

Imagine your Angular project is a house.

```text
House
│
├── Foundation
├── Electrical Wiring
├── Plumbing
├── Rooms
├── Furniture
└── Decorations
```

You live in the **rooms**.

You don't spend every day modifying the plumbing.

Angular is the same.

Some files are your everyday workspace, while others are configuration that you only touch occasionally.

***

# The Files You'll Use Most

Let's start with the ones you'll interact with constantly.

***

## 1. `src/`

This is the **heart of your application**.

Everything you build will be inside this folder.

Think of it as:

```text
src
=
Your actual Angular application
```

When someone says,

> "Go to your Angular code."

They usually mean:

```text
src/
```

***

## 2. `src/app/`

This is the most important folder in the project.

Almost everything you'll create during this course goes here.

For example:

```text
app/
│
├── app.ts
├── app.html
├── app.css
├── app.routes.ts
└── ...
```

Later you'll add:

```text
app/
│
├── components/
├── services/
├── models/
├── pages/
└── ...
```

This is where your application's logic and UI live.

***

## 3. `public/`

This folder contains **static files** that are served as-is.

Examples:

* images
* icons
* fonts
* downloadable files

For example:

```text
public/
    logo.png
    banner.jpg
    favicon.ico
```

Angular doesn't process these files; it simply makes them available to the browser.

***

# Configuration Files

These files tell Angular **how** to build and run your project.

***

## 4. `package.json`

This is one of the most important files.

Think of it as the **identity card** of your project.

It contains:

* project name
* version
* scripts
* dependencies

Example:

```json
{
  "name": "hello-angular"
}
```

It also lists every package your project needs.

Without this file:

```text
npm install
```

would have no idea what to install.

***

## 5. `package-lock.json`

This is created automatically.

It records the **exact versions** of installed packages.

Imagine:

Today:

```text
Angular 20.0.1
```

Six months later:

```text
Angular 20.2.7
```

If everyone downloaded "the latest" version, projects could behave differently.

`package-lock.json` ensures everyone gets the same dependency versions.

**Rule:** Don't edit this file manually.

***

## 6. `angular.json`

This is Angular's main configuration file.

It tells Angular:

* where your source files are
* how to build the project
* which styles to include
* which assets to copy
* build options
* development settings

You won't modify it often as a beginner, but it's useful to know it exists.

***

## 7. `tsconfig.json`

Remember how we said Angular uses TypeScript?

This file configures the TypeScript compiler.

It specifies things like:

* language features
* compiler options
* strictness
* included files

Again, beginners rarely need to change it.

***

# Development Support Files

***

## `.gitignore`

Since you've already worked with Git, this should look familiar.

It tells Git:

> Ignore these files.

For example:

```text
node_modules/
```

You never want to commit `node_modules` because it can contain thousands of files and can always be recreated with `npm install`.

***

## `.editorconfig`

This helps keep formatting consistent across editors.

For example:

* indentation
* tabs vs spaces
* line endings

Your editor can read this file and apply the project's formatting rules.

***

## `.vscode/`

This folder contains project-specific settings for Visual Studio Code, if you choose to use them.

It isn't required for Angular itself.

***

# The Biggest Folder: `node_modules/`

This folder surprises almost every beginner.

It can contain **tens of thousands of files**.

Why?

Because it stores **every package** your project depends on.

```text
Your Project
       │
       ▼
Angular
       │
       ▼
Depends on many other packages
       │
       ▼
All are stored inside node_modules
```

### Should you edit it?

**Never.**

Think of it like the engine inside a car.

You use it, but you don't rewrite it.

If something goes wrong with `node_modules`, you usually delete it and run:

```bash
npm install
```

to recreate it.

***

# How Angular Starts Your Application

When you run:

```bash
ng serve
```

Angular follows a startup sequence.

A simplified version looks like this:

```text
You type:

ng serve
       │
       ▼
Angular CLI
       │
       ▼
Reads angular.json
       │
       ▼
Compiles TypeScript
       │
       ▼
Starts development server
       │
       ▼
Loads src/main.ts
       │
       ▼
Loads your Angular application
       │
       ▼
Browser displays your app
```

The important point is that **`main.ts` is the entry point** of your application.

We'll look at that file more closely later.

***

# Which Files Will You Use Most?

| File/Folder     | How Often You'll Use It |
| --------------- | ----------------------- |
| `src/app/`      | ⭐⭐⭐⭐⭐ Every day         |
| `public/`       | ⭐⭐⭐ Sometimes           |
| `package.json`  | ⭐⭐⭐ Often               |
| `angular.json`  | ⭐ Rarely                |
| `tsconfig.json` | ⭐ Rarely                |
| `node_modules/` | Never edit              |
| `.gitignore`    | Occasionally            |

***

# Common Beginner Mistakes

### ❌ Editing `node_modules`

Never do this.

Changes will be lost the next time dependencies are installed.

***

### ❌ Deleting `package.json`

Without it, npm doesn't know your project's dependencies.

***

### ❌ Committing `node_modules` to Git

Your repository becomes unnecessarily large.

Instead, commit `package.json` and `package-lock.json`.

***

### ❌ Ignoring `package-lock.json`

Some beginners delete it because they think it's unimportant.

In reality, it helps keep dependency versions consistent across different machines.

***

# One Note About Modern Angular

You may notice your project looks a little different from older tutorials. For example, your `src/app` folder may contain files like:

```text
app.ts
app.html
app.css
app.config.ts
app.routes.ts
```

instead of the older:

```text
app.component.ts
app.component.html
app.component.css
app.module.ts
```

That's because **modern Angular uses standalone components by default**, while many older tutorials use the NgModule-based structure.

We'll learn the modern approach first since that's what the Angular CLI now generates. Later in the course, I'll also explain the older NgModule approach because you'll still encounter it in documentation, interview questions, and legacy projects.

***

# Hands-on Exercise

I want you to explore your project.

1. Open your project in VS Code.
2. Locate each of these:

   * `src`
   * `src/app`
   * `public`
   * `package.json`
   * `angular.json`
   * `tsconfig.json`
   * `node_modules`
3. Open `package.json` and identify:

   * The project name.
   * The `scripts` section.
   * The `dependencies` section.
4. Without editing anything, browse through `src/app` and note the files that Angular created.

***

# Lesson Summary

Today you learned:

* ✅ The purpose of the main Angular project folders.
* ✅ What `package.json` and `package-lock.json` do.
* ✅ Why `node_modules` exists.
* ✅ The role of `angular.json` and `tsconfig.json`.
* ✅ Which files you'll use every day versus those you'll rarely touch.
* ✅ That `main.ts` is the entry point of an Angular application.

***

### Roadmap Progress

* 🟩 Module 1 — Angular Introduction

  * ✅ Lesson 1.1 — What is Angular?
  * ✅ Lesson 1.2 — Installing Node.js, Angular CLI & Creating Your First Project
  * ✅ Lesson 1.3 — Angular Project Structure
  * ⬜ Lesson 1.4 — Running & Building an Angular Application

***

### A note for our course

I want to point out something important because it will affect future lessons.

Your project is using **modern Angular (standalone components)**. Many books, YouTube videos, and even exam questions still use the older **NgModule** style. Rather than pretending one doesn't exist, I'll clearly label when something is **modern Angular** versus **legacy Angular**, explain why the difference exists, and make sure you can understand both. That way you'll be prepared whether you're working on a new project or maintaining an older one.
