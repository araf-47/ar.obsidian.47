# Lesson 1.4 — Running the Application, Development Server & Build Process

This lesson is about what happens **after you create an Angular project**: how to run it during development and how Angular turns your source code into something that can be deployed.

***

## 1. Theory

### Running the Angular application

An Angular project contains your application source code, configuration, dependencies, and build information.

You normally work with it in two different situations:

**During development:**

```text
Your Angular code
       ↓
Development server
       ↓
Browser
```

**When preparing the application for deployment:**

```text
Your Angular code
       ↓
Angular build process
       ↓
Production build files
       ↓
Web server
```

The important distinction is:

> `ng serve` is mainly for **development**.
> `ng build` creates files that can be **deployed**.

***

## 2. How It Works Internally

### `ng serve`

When you run:

```bash
ng serve
```

Angular starts a **development server**.

The server watches your project files. When you change your Angular code, Angular detects the change and updates the application.

The browser then displays the updated application.

A simplified mental model:

```text
You edit app.component.ts
          ↓
Angular detects the change
          ↓
Development build/update
          ↓
Browser receives updated application
```

This is why you don't normally have to manually rebuild the application after every small code change.

### Important

The development server is **not your production server**.

It exists mainly to make development convenient.

***

## 3. Syntax

Open a terminal inside your Angular project directory.

### Start the development server

```bash
ng serve
```

You can also use:

```bash
ng serve --open
```

`--open` tells Angular to open the application in your default browser.

You will typically see something similar to:

```text
Local: http://localhost:4200/
```

Open that address in your browser.

You can also use the npm script:

```bash
npm start
```

In a standard Angular project, this runs the development server through the project's configured scripts.

***

### Stop the development server

In the terminal where it is running:

```text
Ctrl + C
```

***

### Build the application

Run:

```bash
ng build
```

This tells Angular to build your application.

Angular processes your source code and produces build output.

The output is normally placed in:

```text
dist/
```

For example:

```text
my-angular-app/
├── src/
├── public/
├── angular.json
├── package.json
└── dist/
```

The exact contents and structure of `dist/` can vary with Angular configuration and version.

***

## 4. Examples

### Example 1 — Start development

Suppose your project is:

```text
my-angular-app/
```

Navigate into it:

```bash
cd my-angular-app
```

Then:

```bash
ng serve
```

You should get a local address such as:

```text
http://localhost:4200/
```

Visit it in your browser.

***

### Example 2 — Make a change

Suppose you change your component template:

```html
<h1>Hello Angular</h1>
```

to:

```html
<h1>Hello World</h1>
```

Save the file.

The development server notices the change and updates the application.

You normally don't need to:

```bash
ng build
```

every time you make a development change.

***

### Example 3 — Create a build

When you want Angular to produce the deployable application files:

```bash
ng build
```

Think of this as:

```text
Source code
    ↓
Angular build
    ↓
Browser-ready application files
    ↓
dist/
```

Those generated files are what you would ultimately deploy to a web server or hosting service.

***

## Development vs Build

| Command           | Purpose                                |
| -------------- | -------------------------------------- |
| `ng serve`        | Run the application during development |
| `ng serve --open` | Run it and open the browser            |
| `ng build`        | Create build output                    |
| `Ctrl + C`        | Stop the development server            |

The simplest mental model is:

```text
ng serve
   ↓
"I am developing and want to see my app."

ng build
   ↓
"I want Angular to produce the application files."
```

***

## 5. Common Mistakes

### Mistake 1 — Running the command outside the project

If you are not inside the Angular project directory:

```bash
ng serve
```

may fail because Angular cannot find the project configuration.

Make sure you are inside:

```text
my-angular-app/
```

before running it.

***

### Mistake 2 — Thinking `ng serve` creates deployment files

`ng serve` is primarily a development workflow.

Don't think:

```text
ng serve = production deployment
```

Instead:

```text
ng serve = development server
ng build = build application
```

***

### Mistake 3 — Closing the terminal

If you start:

```bash
ng serve
```

and then close the terminal, the development server stops.

The terminal is running the server process.

***

### Mistake 4 — Manually editing `dist/`

Don't normally edit files inside:

```text
dist/
```

They are generated output.

Your actual source code lives in your project source files, such as:

```text
src/
```

Then Angular generates the build output again when you run:

```bash
ng build
```

***

## 6. Hands-on Exercise

Use the Angular project you created in **Lesson 1.2**.

### Step 1

Open a terminal inside the project:

```bash
cd your-project-name
```

### Step 2

Start the development server:

```bash
ng serve
```

### Step 3

Open:

```text
http://localhost:4200/
```

### Step 4

Change something visible in your root component's template.

For example, change some existing text to:

```html
<h1>My Angular Application</h1>
```

Save the file and observe the browser update.

### Step 5

Stop the server:

```text
Ctrl + C
```

### Step 6

Build the application:

```bash
ng build
```

Check that Angular created the:

```text
dist/
```

directory.

**Your task:** tell me what you observed from `ng serve` and `ng build`, especially what appeared in the terminal and what was created inside `dist/`.

***

## 7. Quick Review

### Question 1

What is `ng serve` primarily used for?

> A. Deploying an application
> B. Running the application during development
> C. Creating a database
> D. Installing Angular

**Correct answer: B**

`ng serve` starts Angular's development server.

***

### Question 2

What does `ng build` do?

> A. Starts the development server
> B. Creates Angular build output
> C. Creates a new component
> D. Installs dependencies

**Correct answer: B**

`ng build` processes the application and produces build output.

***

### Question 3

Where is Angular build output normally placed?

> A. `src/`
> B. `node_modules/`
> C. `dist/`
> D. `public/`

**Correct answer: C**

Angular normally places generated build output under `dist/`.

***

### Question 4

What happens when you save a source file while `ng serve` is running?

> A. Angular can detect the change and update the development application
> B. The project is permanently deployed
> C. The `dist/` directory is manually edited
> D. Angular deletes the source file

**Correct answer: A**

The development server watches for changes and updates the application.

***

### Question 5

Which command can start the development server and open the browser?

> A. `ng build --open`
> B. `ng serve --open`
> C. `ng install --open`
> D. `ng browser`

**Correct answer: B**

`ng serve --open` starts the development server and opens the application in the browser.

***

## Progress

**Completed:** Lesson 1.4 — Running the Application, Development Server & Build Process

**Next:** Lesson 2.1 — What is a Component? / Component Anatomy

**Module 1 is now complete.** You should now understand what Angular is at a basic level, how to create an Angular project, its modern project structure, and how to run and build it.
