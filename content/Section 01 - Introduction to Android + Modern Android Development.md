# Section 01 — Introduction to Android + Modern Android Development

We’ll keep this section focused on **understanding Android and the modern Java/XML development environment**. We will **not** start Activities, layouts, intents, databases, RecyclerView, etc. yet. Those belong to later sections.

The goal for this section is:

> **Understand what you are actually building when you create an Android application, what Android Studio/SDK do, and where Java fits into the picture.**

***

# 1. What is Android?

At the simplest level:

> **Android is an operating system and software platform primarily used on mobile and other embedded devices.**

You can think of Android as playing a role similar to:

* Windows → desktop/laptop
* Linux → servers/desktops/embedded systems
* iOS → iPhone/iPad
* Android → phones, tablets, TVs, watches, cars, etc.

But Android is more than just the operating system from a developer's perspective.

It also provides a large collection of APIs[^1] and services that applications use to interact with the device.

For example, an Android application can use Android's APIs to:

* display UI
* respond to touches
* access the camera
* access location
* make network requests
* store data
* show notifications
* communicate with other applications
* use Bluetooth
* interact with sensors

So when we say:

> "I'm developing an Android application"

we mean:

> "I'm writing software that runs on the Android platform and uses Android's APIs and application framework."

***

# 2. What is an Android Application?

An Android application is software packaged so that Android can install and run it.

Examples:

* WhatsApp
* YouTube
* Google Maps
* banking applications
* games
* your future **LandLord Android application**

Conceptually:

```text
Android Device
      │
      ▼
 Android OS
      │
      ├── Android APIs
      │
      └── Your Application
              │
              ├── Java code
              ├── XML layouts/resources
              ├── configuration
              └── other resources
```

Your application does **not** directly control the hardware.

For example, if your application wants to use the camera, it generally interacts with Android's APIs rather than directly manipulating the camera hardware.

***

# 3. Android OS

**OS** means **Operating System**.

The operating system is the software layer that manages the device and provides services to applications.

A simplified picture:

```text
┌──────────────────────────────┐
│       Your Android App       │
├──────────────────────────────┤
│       Android Framework      │
│          APIs / SDK          │
├──────────────────────────────┤
│       Android Platform       │
├──────────────────────────────┤
│      Linux-based kernel      │
├──────────────────────────────┤
│          Hardware            │
└──────────────────────────────┘
```

Don't worry about memorizing this architecture yet.

The important idea is:

> **Your application sits on top of Android and uses Android-provided APIs to perform work.**

This is somewhat similar to how you've worked with Java and JDBC.

You don't normally tell PostgreSQL how to physically move bytes around its storage system.

Instead:

```text
Java application
      ↓
JDBC API
      ↓
PostgreSQL driver
      ↓
PostgreSQL
```

Android has a similar idea:

```text
Your Java application
        ↓
Android APIs
        ↓
Android platform
        ↓
Device
```

***

# 4. What is the Android SDK?

SDK means:

> **Software Development Kit**

The Android SDK is the collection of tools, APIs, libraries, build components, and other resources developers use to build Android applications.

You can think of it as the **developer's toolbox for Android**.

For example, it contains things needed to:

* compile Android applications
* communicate with Android devices
* build APKs/app bundles
* use Android APIs
* test applications
* debug applications
* interact with emulators

### Compare it with Java

You have probably seen something like:

```text
JDK
```

The Java JDK gives you tools needed to develop Java programs.

Similarly:

```text
Android SDK
```

provides tools and APIs needed to develop Android applications.

***

# 5. Android Studio

Android Studio is the primary IDE used for Android development.

IDE = **Integrated Development Environment**

You can think of it as:

```text
Android Studio
     │
     ├── Code editor
     ├── Project management
     ├── Gradle integration
     ├── Debugger
     ├── Emulator management
     ├── Android SDK integration
     ├── Logcat
     └── Android development tools
```

This is similar to the role IntelliJ IDEA/Eclipse plays in Java development.

In fact, Android Studio is based on IntelliJ IDEA.

So conceptually:

```text
Java development
    ↓
IntelliJ IDEA / Eclipse

Android development
    ↓
Android Studio
```

***

# 6. Android Studio vs Android SDK

This distinction is important.

They are **not the same thing**.

### Android Studio

The development environment.

```text
Android Studio
= IDE
```

### Android SDK

The Android development tools/APIs.

```text
Android SDK
= Android development toolkit
```

They work together.

For example:

```text
You write code
     ↓
Android Studio
     ↓
uses Android SDK + build tools
     ↓
builds application
     ↓
runs it on emulator/device
```

***

# 7. Where does Java fit?

This is particularly important for **your course**.

Android applications can be developed using different programming technologies.

For this course, we are deliberately using:

> **Java + Android SDK + XML/View system**

Your Java code will contain application logic.

For example, conceptually:

```java
public class MainActivity extends Activity {

    // Java code
}
```

The Android framework provides classes that your Java code can use.

For example:

```java
Activity
View
Context
Intent
RecyclerView
```

etc.

We will learn those later when they appear in the syllabus.

***

# 8. Java is not Android

This distinction is important.

You already know Java.

But:

```text
Java ≠ Android
```

Java is a programming language.

Android is a platform.

Your Java code uses Android's APIs.

Similar to:

```text
Java
  +
JDBC API
  +
PostgreSQL driver
  =
Java application communicating with PostgreSQL
```

In Android:

```text
Java
  +
Android APIs
  +
Android SDK
  =
Android application
```

So Android development will require you to learn **Android concepts**, not relearn programming from zero.

***

# 9. XML's Role

We are also deliberately using the traditional **XML/View-based UI system**.

This means your Android application will commonly have:

```text
Java
+
XML
```

Java handles application behavior.

XML describes many aspects of the UI and resources.

For example, conceptually:

```text
Java
    ↓
"What should happen?"

XML
    ↓
"What does the UI look like?"
```

Later we'll have something like:

```text
MainActivity.java
activity_main.xml
```

where:

```text
MainActivity.java
        ↓
application behavior

activity_main.xml
        ↓
screen layout
```

Don't worry about Activities or layouts yet. **We'll cover them in their dedicated sections.**

***

# 10. Modern Android Development — Our Technology Stack

This is the stack we will use throughout this course:

```text
                    Android Application
                           │
             ┌─────────────┴─────────────┐
             │                           │
           Java                         XML
             │                           │
     Application logic              UI / Resources
             │                           │
             └─────────────┬─────────────┘
                           │
                    Android APIs
                           │
                    Android SDK
                           │
                     Android OS
                           │
                       Hardware
```

For specific parts of the syllabus, we'll use modern replacements where the old technology is obsolete.

Our practical stack will be:

| Area               | Technology                           |
| ------------------ | ------------------------------------ |
| Language           | **Java**                             |
| IDE                | **Android Studio**                   |
| UI                 | **XML + Android Views**              |
| UI components      | **Material Components**              |
| Lists              | **RecyclerView**                     |
| Grid               | **RecyclerView + GridLayoutManager** |
| Local database     | **Room (SQLite underneath)**         |
| Networking         | **Volley**                           |
| Push notifications | **Firebase Cloud Messaging**         |
| Maps               | **Current Google Maps Android SDK**  |
| Build system       | **Gradle**                           |

This is important:

**Modernizing the syllabus does not mean throwing away the concepts.**

For example:

```text
Original syllabus:
ListView
       ↓
Understand Adapter concept
       ↓
Modern implementation:
RecyclerView
```

and:

```text
Original syllabus:
SQLite
       ↓
Understand local relational database
       ↓
Modern implementation:
Room
       ↓
SQLite underneath
```

We'll do this systematically when those sections arrive.

***

# 11. High-Level Android Application Architecture

At this stage, don't worry about every Android component.

Just understand the broad relationship:

```text
┌─────────────────────────────────────┐
│         Your Android App            │
│                                     │
│  Java code                           │
│  XML resources                       │
│  App configuration                   │
│  Images / strings / etc.             │
└─────────────────┬───────────────────┘
                  │
                  ▼
        Android Application APIs
                  │
                  ▼
             Android OS
                  │
                  ▼
              Hardware
```

Later, we will break the application itself into concepts such as:

```text
Activity
Intent
Service
Broadcast Receiver
Content Provider
```

Those are **not today's topic**.

For now, just recognize them as pieces of the Android application model.

***

# 12. A Comparison With Your Spring Boot Knowledge

This should help because you're learning Spring Boot.

In Spring Boot you have something roughly like:

```text
Your Java application
        ↓
Spring Framework
        ↓
JVM
        ↓
Operating System
```

In Android:

```text
Your Java application
        ↓
Android Framework / APIs
        ↓
Android Runtime / Platform
        ↓
Android OS
        ↓
Device hardware
```

The important common idea is:

> **Your application is built on top of a framework/platform that provides services and APIs.**

You don't implement everything yourself.

***

# 13. Our First Android Studio Setup

Now we're going to do something practical.

We're **not creating our actual course project yet**.

The purpose of this exercise is simply to make sure your Android development environment works.

## Step 1 — Open Android Studio

Open:

**Android Studio**

From the welcome screen, you should see an option similar to:

```text
New Project
```

We will use it.

***

## Step 2 — Create a test project

Click:

**New Project**

You should see Android Studio's project templates.

For this first test, choose a basic phone/tablet application template that uses the **Views/XML system**, not Compose.

Depending on your Android Studio version, the exact template name may differ.

Look for something along the lines of:

```text
Empty Views Activity
```

or another basic **Views** template.

### Do NOT choose:

```text
Empty Activity
```

if that template is specifically the Compose version in your Android Studio.

We want:

```text
XML + Views
```

not:

```text
Jetpack Compose
```

***

# 14. Project Configuration

Android Studio will ask for information such as:

```text
Name
Package name
Save location
Language
Minimum SDK
```

For now, use:

```text
Name:
AndroidIntroductionTest
```

For language:

```text
Java
```

This is critical.

If Android Studio gives you:

```text
Kotlin
Java
```

choose:

> **Java**

For the minimum SDK, Android Studio's current recommended/default choice is fine for this test project.

Don't spend time optimizing the minimum SDK yet.

We'll discuss Android versions and SDK levels later when they become relevant.

***

# 15. What Android Studio Creates

After the project opens, don't worry if the project structure looks complicated.

You may see something broadly like:

```text
AndroidIntroductionTest
│
├── app
│   │
│   ├── manifests
│   │
│   ├── java
│   │
│   └── res
│
├── Gradle Scripts
└── ...
```

For now, remember only:

```text
Project
   ↓
contains modules

app module
   ↓
contains the actual Android application
```

We'll study this structure properly later.

***

# 16. Project vs Module

Since this is likely to be unfamiliar, let's establish this now.

### Project

The overall Android Studio workspace.

```text
AndroidIntroductionTest
```

### Module

A distinct part of the project.

For our normal Android application:

```text
AndroidIntroductionTest
        │
        └── app
```

The `app` module is where our Android application lives.

So when I later tell you:

> "Create this file in the app module"

you'll know what I mean.

***

# 17. Run the Test Application

Once Android Studio has finished creating and indexing the project, look for the **Run ▶** button.

You need somewhere to run the application.

There are two common choices:

```text
Physical Android phone
```

or:

```text
Android Emulator
```

For now, use an emulator if one is already available.

If you haven't created an emulator yet, **don't start creating one independently just yet**.

The syllabus has a dedicated topic:

> **Creating a new AVD**

We'll cover that separately.

If Android Studio already provides a working virtual device, use it.

***

# 18. What Should Happen?

When you run the application, Android Studio should:

```text
compile Java code
       ↓
build Android application
       ↓
start/install application
       ↓
launch it on emulator/device
```

You should eventually see a basic Android application screen.

The exact generated UI depends on your Android Studio template/version.

That's okay.

For this exercise, we're testing the **development environment**, not building UI.

***

# 19. What Does "Build" Mean?

You will see this word constantly in Android development.

When you write:

```java
System.out.println("Hello");
```

in a normal Java application, Java source code needs to be compiled.

Android applications similarly go through a build process.

Very roughly:

```text
Java + XML + resources
          ↓
       Gradle
          ↓
    Android build
          ↓
    installable app
```

The Android build system is based on **Gradle**.

We'll study Gradle more when project structure/dependencies become relevant.

For now:

> **Gradle is the build system that Android Studio uses to build your application.**

***

# 20. Your First Practical Task

Don't modify any code yet.

### Task

Create:

```text
AndroidIntroductionTest
```

with:

```text
Language: Java
UI technology: XML / Views
```

Then run it.

### Your job

Tell me:

1. Did Android Studio create the project successfully?
2. Did you find the `app` module?
3. Did the application build successfully?
4. Did it launch on an emulator/device?
5. What screen did you see?
6. If there was an error, paste the **complete error** here.

**Do not continue to the next concept until you've actually run it.**

***

# Section 01 Checkpoint — Before We Move On

After your environment works, you should be able to explain these in your own words:

### Understanding questions

**1.** What is the difference between **Android**, **Android SDK**, and **Android Studio**?

**2.** What is the role of **Java** in the Android application we are building?

**3.** Why are we using **Java + XML Views** rather than Kotlin + Jetpack Compose?

**4.** What is the difference between an Android **project** and the `app` **module**?

**5.** What does Gradle roughly do?

### Prove-it task

Without looking back at this lesson, explain this diagram in your own words:

```text
Java + XML
    ↓
Android APIs
    ↓
Android SDK / build tools
    ↓
Android application
    ↓
Android OS
    ↓
Device
```

You don't need textbook definitions. **Explain what each layer is doing.**

Once you've created and run the test project, send me the result. Then we'll finish the Section 01 checkpoint and only afterward move to the next section.

***
# Footnotes
[^1]: [[What is API (in Android development or in general)]].
