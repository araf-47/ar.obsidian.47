Perfect. Since this is the **foundation** of your Angular environment, we're not just going to install things—we're going to understand **why** each tool exists. This will help you troubleshoot problems later instead of memorizing commands.

***

# Angular Master Course

# Module 1 — Angular Introduction

## Lesson 1.2 — Installing Node.js, Angular CLI & Creating Your First Project

### Progress

* 🟩 Module 1 — Angular Introduction

  * ✅ Lesson 1.1 — What is Angular?
  * 🟨 Lesson 1.2 — Installing Node.js, Angular CLI & Creating Your First Project
  * ⬜ Lesson 1.3 — Angular Project Structure
  * ⬜ Lesson 1.4 — Running & Building an Angular Application

***

# Lesson Objective

By the end of this lesson, you will understand:

* Why Angular needs Node.js
* What npm is
* What Angular CLI is
* How to install Angular on Debian 13
* How to install Angular on Windows 11
* How to create your first Angular project
* What happens behind the scenes when you create a project

***

# The Big Picture

Before installing anything, let's see how the tools fit together.

```text
                 You
                  │
                  ▼
           Angular CLI
                  │
                  ▼
             Node.js Runtime
                  │
                  ▼
          npm Package Manager
                  │
                  ▼
      Angular Packages & Libraries
                  │
                  ▼
        Your Angular Project
```

Each layer has a different responsibility.

***

# Step 1 — Why Do We Need Node.js?

This is one of the most common beginner questions.

> **"Angular runs in the browser. So why do I need Node.js?"**

Excellent question.

Angular **applications** run in the browser.

But **building** Angular applications happens on your computer.

For example:

* Creating a project
* Installing libraries
* Compiling TypeScript
* Bundling JavaScript
* Running the development server

These are development tasks, not browser tasks.

Node.js provides the environment where these tools can run.

Think of it like this:

```text
Browser
Runs your Angular application.

Node.js
Builds your Angular application.
```

Node.js is **not** shipped to your users. It's mainly for developers.

***

# Step 2 — What is npm?

When you install Node.js, you also get **npm**.

**npm** stands for:

> **Node Package Manager**

Imagine you want to use Angular.

Instead of downloading hundreds of files manually,

npm downloads everything automatically.

Example:

```bash
npm install
```

npm reads a file called:

```text
package.json
```

and downloads every required package.

Without npm, managing dependencies would be tedious.

***

# Step 3 — What is Angular CLI?

CLI means:

> **Command Line Interface**

Instead of manually creating dozens of folders and configuration files, Angular CLI does it for you.

Without Angular CLI:

```text
Create folders manually

Write configuration manually

Install packages manually

Configure TypeScript manually

Configure build tools manually
```

With Angular CLI:

```bash
ng new my-app
```

One command sets up a complete Angular project.

Later, you'll also use it to generate components, services, and more.

***

# Installation on Debian 13 (Recommended for Your Laptop)

Since you're using Debian 13 now, this will be your main setup.

## Step 1 — Check if Node.js is installed

Open a terminal:

```bash
node -v
```

Example output:

```text
v22.18.0
```

Then check npm:

```bash
npm -v
```

Example:

```text
10.9.3
```

***

### If Node.js is missing

If `node` or `npm` isn't found, you have two common options:

* Install from Debian's repositories (`apt`) — simple and stable, but versions may lag behind.
* Install using a Node version manager such as `nvm` — gives you easy upgrades and multiple Node versions.

For learning Angular, I recommend **using `nvm`** because it makes upgrading and switching Node versions much easier without requiring administrator privileges.

> **Note:** Earlier, when you were learning TypeScript, you installed Node.js through `apt`. If that installation is still present and reasonably current, you can continue using it for now. We can switch to `nvm` later if needed.

***

## Step 2 — Install Angular CLI

Once Node.js and npm are working:

```bash
npm install -g @angular/cli
```

What this does:

* Downloads Angular CLI
* Installs the `ng` command globally
* Makes `ng` available from any terminal

***

## Step 3 — Verify Installation

```bash
ng version
```

You'll see information such as:

* Angular CLI version
* Node version
* npm version
* Operating System

This confirms the CLI is installed correctly.

***

# Installation on Windows 11

When you switch to your desktop, follow these steps.

### Step 1

Download the **LTS (Long-Term Support)** version of Node.js from the official website.

During installation:

✔ Leave the default settings.

✔ Ensure npm is included (it is by default).

***

### Step 2

Open either:

* Command Prompt
* PowerShell
* Windows Terminal

Check:

```bash
node -v
```

```bash
npm -v
```

***

### Step 3

Install Angular CLI:

```bash
npm install -g @angular/cli
```

***

### Step 4

Verify:

```bash
ng version
```

If you see version information, your Windows setup is ready.

***

# Creating Your First Angular Project

Now comes the exciting part.

Create a project:

```bash
ng new hello-angular
```

Angular CLI will ask you a few questions.

For your first project, the defaults are usually fine. In current versions, you'll typically be asked about features such as routing and stylesheet format.

For example:

```
Would you like to add Angular routing?
```

Choose:

```
Yes
```

Even if you won't use routing immediately, enabling it now saves you from adding it later.

Next:

```
Which stylesheet format?
```

Choose:

```
CSS
```

We'll learn other options like SCSS after you've mastered the basics.

***

# What Happens Behind the Scenes?

When you press **Enter**, Angular CLI does much more than create a folder.

It:

1. Creates the project directory.
2. Generates the recommended Angular file structure.
3. Creates configuration files.
4. Sets up TypeScript.
5. Creates the initial application.
6. Downloads Angular packages using npm.
7. Installs project dependencies into `node_modules`.

All of this can take a few minutes, especially the first time.

***

# Running the Application

Navigate into your project:

```bash
cd hello-angular
```

Start the development server:

```bash
ng serve
```

or

```bash
ng serve --open
```

The `--open` (or `-o`) option automatically opens your default browser.

***

Then visit:

```text
http://localhost:4200
```

If everything worked, you'll see the default Angular welcome page.

Congratulations! You've created and run your first Angular application.

***

# Common Beginner Mistakes

### ❌ Running `ng` before installing the CLI

You'll get:

```text
ng: command not found
```

or on Windows:

```text
'ng' is not recognized...
```

Install the Angular CLI first.

***

### ❌ Forgetting to enter the project directory

Running:

```bash
ng serve
```

outside your project folder won't work.

Always:

```bash
cd hello-angular
```

first.

***

### ❌ Confusing global and local installs

`npm install -g @angular/cli` installs the CLI globally, so you can run `ng` from anywhere.

The Angular libraries for a specific application are installed locally inside that project's `node_modules` directory when you create the project.

***

# Hands-on Exercise

On your **Debian 13 laptop**:

1. Check your installed versions:

   * `node -v`
   * `npm -v`
2. Install Angular CLI if you haven't already.
3. Verify with:

   * `ng version`
4. Create a project named:

   ```bash
   ng new hello-angular
   ```
5. Start it:

   ```bash
   cd hello-angular
   ng serve --open
   ```
6. Confirm you can access `http://localhost:4200`.

***

# Lesson Summary

Today you learned:

* ✅ Why Angular requires Node.js
* ✅ What npm does
* ✅ What Angular CLI is
* ✅ How to install Angular on Debian 13 and Windows 11
* ✅ How to create your first Angular project
* ✅ What Angular CLI generates behind the scenes
* ✅ How to run the development server

***

## Before Lesson 1.3

Complete the hands-on exercise. If you encounter any errors during installation or project creation, send me:

* The exact command you ran.
* The full error message (copy and paste it if possible).

We'll troubleshoot it together before moving on to **Lesson 1.3 — Understanding the Angular Project Structure**, where we'll examine every file and folder that `ng new` created and explain its purpose.
