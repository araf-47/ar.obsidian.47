
Excellent. This is where the course starts becoming hands-on.

From this point onward, I want you to have **Tomcat running while we're learning**. Instead of me saying "trust me," you'll actually see what Tomcat is doing.

---

# Day 1 – Module 1.3

# Starting Tomcat & Understanding What Happens

We'll use your installation:

```text
/home/araf/server/apache-tomcat-9.0.119
```

---

# Learning Objectives

By the end of this module, you'll be able to:

* Start Tomcat
* Stop Tomcat
* Verify that it's running
* Understand the startup messages
* Understand what Tomcat does during startup
* Know where to look if something goes wrong

---

# Step 1 — Check That Java Exists

Tomcat is written in Java.

Without Java, Tomcat cannot run.

Run:

```bash
java -version
```

Example output:

```text
openjdk version "21.0.7"
```

**Question for you:**

What does your command output?

(Don't continue until you've checked.)

---

# Step 2 — Go to Tomcat

```bash
cd /home/araf/server/apache-tomcat-9.0.119/bin
```

Let's see what's inside.

```bash
ls
```

You should recognize:

```text
startup.sh
shutdown.sh
catalina.sh
```

Notice how familiar these already are.

---

# Step 3 — Start Tomcat

Run:

```bash
./startup.sh
```

Typical output:

```text
Using CATALINA_BASE: ...
Using CATALINA_HOME: ...
Using CATALINA_TMPDIR: ...
Using JRE_HOME: ...
Using CLASSPATH: ...
Tomcat started.
```

Don't worry about every line yet.

Let's decode them.

---

# What Happens Internally?

Imagine Tomcat as a factory opening in the morning.

## Phase 1

```text
Read Configuration
```

Tomcat opens:

```text
conf/server.xml
```

It asks:

* Which port?
* Which host?
* Which applications?

---

## Phase 2

```text
Load Libraries
```

Tomcat loads every JAR from:

```text
lib/
```

Now it understands:

* Servlets
* JSP
* Sessions
* Cookies

---

## Phase 3

```text
Create Internal Components
```

Tomcat builds its internal objects.

Think of this as the engine warming up.

---

## Phase 4

```text
Open Port 8080
```

Tomcat tells Linux:

> "I'm listening on port 8080."

Now Firefox can connect.

---

## Phase 5

```text
Deploy Applications
```

Tomcat scans:

```text
webapps/
```

Example:

```text
ROOT/
manager/
host-manager/
docs/
examples/
```

Each application is prepared.

---

## Phase 6

Tomcat waits.

Literally.

Nothing happens until a browser sends a request.

---

# The Complete Startup

```text
startup.sh

↓

catalina.sh

↓

Read conf/

↓

Load lib/

↓

Open port 8080

↓

Deploy webapps/

↓

Wait for Browser
```

Notice how every folder you've learned now has a role.

---

# Step 4 — Verify Tomcat Is Running

Open Firefox.

Visit:

```text
http://localhost:8080
```

If everything is working, you'll usually see the default Tomcat welcome page (unless you've replaced the `ROOT` application).

That page is simply proof that:

* Firefox can reach Tomcat.
* Tomcat is listening on port 8080.
* The default web application is deployed.

---

# Step 5 — Verify from the Terminal

Instead of trusting Firefox, let's ask Linux directly.

Run:

```bash
ss -ltn | grep 8080
```

If Tomcat is running, you'll see a line indicating something is **LISTENING** on port **8080**.

This tells us:

> A program has successfully opened port 8080.

Notice:

This command does **not** tell us it's Tomcat specifically.

It only tells us **something** is listening on that port.

---

# Step 6 — Stop Tomcat

Run:

```bash
./shutdown.sh
```

Tomcat closes:

* Port 8080
* Sessions
* Applications

Then exits.

---

# Verify It Stopped

Run again:

```bash
ss -ltn | grep 8080
```

You should get **no output**.

Why?

Because no process is listening anymore.

---

# What Happens If Port 8080 Is Already Used?

Imagine another program is already using:

```text
8080
```

Tomcat tries to start.

Linux says:

> Sorry.

> That port is already occupied.

Tomcat cannot listen on the same port.

You'll usually see an error about the address already being in use.

This is one reason you might change Tomcat to another port (for example, 9090) in `server.xml`.

---

# Where Do We Look If Startup Fails?

Remember this folder?

```text
logs/
```

This is where Tomcat writes startup information and errors.

If Tomcat refuses to start, the logs are often your first stop.

---

# A Common Beginner Mistake

Suppose Tomcat is stopped.

You open:

```text
http://localhost:8080
```

Firefox reports it can't connect.

Many beginners think:

> "My JSP is broken."

But your JSP hasn't even been reached yet.

The browser couldn't connect to Tomcat at all.

Always ask yourself:

1. Is Tomcat running?
2. Is it listening on the expected port?
3. Only then start debugging your application.

This simple habit will save you a lot of time.

---

# Knowledge Check

Let's combine theory with practice.

### Question 1

Why do we need Java installed before Tomcat can run?

---

### Question 2

What are the six major startup phases we discussed?

Try to list them in order.

---

### Question 3

What command starts Tomcat?

---

### Question 4

What command stops Tomcat?

---

### Question 5

What does this command check?

```bash
ss -ltn | grep 8080
```

---

### Question 6

Suppose Firefox says:

> Unable to connect

What is the **first thing** you should check before looking at your JSP code?

---

### Question 7 (Practical)

Please perform these steps on your Debian machine:

1. Run:

```bash
java -version
```

2. Start Tomcat:

```bash
cd /home/araf/server/apache-tomcat-9.0.119/bin
./startup.sh
```

3. Open:

```text
http://localhost:8080
```

4. Run:

```bash
ss -ltn | grep 8080
```

Then **paste the outputs here** (or tell me exactly what happened at each step).

---

## 📌 A small note about your setup

Earlier, you mentioned you're planning to use **SQLite with JDBC** and eventually move to **Spring Boot**. I think that's an excellent learning path:

* JSP + Servlets → learn how the web actually works.
* JDBC + SQLite → understand database access without the complexity of a database server.
* Spring Boot → appreciate what the framework automates because you'll already understand what's happening underneath.

By the time we reach Spring Boot, concepts like controllers, sessions, request handling, and dependency injection will feel much less "magical" because you'll have built the foundation yourself.


# Answer and feedback
Excellent! This is the point where theory meets reality. Everything you've learned is now reflected in your actual Tomcat installation.

I'd give this another **7/7**.

## Question 1 ✅

> Because it is a Java server.

Exactly.

A slightly more precise explanation:

> **Tomcat itself is a Java application. Therefore, the JVM (Java Virtual Machine) must be installed before Tomcat can run.**

Think of it like this:

```text
Tomcat
    │
runs on
    ▼
JVM
    │
provided by
    ▼
Java Installation
```

Without Java, there is no JVM.

Without the JVM, Tomcat cannot execute.

---

## Question 2 ✅

You remembered almost everything.

The exact order is:

```
startup.sh
      ↓
catalina.sh
      ↓
Read conf/
      ↓
Load lib/
      ↓
Open Port 8080
      ↓
Deploy webapps/
      ↓
Wait for Requests
```

Notice one small correction:

Tomcat opens **port 8080 before** it begins waiting for requests.

Once the port is open, it sits there waiting.

---

## Question 3 & 4 ✅

Correct.

```
./startup.sh
```

starts Tomcat.

```
./shutdown.sh
```

stops Tomcat.

---

## Question 5 ✅

Exactly.

```
ss -ltn | grep 8080
```

asks Linux:

> "Is any process listening on TCP port 8080?"

It doesn't know *which* process. It just reports that something is listening.

---

## Question 6 ✅

Excellent troubleshooting sequence.

You said:

1. Is Tomcat started?
2. Is it listening on 8080?
3. Then check the logs.

That's exactly the order experienced developers use.

Many beginners immediately start changing JSP code, even though the server isn't running.

---

# Question 7 — Let's Analyze Your Real Output

---

## Java Version

```text
openjdk version "21.0.11"
```

Perfect.

Tomcat 9 works well with Java 21.

No issues here.

---

## Startup

```
Using CATALINA_BASE
Using CATALINA_HOME
Using CATALINA_TMPDIR
Using JRE_HOME
Using CLASSPATH
Tomcat started.
```

Let's decode each one.

---

### CATALINA_HOME

```
/home/araf/server/apache-tomcat-9.0.119
```

This tells Tomcat:

> "This is where I am installed."

Correct.

---

### CATALINA_BASE

Notice it's the same directory.

That's completely normal.

Later, in production, these can be different.

For learning:

```
CATALINA_HOME == CATALINA_BASE
```

is perfectly fine.

---

### CATALINA_TMPDIR

```
temp/
```

Exactly the folder we discussed.

Tomcat stores temporary files here.

---

### JRE_HOME

```
/usr
```

Tomcat successfully found Java.

Excellent.

---

### CLASSPATH

```
bootstrap.jar
tomcat-juli.jar
```

Don't worry about these yet.

Just know:

These are some of the libraries Tomcat needs to start.

We'll study the classpath much later.

---

### Tomcat started.

This is exactly what we wanted.

---

# Browser Test

You said:

> It's showing my webpage.

Excellent.

That proves:

```
Firefox

↓

localhost

↓

8080

↓

Tomcat

↓

ROOT Application

↓

HTML

↓

Firefox
```

Every part of that chain is working.

---

# ss Output

You got:

```
LISTEN
*:8080
```

Perfect.

This means:

Linux confirms:

> A process is listening on TCP port 8080.

Exactly what we expected.

---

# Let's Connect Everything

Today, when you typed:

```
http://localhost:8080
```

this is what **actually happened**:

```
You
 │
 ▼
Firefox
 │
 │ GET /
 ▼
Linux Networking
 │
 ▼
Port 8080
 │
 ▼
Tomcat
 │
 ▼
ROOT Web Application
 │
 ▼
Generated HTML
 │
 ▼
HTTP Response
 │
 ▼
Firefox
 │
 ▼
Screen
```

Notice something amazing.

Every concept from Module 0 has now appeared in real life.

* ✅ Client
* ✅ Server
* ✅ HTTP
* ✅ URL
* ✅ Port
* ✅ Tomcat
* ✅ Web Application

Nothing has been theoretical anymore.

---
⚠️ [[heloC response - 2TF9z]].
