# Lesson 1.2 — Installing Node.js, Angular CLI, and Creating Your First Project

This lesson gets your computer ready for Angular development. By the end, you will have a working Angular project running locally.

I checked the current Angular documentation first. The current Angular installation guide requires **Node.js 22.22.3 or newer**, and the current Node.js download page lists **Node.js 24.21.0 as LTS**. ([Angular][1])

***

## 1. Theory

### What is Node.js?

Node.js lets JavaScript code run **outside the browser**.

Normally:

```text
JavaScript → Browser
```

With Node.js:

```text
JavaScript → Node.js → Your computer
```

Angular uses Node.js during development.

For example, when you run:

```bash
ng serve
```

Angular's development tools run through Node.js.

### What is npm?

When Node.js is installed, it also includes **npm**.

npm is a package manager.

It allows you to install JavaScript packages and tools.

For example:

```bash
npm install -g @angular/cli
```

means:

> Use npm to install the Angular CLI globally.

***

## 2. How It Works Internally

Think of the setup like this:

```text
Node.js
   │
   └── npm
        │
        └── Angular CLI
              │
              ├── Create Angular projects
              ├── Run development server
              ├── Generate files
              └── Build Angular applications
```

The Angular CLI is a command-line tool published as the `@angular/cli` npm package. Its command is `ng`. ([Angular][2])

So when you type:

```bash
ng
```

you are using the Angular CLI.

***

## 3. Install Node.js

### Step 1 — Check whether Node.js is already installed

Open your terminal and run:

```bash
node --version
```

Also check npm:

```bash
npm --version
```

If Node.js is not installed, install the current **LTS** version from the official Node.js website.

[Node.js official download page](https://nodejs.org/en/download/?utm_source=chatgpt.com)

For the current Angular release, Angular's documentation lists **Node.js 22.22.3 or newer** as the requirement. ([Angular][1])

The current Node.js LTS is **24.21.0**. ([Node.js][3])

After installation, verify:

```bash
node --version
```

You should get something similar to:

```text
v24.21.0
```

The exact version may change as Node.js releases new versions.

Then:

```bash
npm --version
```

You should get an npm version number.

***

## 4. Install Angular CLI

Once Node.js and npm work, install Angular CLI:

```bash
npm install -g @angular/cli
```

The `-g` means **global**.

It makes the `ng` command available from your terminal rather than installing it only inside one project. Angular's official installation guide uses this command. ([Angular][1])

Now verify it:

```bash
ng version
```

You should see Angular CLI information.

You can also use:

```bash
ng --version
```

`ng version` reports the Angular version information for the environment/project. ([Angular][4])

***

## 5. Create Your First Angular Project

Now we can create an Angular application.

First, move to a folder where you want to keep your Angular projects.

For example:

```bash
cd ~/Projects
```

Then:

```bash
ng new my-first-angular-app
```

Angular CLI will ask you some questions.

The exact prompts can change between Angular versions.

For this lesson, **accept the recommended/default choices** unless the CLI asks you something you don't understand.

Angular's current `ng new` command creates a new workspace and initial application. Standalone applications are the default. ([Angular][5])

After the command finishes, you will have:

```text
Projects/
└── my-first-angular-app/
```

***

## 6. Enter the Project

Move inside the project:

```bash
cd my-first-angular-app
```

You are now inside your Angular workspace.

This distinction is important:

```text
~/Projects/
    │
    └── my-first-angular-app/   ← Angular workspace
```

Commands such as:

```bash
ng serve
ng generate
ng build
```

are normally run from inside the workspace.

***

## 7. Run the Angular Application

Run:

```bash
ng serve
```

Angular will start a development server.

You should see something similar to:

```text
Local: http://localhost:4200/
```

Open this in your browser:

```text
http://localhost:4200
```

You should see the Angular starter application.

You can also let Angular open the browser automatically:

```bash
ng serve --open
```

Angular documents `ng serve --open` as the command for starting the development server and opening the application in the browser. ([Angular][6])

***

## 8. What Just Happened?

You performed this sequence:

```text
Install Node.js
      ↓
npm becomes available
      ↓
Install Angular CLI
      ↓
ng command becomes available
      ↓
ng new my-first-angular-app
      ↓
Angular workspace created
      ↓
cd my-first-angular-app
      ↓
ng serve
      ↓
Angular development server
      ↓
http://localhost:4200
```

That's the basic Angular development environment.

***

## 9. A Few Important Commands

You don't need to memorize everything yet.

Just recognize these:

| Command           | Purpose                       |
| -------------- | ----------------------------- |
| `node --version`  | Check Node.js                 |
| `npm --version`   | Check npm                     |
| `ng version`      | Check Angular CLI/version     |
| `ng new app-name` | Create a new Angular project  |
| `cd app-name`     | Enter the project             |
| `ng serve`        | Start development server      |
| `ng serve --open` | Start server and open browser |

The Angular CLI provides commands for creating, serving, building, generating, testing, and maintaining Angular applications. ([Angular][2])

***

## 10. Common Mistakes

### Mistake 1 — `node: command not found`

This usually means Node.js isn't installed or your terminal cannot find it.

Check:

```bash
node --version
```

If it fails, install Node.js and open a new terminal.

***

### Mistake 2 — `ng: command not found`

Angular CLI isn't available to your shell.

Check:

```bash
ng version
```

If it fails, make sure this completed successfully:

```bash
npm install -g @angular/cli
```

***

### Mistake 3 — Running `ng serve` in the wrong folder

Don't do this:

```text
~/Projects/
$ ng serve
```

if there isn't an Angular workspace there.

Instead:

```bash
cd my-first-angular-app
ng serve
```

`ng new` creates the workspace; commands such as `ng serve` operate on that workspace. ([Angular][6])

***

### Mistake 4 — Thinking `localhost:4200` is a website on the internet

It isn't.

```text
localhost
```

means:

> This computer.

So:

```text
http://localhost:4200
```

means your Angular development server is running on your own computer, using port `4200`.

***

# 11. Hands-On Exercise

Do this yourself rather than just reading it.

### Task

Create a new Angular project called:

```text
angular-learning
```

Follow this sequence:

```bash
node --version
```

```bash
npm --version
```

```bash
ng version
```

Then create the project:

```bash
ng new angular-learning
```

Enter it:

```bash
cd angular-learning
```

Start it:

```bash
ng serve --open
```

Then verify that the Angular application opens in your browser.

### Your checkpoint

Once it is running, tell me:

1. Your Node.js version
2. Your npm version
3. Your Angular CLI version
4. Whether `http://localhost:4200` opened successfully

If you encounter an error, **paste the exact error instead of trying random fixes**.

***

# 12. Quick Review

### Question 1

What does Node.js provide for Angular development?

```text
A. A browser
B. A JavaScript runtime outside the browser
C. An HTML editor
D. A database
```

**Correct answer: B**

Node.js allows JavaScript-based development tools to run outside the browser.

***

### Question 2

What does npm primarily do?

```text
A. Manage JavaScript packages and tools
B. Display Angular pages
C. Replace HTML
D. Run SQL queries
```

**Correct answer: A**

npm is the package manager that comes with Node.js.

***

### Question 3

What does this command install?

```bash
npm install -g @angular/cli
```

```text
A. Node.js
B. Angular CLI globally
C. An Angular component
D. A browser
```

**Correct answer: B**

`@angular/cli` is the Angular CLI package, and `-g` installs it globally.

***

### Question 4

What does this command do?

```bash
ng new angular-learning
```

```text
A. Starts an existing Angular application
B. Deletes an Angular application
C. Creates a new Angular workspace and application
D. Opens the Angular documentation
```

**Correct answer: C**

`ng new` creates a new Angular workspace with an initial application.

***

### Question 5

What does this URL normally point to when `ng serve` is running?

```text
http://localhost:4200
```

```text
A. An Angular application running locally
B. Google's Angular server
C. A remote production server
D. The Node.js website
```

**Correct answer: A**

`localhost` refers to your own computer, and Angular's development server commonly uses port `4200`.

***

## Progress

**Completed:** Lesson 1.2 — Installing Node.js, Angular CLI, and Creating the First Project

**Next:** Lesson 1.3 — Modern Project Structure

* `main.ts`
* `bootstrapApplication()`
* Root component
* `app.config.ts`
* `app.routes.ts`
* `angular.json`
* `tsconfig.json`

Stop here. We will not move into Lesson 1.3 until you ask for it.

[1]: https://angular.dev/installation?utm_source=chatgpt.com "Installation • Angular"
[2]: https://angular.dev/tools/cli?utm_source=chatgpt.com "Angular CLI • Overview • Angular"
[3]: https://nodejs.org/en/download.?utm_source=chatgpt.com "Node.js — Download Node.js®"
[4]: https://angular.dev/update?utm_source=chatgpt.com "Keeping up-to-date • Angular"
[5]: https://angular.dev/cli/new?utm_source=chatgpt.com "ng new • Angular"
[6]: https://angular.dev/tools/cli/setup-local?utm_source=chatgpt.com "Local set-up • Angular"
