Excellent. This is one of those modules that pays dividends for years. When beginners have a Tomcat problem, they often have no idea where to look because all the folders look mysterious.

After today, when you see:

```text
/home/araf/server/apache-tomcat-9.0.119/
```

you'll know what almost every important file and folder is for.

---

# Day 1 – Module 1.2

# Inside the Tomcat Directory

We'll use **your** installation:

```text
/home/araf/server/apache-tomcat-9.0.119/
```

---

# Before We Start

Let's see the structure.

If you run:

```bash
cd /home/araf/server/apache-tomcat-9.0.119

ls
```

You'll probably see something similar to:

```text
bin/
conf/
lib/
logs/
temp/
webapps/
work/
webapps.dist/

BUILDING.txt
LICENSE
NOTICE
README.md
RELEASE-NOTES
RUNNING.txt
```

Don't worry about every file.

We'll focus on the ones you'll actually use.

---

# Big Picture

Think of Tomcat as a company.

```text
Tomcat

├── bin        → Employees who start the company
├── conf       → Company rules
├── lib        → Shared tools
├── logs       → Company diary
├── temp       → Temporary workspace
├── webapps    → Customer projects
├── work       → Tomcat's workshop
└── webapps.dist → Backup/example applications
```

That analogy isn't perfect, but it's surprisingly useful.

---

# 1. `bin/`

Location:

```text
/home/araf/server/apache-tomcat-9.0.119/bin
```

This folder contains scripts used to control Tomcat.

Let's list it:

```bash
cd /home/araf/server/apache-tomcat-9.0.119/bin

ls
```

You'll see many files.

Don't panic.

You'll only use a few regularly.

---

## `startup.sh`

Starts Tomcat.

```bash
./startup.sh
```

Internally, it calls another script (`catalina.sh`) with the `start` command.

Think of it as a convenient shortcut.

> For windows use `startup.bat`
---

## `shutdown.sh`

Stops Tomcat.

```bash
./shutdown.sh
```

Again, it's a convenience wrapper around `catalina.sh`.

> In windows use `shutdown.bat`
---

## `catalina.sh`

This is the **real** control script.

Almost everything eventually goes through it.

For example:

```bash
./catalina.sh start
```

or

```bash
./catalina.sh stop
```

or

```bash
./catalina.sh run
```

Later, when debugging, you'll often use:

```bash
./catalina.sh run
```

because it keeps Tomcat attached to your terminal and prints logs directly there.

---

## Why Do `startup.sh` and `shutdown.sh` Exist?

Good question.

Instead of remembering:

```bash
./catalina.sh start
```

you can simply type:

```bash
./startup.sh
```

They're helper scripts.

---

# 2. `conf/`

Location:

```text
/home/araf/server/apache-tomcat-9.0.119/conf
```

This is one of the most important directories.

It contains Tomcat's configuration.

---

## Inside `conf/`

You'll see files like:

```text
server.xml
web.xml
context.xml
tomcat-users.xml
logging.properties
```

Let's understand each.

---

## `server.xml`

This is Tomcat's main configuration file.

It defines things such as:

* HTTP port
* Connectors
* Engine
* Host
* Services

For now, the most interesting part is the HTTP connector.

You'll find something similar to:

```xml
<Connector port="8080"
           protocol="HTTP/1.1" />
```

That's why Tomcat listens on port **8080**.

If you changed it to:

```xml
port="9090"
```

you'd access Tomcat with:

```text
http://localhost:9090
```

---

## `web.xml`

This is called the **Deployment Descriptor**.

Historically, developers configured many web application settings here, such as:

* Welcome pages
* Error pages
* Session timeout
* Filters
* Servlets

Modern Java applications often use annotations instead, but `web.xml` is still important to understand.

We'll revisit it when we build our first application.

---

## `context.xml`

Defines default settings for web applications.

You'll rarely modify it as a beginner.

---

## `tomcat-users.xml`

Stores Tomcat users and roles.

This is **not** your application's user database.

It's for Tomcat's own administration features (like the Manager app).

---

## `logging.properties`

Controls how Tomcat writes logs.

Most beginners never need to edit it.

---

# 3. `lib/`

Location:

```text
/home/araf/server/apache-tomcat-9.0.119/lib
```

This folder contains JAR files that Tomcat itself uses.

Examples include the Servlet API and JSP libraries.

---

## Why Doesn't Java Already Have These?

Excellent question.

The JDK provides the Java language and standard libraries.

Tomcat provides **web-specific APIs**, such as:

* Servlet API
* JSP API

Without these libraries, Java wouldn't know what classes like `HttpServletRequest` are.

---

# 4. `logs/`

Location:

```text
/home/araf/server/apache-tomcat-9.0.119/logs
```

This folder stores log files.

Think of logs as Tomcat's diary.

Whenever something important happens, Tomcat writes it down.

Examples:

* Tomcat started.
* Tomcat stopped.
* Errors occurred.
* Exceptions were thrown.

When something goes wrong, this is one of the first places developers check.

---

# 5. `temp/`

Location:

```text
/home/araf/server/apache-tomcat-9.0.119/temp
```

Stores temporary files.

Tomcat uses it internally.

==You generally don't interact with it directly==.

---

# 6. `webapps/`

==This is the folder you'll spend the most time with==.

Location:

```text
/home/araf/server/apache-tomcat-9.0.119/webapps
```

Every web application lives here.

For example:

```text
webapps/

ROOT/
StudentManagement/
LibrarySystem/
```

==Each subdirectory represents a web application==.

---

## Example

Suppose you create:

```text
webapps/
    StudentManagement/
```

Then you can access it with:

```text
http://localhost:8080/StudentManagement
```

Notice the connection to the **context path** we learned earlier.

The folder name becomes the context path (unless you configure it differently).

---

# What Is `ROOT/`?

This folder is special.

If you visit:

```text
http://localhost:8080/
```

Tomcat serves the application inside `ROOT/`.

Think of `ROOT` as the default web application.

If you delete or replace it, the homepage changes accordingly.

---

# 7. `work/`

This folder confuses many beginners.

Tomcat uses it as a working area.

One important thing happens here:

When Tomcat receives a JSP for the first time, it:

```text
index.jsp

↓

Generates Java Servlet source

↓

Compiles it

↓

Stores generated files in work/
```

This is why JSPs often load a little slower the **first** time after starting Tomcat—they need to be translated and compiled.

Subsequent requests are faster because Tomcat reuses the compiled version.

---

# 8. `webapps.dist/`

Depending on how Tomcat was installed, you may see a `webapps.dist/` directory.

It typically contains default/example web applications provided with Tomcat.

Many Linux package installations use this directory to separate packaged defaults from deployed applications.

For learning JSP, you usually won't touch it.

---

# Putting It All Together

When you start Tomcat:

```bash
cd /home/araf/server/apache-tomcat-9.0.119/bin

./startup.sh
```

A simplified sequence is:

```text
startup.sh
        │
        ▼
catalina.sh
        │
        ▼
Read conf/
        │
        ▼
Load lib/
        │
        ▼
Deploy webapps/
        │
        ▼
Listen on port 8080
        │
        ▼
Wait for HTTP requests
```

---

# Your Typical Workflow (Soon)

Once we start coding JSP, you'll often work like this:

```text
Write JSP

↓

Save file

↓

Place project in webapps/

↓

Start Tomcat

↓

Open Firefox

↓

http://localhost:8080/YourProject

↓

Test

↓

Check logs/ if something fails

↓

Repeat
```

As projects become more advanced, IDEs like Eclipse or IntelliJ automate deployment, but understanding what's happening underneath is invaluable.

---

# Knowledge Check

Answer these without looking back.

### Question 1

What is the purpose of the `bin/` directory?

---

### Question 2

Which script actually performs most of the work behind starting and stopping Tomcat?

* `startup.sh`
* `shutdown.sh`
* `catalina.sh`

Why?

---

### Question 3

Which directory contains Tomcat's configuration files?

---

### Question 4

Which file would you edit if you wanted Tomcat to listen on **9090** instead of **8080**?

---

### Question 5

Where should your `StudentManagement` web application be placed?

---

### Question 6

What is the purpose of the `work/` directory?

---

### Question 7 (Thinking Question)

Suppose you edit `server.xml` and change the port from **8080** to **9090**, but you **do not restart Tomcat**.

Then you open:

```text
http://localhost:9090
```

Do you expect it to work?

Why or why not?

This question introduces an important idea about configuration files and when changes actually take effect.

# Answer and feedback
🎉 **Outstanding. 7/7 again.**

And I want to point out something that makes me happy as your teacher: **you're starting to reason from first principles instead of relying on memory.** That's exactly how good software engineers think.

Let's review.

---

## Question 1 ✅

> It contains scripts that are used to control Tomcat.

Perfect.

Examples:

```text
startup.sh
shutdown.sh
catalina.sh
```

These scripts don't *contain* Tomcat—they **control** it.

---

## Question 2 ✅

> catalina.sh because startup.sh uses catalina.

Exactly.

Think of it like this:

```
startup.sh
      │
      ▼
catalina.sh start
```

and

```
shutdown.sh
      │
      ▼
catalina.sh stop
```

`startup.sh` and `shutdown.sh` are convenience wrappers.

`catalina.sh` is the real engine.

---

## Question 3 ✅

```
conf/
```

Correct.

Everything about configuring Tomcat starts here.

---

## Question 4 ✅

```
conf/server.xml
```

Exactly.

Inside you'll find something like:

```xml
<Connector port="8080"
           protocol="HTTP/1.1"/>
```

Changing it to:

```xml
port="9090"
```

changes the listening port **after Tomcat is restarted**.

---

## Question 5 ✅

```
webapps/
```

Exactly.

Soon your folder may look like:

```
webapps/

StudentManagement/
    index.jsp
```

and you'll access it through:

```
http://localhost:8080/StudentManagement
```

---

## Question 6 ✅

You wrote:

> Tomcat uses it as a kind of workspace...

Excellent.

Then you remembered:

> something to do with JSP...

Exactly.

Let's make it precise.

Suppose you create:

```
index.jsp
```

Tomcat internally does this:

```
index.jsp

↓

Generate Java source

↓

Compile

↓

Store compiled files in work/

↓

Execute
```

The `work/` directory is essentially Tomcat's **build workspace**.

That's why it's called **work**.

Many beginners think:

> "work contains my project."

No.

It contains **Tomcat's generated artifacts**, especially those related to JSP compilation.

---

## Question 7 ⭐⭐⭐⭐⭐

This answer impressed me.

You wrote:

> Tomcat already has the configs in memory...

Exactly.

This is precisely how experienced developers think.

Let's visualize it.

---

### Tomcat Startup

```
server.xml

↓

Tomcat reads it

↓

Configuration loaded into memory

↓

Tomcat starts listening
```

Now imagine you edit:

```
server.xml
```

What happens?

Nothing.

Because Tomcat isn't constantly watching the file.

It's already using the configuration it loaded when it started.

Only after restarting:

```
Stop

↓

Read server.xml again

↓

Start
```

does the new configuration take effect.

---

## This Principle Exists Everywhere

You'll encounter this pattern many times:

### Tomcat

```
server.xml

↓

Restart Required
```

---

### Spring Boot

```
application.properties

↓

Restart Required
```

---

### Nginx

```
nginx.conf

↓

Reload Required
```

---

### Apache HTTP Server

```
httpd.conf

↓

Restart Required
```

Once a program has read its configuration into memory, changing the file on disk doesn't magically change the running program.

---

# 🧠 One Small Refinement

You said:

> "temporary memory like RAM"

That's actually correct.

Just use the term:

> **RAM (main memory)**

instead of "temporary memory."

When Tomcat starts, it loads its configuration into RAM.

That's exactly what happens.

---

# 🏆 Congratulations!

You have now completed **Module 1.2**.

Here's your progress so far:

```
Day 1

Module 0
──────────────
✅ Client vs Server
✅ HTTP Basics
✅ HTTP Methods
✅ URL Anatomy
✅ Stateless HTTP

Module 1
──────────────
✅ What is Tomcat?
✅ Tomcat Directory Structure

Next:
⬜ Tomcat Startup Process
⬜ Deploying Your First Web App
⬜ JSP Lifecycle
```

---

# 🎯 Before We Continue...

This is a good moment to transition from **theory** to **real Tomcat**.

So instead of immediately continuing with more theory, I'd like to spend the next module interacting with **your actual installation** at:

```text
/home/araf/server/apache-tomcat-9.0.119
```

We'll verify that everything is working and connect what you've learned to the real server.

We'll cover:

* Starting Tomcat
* Stopping Tomcat
* Understanding what each startup message means
* Verifying Tomcat is listening on port **8080**
* Accessing the default Tomcat page in Firefox
* Understanding what happens internally during startup
* Reading Tomcat log messages
* Creating your **very first web application** (before writing JSP)

I intentionally don't want to jump into JSP syntax yet. I want you to become comfortable with the environment first. By the time we create your first `index.jsp`, you'll know exactly **where it goes, how Tomcat finds it, and what Tomcat does with it** behind the scenes. I think that's a much stronger foundation than simply saying "create a JSP file and run it."

# ➡️ [[Module 1.3 Starting Tomcat & Understanding What Happens]].