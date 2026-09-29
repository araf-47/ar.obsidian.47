# Section 02 — Android Studio + Emulator/AVD + First Application

We’ll build this section around one simple goal:

**Create a Java + XML Android application in Android Studio, understand what Android Studio generated, run it on an emulator, and understand the role of the main project files.**

We will **not** move into Activities, Intents, databases, RecyclerView, networking, etc. yet. Those belong to later sections.

## 1. What we are learning

By the end of this section, you should be able to explain:

```text
Android Studio
    ↓
Android Project
    ↓
app module
    ↓
Gradle builds the app
    ↓
Android SDK provides Android APIs/tools
    ↓
APK is built
    ↓
Emulator/physical device runs the app
```

And you should recognize the important pieces of a generated project:

```text
MyAndroidApp/
│
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       ├── res/
│   │       └── AndroidManifest.xml
│   │
│   ├── build.gradle(.kts)
│   └── ...
│
├── build.gradle(.kts)
├── settings.gradle(.kts)
└── gradle/
```

Don't worry if that structure looks unfamiliar. We'll create the project and inspect each part rather than memorizing it.

***

# Part 1 — Android Studio

## What is Android Studio?

**Android Studio is the main development environment for Android applications.**

You can think of it somewhat like:

| Technology | Development environment |
| ---------- | ----------------------- |
| Java       | IntelliJ IDEA / Eclipse |
| Web        | VS Code / WebStorm      |
| Android    | Android Studio          |

Android Studio gives you:

* Java code editor
* XML layout editor
* project management
* Gradle integration
* Android SDK management
* emulator management
* debugger
* Logcat
* APK building
* device deployment

So Android Studio isn't Android itself.

It is the **tool you use to develop Android applications**.

***

# Part 2 — Android SDK

## What is the Android SDK?

SDK means:

> **Software Development Kit**

The Android SDK provides the tools and APIs needed to develop Android applications.

For example, your Java Android code may use Android classes such as:

```java
Activity
View
Button
TextView
Intent
```

These are provided by the Android platform/API.

The SDK also contains development tools used to:

* compile applications
* package applications
* communicate with devices
* create/manage emulators
* debug applications

A useful mental model is:

```text
Android Studio
      ↓
uses
      ↓
Android SDK + build tools
      ↓
builds
      ↓
Android application
```

### Don't confuse these

**Android Studio ≠ Android SDK**

Android Studio is the development environment.

The SDK contains Android development APIs and tools.

***

# Part 3 — Emulator vs AVD

These two terms are easy to mix up.

## Emulator

An **Android Emulator** is a program that behaves like an Android device on your computer.

For example:

```text
Your Debian/Windows computer
        │
        └── Android Emulator
                 │
                 └── Android device
```

You can run your application on it without owning a physical Android phone.

***

## AVD

AVD means:

> **Android Virtual Device**

An AVD is the **configuration/definition of the virtual device**.

For example, you might create an AVD configured as:

```text
Device: Pixel 7
Android version: API 35
RAM: ...
Storage: ...
```

Then the Android Emulator uses that configuration to run the virtual device.

So:

```text
AVD
↓
defines the virtual device

Emulator
↓
actually runs the virtual device
```

A simple analogy:

> **AVD = specification of the device**
> **Emulator = software that runs that device**

***

# Part 4 — Your First Android Project

Now we stop talking about theory and create something.

## Step 1 — Open Android Studio

Open **Android Studio**.

At the welcome screen, choose:

**New Project**

You should see Android project templates.

Choose a basic template that creates a **Views/XML-based application**, not a Compose application.

Depending on your Android Studio version, the exact template name/interface may differ. Look for a basic **Views/XML** application template.

### Important

If Android Studio offers:

* Kotlin
* Java

choose:

**Java**

If it offers:

* Jetpack Compose
* Views/XML

choose:

**Views/XML**

We are intentionally using:

```text
Java + XML Views
```

not:

```text
Kotlin + Jetpack Compose
```

***

## Step 2 — Project configuration

You'll see fields such as:

### Name

Use:

```text
AndroidLearning
```

### Package name

You can use:

```text
com.example.androidlearning
```

### Save location

Choose a location where you keep your Android practice projects.

For example:

```text
~/AndroidStudioProjects/AndroidLearning
```

or another location you prefer.

### Language

Select:

```text
Java
```

### Minimum SDK

For now, use the default recommended minimum SDK unless Android Studio requires a choice.

We don't need to optimize the application's Android-version compatibility yet.

***

# Step 3 — Create the project

Click:

**Finish**

Android Studio will now do something important.

It will create the project and run **Gradle** to configure/build it.

The first project creation can take some time because Android Studio may need to download/configure dependencies and build tools.

**Do not start changing files while Gradle is still setting everything up.**

Wait until Android Studio finishes loading/syncing.

***

# Part 5 — What is Gradle?

You'll see files with names such as:

```text
build.gradle
```

or, depending on your Android Studio version:

```text
build.gradle.kts
```

Don't worry about the `.kts` part yet.

## What is Gradle?

Gradle is the **build system** used by Android projects.

Its job includes things like:

```text
Your source code
      ↓
compile
      ↓
resolve dependencies
      ↓
package resources
      ↓
build application
      ↓
APK
```

You can think of it as the system that answers:

> "How do I turn all these project files and dependencies into an Android application?"

***

## Why do we need Gradle?

Suppose your application eventually uses:

```text
Android SDK
Material Components
RecyclerView
Room
Volley
Firebase
Google Maps
```

You don't want to manually download and configure every library.

Gradle helps manage this.

For example, a dependency might eventually be declared something like:

```text
implementation("some-library")
```

Gradle can then obtain and include the required library during the build.

**We will learn dependency management properly later.**

For this section, remember:

> **Gradle is responsible for building and configuring the Android project and managing its dependencies.**

***

# Part 6 — The Project vs the App Module

This is one of the most important concepts in Android Studio.

When you create:

```text
AndroidLearning
```

you created an **Android project**.

Inside that project is an:

```text
app
```

module.

Initially, think of it like this:

```text
AndroidLearning       ← Project
│
└── app                ← Application module
```

## What is a module?

A module is a distinct part of an Android project that can be built.

For our beginner application, the important module is:

```text
app
```

The `app` module contains the actual Android application we're building.

So when I later tell you:

> "Create this file inside the app module"

I'm referring to:

```text
AndroidLearning
└── app
```

This distinction will become particularly important when projects become larger.

***

# Part 7 — Let's inspect the generated project

In Android Studio, look at the **Project** panel.

You may initially see a simplified Android view.

For learning the actual structure, change the project panel from:

```text
Android
```

to:

```text
Project
```

The exact UI may vary slightly between Android Studio versions.

Now you should be able to see something closer to the actual filesystem structure.

Look for:

```text
AndroidLearning
└── app
```

Expand it.

Then look for:

```text
app
└── src
    └── main
```

Inside `main`, you should find things corresponding to:

```text
java
res
AndroidManifest.xml
```

The exact generated names may differ slightly depending on the template and current Android Studio version.

***

# Part 8 — The `src/main` directory

This is where the main application source lives.

Conceptually:

```text
app
└── src
    └── main
        ├── java
        ├── res
        └── AndroidManifest.xml
```

These three are extremely important.

***

## `java`

This is where our Java source code lives.

For example:

```text
app
└── src
    └── main
        └── java
            └── com.example.androidlearning
                └── MainActivity.java
```

This is where Android Java classes such as our Activities will live.

We aren't studying Activities deeply yet. For now, just recognize where the Java code goes.

***

# Part 9 — `res`

`res` means:

> **resources**

Android separates many application resources from Java code.

You'll see directories such as:

```text
res/
├── drawable/
├── mipmap/
├── values/
└── layout/
```

The exact generated directories can vary.

The important one for us right now is:

```text
layout/
```

This is where XML layouts live.

For example:

```text
res
└── layout
    └── activity_main.xml
```

That XML file describes part of the application's user interface.

Conceptually:

```text
MainActivity.java
       +
activity_main.xml
       ↓
Android application screen
```

We'll learn exactly how Java and XML interact in a later section when we study Android UI/Activities.

***

# Part 10 — `AndroidManifest.xml`

You'll also see:

```text
AndroidManifest.xml
```

The manifest provides important information about the application to Android.

It can describe things such as:

* application configuration
* application components
* permissions
* app entry information
* other metadata

For example, Android needs to know what components exist in an application.

Don't try to memorize the manifest syntax yet.

Just establish this mental model:

```text
AndroidManifest.xml
        ↓
Information/configuration Android needs
        about the application
```

We'll return to it when the relevant Android concepts appear.

***

# Part 11 — First important architecture picture

At this point, you should have this mental model:

```text
AndroidLearning/
│
├── app/
│   │
│   └── src/
│       │
│       └── main/
│           │
│           ├── java/
│           │      └── Java source code
│           │
│           ├── res/
│           │      └── XML/images/other resources
│           │
│           └── AndroidManifest.xml
│
├── Gradle configuration
└── other project files
```

Don't memorize every Gradle file yet.

Understand the **purpose** of the major areas.

***

# Part 12 — Run the application

Now let's actually run the generated application.

We need an Android device.

You have two options:

```text
Physical Android phone
        OR
Android Emulator
```

For this exercise, we'll use the emulator.

***

## Step 1 — Open Device Manager

In Android Studio, find:

**Device Manager**

Depending on the Android Studio version, it may be available from the toolbar or under a menu such as:

**Tools → Device Manager**

Open it.

***

## Step 2 — Create an AVD

Choose:

**Create Virtual Device**

You'll be asked to select a hardware profile.

Choose something like:

```text
Pixel
```

You don't need to obsess over which Pixel model we use.

Select a reasonable phone profile and continue.

***

## Step 3 — Select an Android system image

You'll then choose an Android system image.

You'll see Android versions/API levels.

Choose a recommended/current stable image that Android Studio offers for your environment.

If the image isn't installed, Android Studio may offer:

**Download**

Allow it to download and install.

***

## Step 4 — Finish AVD creation

Give the virtual device its default name or choose something meaningful, for example:

```text
Pixel_API_35
```

Finish the setup.

You should now see the AVD in Device Manager.

***

# Part 13 — Start the emulator

Start the AVD.

The first boot can take some time.

Eventually you should see something resembling an Android phone on your desktop.

That's the **Android Emulator** running your **AVD configuration**.

Again:

```text
AVD
= configuration

Emulator
= program running that virtual Android device
```

***

# Part 14 — Run our application

With the emulator running, return to Android Studio.

At the top of Android Studio, you should have a device selector.

Select your emulator.

Then press:

**Run ▶**

Android Studio will:

```text
Java/XML project
      ↓
Gradle build
      ↓
Android application package
      ↓
install application
      ↓
emulator
      ↓
application starts
```

You should eventually see the generated application running on the emulator.

***

# Your first practical checkpoint

**Stop here after running it.**

Do not move to the next part until you've actually tested it.

I want you to report back with:

```text
1. Android Studio opened successfully: YES/NO

2. Project created successfully: YES/NO

3. Java selected: YES/NO

4. XML/View-based project created: YES/NO

5. Gradle finished successfully: YES/NO

6. AVD created: YES/NO

7. Emulator started: YES/NO

8. Application ran: YES/NO

9. What appeared on the emulator:
   __________________________
```

If something fails, **paste the exact error/message or show me what you see**. Don't try to fix it yourself yet.

***

## Before continuing: 5 understanding questions

Don't look anything up; answer from your current understanding.

**1.** What is the difference between **Android Studio** and the **Android SDK**?

**2.** What is the difference between an **AVD** and the **Android Emulator**?

**3.** What is the purpose of the `app` module?

**4.** What is Gradle responsible for?

**5.** What is the general purpose of these three?

```text
java/
res/
AndroidManifest.xml
```

Once you run the application and answer these, we'll continue with the **anatomy of the generated Java Android project**, examining the actual files one by one rather than memorizing a generic project tree.

### My reply - ↪️ - I will answer  them later.

Sure. We’ll continue, and you can answer the checkpoint questions later. I’ll still treat the actual emulator run as unconfirmed until you tell me what happened.

# Part 15 — Anatomy of the Generated Java Android Project

Now we're going to look at the project you just created and understand **why each important file exists**.

Don't worry about every file Android Studio generates. We'll focus on the ones that matter for understanding Android development.

Your project should conceptually look something like:

```text
AndroidLearning/
│
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       ├── res/
│   │       └── AndroidManifest.xml
│   │
│   ├── build.gradle(.kts)
│   └── ...
│
├── build.gradle(.kts)
├── settings.gradle(.kts)
└── gradle/
```

There may be additional files and folders. That's normal.

***

# 16 — The `app` module

Let's start from:

```text
AndroidLearning/
└── app/
```

This is the most important module for our application.

Think of:

```text
AndroidLearning
```

as the **whole project**, while:

```text
app
```

is the **Android application module we're developing**.

For our course, most of our work will happen inside:

```text
app/src/main/
```

Eventually we'll create things like:

```text
Java classes
XML layouts
drawables
strings
database classes
adapters
services
etc.
```

inside this module.

***

# 17 — `app/src/main`

Open:

```text
app
└── src
    └── main
```

`main` is essentially the main source set for the application.

Inside it you'll encounter:

```text
main/
├── java/
├── res/
└── AndroidManifest.xml
```

Let's examine these individually.

***

# 18 — `java/`

Open:

```text
app
└── src
    └── main
        └── java
```

You should find your package.

Something similar to:

```text
com.example.androidlearning
```

Inside it you'll find the generated Java class.

Probably something similar to:

```text
MainActivity.java
```

The exact name depends on the project template you selected.

***

## Why is it inside a package?

This is normal Java structure.

For example:

```java
package com.example.androidlearning;
```

The package gives the class its namespace.

This is the same basic Java concept you've encountered outside Android.

For example, in a Spring project you might have:

```text
com.lord.LandLord.Controller
```

Android isn't inventing a new concept here.

It's using Java's package system.

So:

```text
Android
    ↓
Java
    ↓
packages/classes
```

***

# 19 — `MainActivity.java`

You'll probably see something like:

```java
public class MainActivity extends AppCompatActivity {
    ...
}
```

Don't worry about `Activity` yet.

**Activities are a later section of the syllabus.**

For now, understand only this:

> `MainActivity.java` is Java code belonging to the application's initial screen/component.

You may see code similar to:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
}
```

There are several new concepts here:

```text
onCreate()
Bundle
setContentView()
R.layout.activity_main
```

We are **not going to fully study these yet**.

Why?

Because they belong to the Android Activity/UI concepts that come later.

For this section, just notice the relationship:

```text
MainActivity.java
        ↓
references
        ↓
activity_main.xml
```

We'll properly explain that relationship when we reach the Activity section.

***

# 20 — `res/` — Android resources

Now open:

```text
app/src/main/res/
```

You'll find various resource directories.

Common examples include:

```text
drawable/
mipmap/
values/
layout/
```

depending on the project template.

The key idea is:

> `res` contains resources used by the Android application.

Resources are things that aren't simply Java classes.

For example:

```text
XML layouts
images
strings
colors
dimensions
icons
```

***

# 21 — `layout/`

If your project contains:

```text
res/
└── layout/
```

open it.

You may see:

```text
activity_main.xml
```

This is an XML layout file.

For example, it might contain something conceptually like:

```xml
<LinearLayout
    ...>

    <TextView
        ...
        android:text="Hello World!" />

</LinearLayout>
```

The exact generated XML may differ in your Android Studio version/template.

The important idea is:

```text
XML
↓
describes UI structure
```

This is somewhat comparable to HTML.

You already know HTML, so this connection is useful:

```text
HTML
↓
describes web UI structure

Android XML
↓
describes Android View hierarchy
```

But don't conclude that Android XML **is HTML**.

It isn't.

They're just both markup-based ways of describing UI structure.

***

# 22 — `values/`

You may see files such as:

```text
res/
└── values/
    ├── strings.xml
    ├── colors.xml
    └── themes.xml
```

Again, the exact files depend on the template.

For example:

### `strings.xml`

This can contain text resources:

```xml
<resources>
    <string name="app_name">AndroidLearning</string>
</resources>
```

Instead of hardcoding the same text everywhere, Android can reference a resource.

You'll encounter this idea repeatedly throughout Android development.

***

# 23 — Why does Android have resources?

This is an important design idea.

Imagine an application has:

```text
100 different screens
```

and you hardcode every piece of text, color, dimension, image, etc. directly into Java code.

That quickly becomes difficult to maintain.

Android therefore has a resource system.

Conceptually:

```text
Java code
   │
   ├── application logic
   │
   └── references resources

res/
   ├── layouts
   ├── strings
   ├── images
   ├── colors
   └── etc.
```

This separation becomes particularly useful when dealing with different screen sizes, languages, themes, and device configurations.

***

# 24 — `AndroidManifest.xml`

Now open:

```text
app/src/main/AndroidManifest.xml
```

This file is important because Android needs information about the application before it can run it.

For example, the manifest can declare:

* application components
* permissions
* application-level configuration
* component metadata

You'll eventually encounter declarations such as Activities, Services, and Broadcast Receivers.

Those are later syllabus topics.

So don't try to master them now.

For this section, remember:

> **The manifest tells Android important information about the application and its components.**

***

# 25 — Where does the application actually start?

You might naturally ask:

> "If `MainActivity.java` exists, how does Android know to launch it?"

Excellent question.

Part of the answer involves the **AndroidManifest.xml** and the application's declared entry component.

Modern Android project templates configure the starting component for you.

You don't need to manually construct this yet.

This is exactly why I don't want you memorizing the generated code before learning Activities.

When we reach:

**Section — Android Activity**

we'll break this relationship down properly.

For now:

```text
Android system
      ↓
knows about application
      ↓
Manifest
      ↓
application's components
      ↓
initial component
      ↓
screen appears
```

***

# 26 — Gradle files

Now let's move one level higher.

You'll find Gradle configuration associated with:

```text
project
```

and:

```text
app module
```

This distinction is important.

Conceptually:

```text
Project-level Gradle configuration
        ↓
whole project

App-level Gradle configuration
        ↓
app module
```

Modern Android Studio projects may use:

```text
build.gradle.kts
```

instead of:

```text
build.gradle
```

The `.kts` version uses **Kotlin DSL** for Gradle configuration.

### Important distinction

This does **NOT** mean your Android application is written in Kotlin.

You can have:

```text
Android application code → Java
Gradle configuration → Kotlin DSL
```

Those are separate things.

Your Java requirement applies to the **Android application implementation**.

We are not switching your application to Kotlin.

***

# 27 — What does the app Gradle file control?

The app-level Gradle configuration contains information related to building the application.

Among other things, it can specify:

```text
application ID
compile SDK
minimum SDK
target SDK
version information
dependencies
build configuration
```

For example, conceptually:

```text
compile SDK
    ↓
Android API level used when compiling

minimum SDK
    ↓
oldest Android version your app supports

dependencies
    ↓
external libraries your app uses
```

We'll learn these more carefully as they become necessary.

***

# 28 — SDK versions: an important distinction

You will encounter terms such as:

```text
compileSdk
minSdk
targetSdk
```

Don't memorize them blindly.

For now:

### `compileSdk`

The Android API level your application is compiled against.

### `minSdk`

The oldest Android version your application is intended to support.

### `targetSdk`

The Android API level your application is designed/tested to target, which also affects platform behavior and compatibility expectations.

So conceptually:

```text
compileSdk
    ↓
"What Android API do I compile against?"

minSdk
    ↓
"What's the oldest Android version I support?"

targetSdk
    ↓
"What Android behavior/version am I targeting?"
```

We'll revisit these when they become relevant.

***

# 29 — `settings.gradle(.kts)`

You'll also see something like:

```text
settings.gradle.kts
```

This is associated with the **project structure**, including which modules belong to the project.

For our simple project, you'll commonly see the `app` module included.

Conceptually:

```text
AndroidLearning project
        ↓
settings
        ↓
app module
```

Again, you don't need to memorize the syntax yet.

***

# 30 — The complete mental model

Now put everything together.

```text
AndroidLearning
│
├── Project configuration
│
├── Gradle
│
├── app
│   │
│   ├── build configuration
│   │
│   └── src/main
│       │
│       ├── java
│       │   └── Java application code
│       │
│       ├── res
│       │   ├── layout
│       │   │   └── XML UI
│       │   ├── values
│       │   └── other resources
│       │
│       └── AndroidManifest.xml
│
└── other project/build files
```

And when you press **Run**:

```text
Java + XML + resources
          ↓
        Gradle
          ↓
      Android build
          ↓
       APK/app
          ↓
Android Emulator / Phone
          ↓
       Application
```

That's the core of this section.

***

# 31 — A very important comparison with Spring Boot

Since you're learning Spring Boot, here's a useful comparison.

In Spring Boot, you might have:

```text
Spring Boot project
│
├── src/main/java
│   └── Java classes
│
├── src/main/resources
│   └── configuration/resources
│
└── pom.xml / build.gradle
```

Android has a similar overall idea:

```text
Android project
│
├── app/src/main/java
│   └── Java classes
│
├── app/src/main/res
│   └── Android resources
│
├── AndroidManifest.xml
│
└── Gradle configuration
```

So you already have a useful mental model:

**Android is not abandoning normal Java project organization.**

It adds Android-specific pieces around the Java application.

***

# 32 — Your first "prove it" exercise

Since you asked to continue without answering the previous questions, let's make the practical part more important.

Open your actual Android project and locate these **five things**:

### A

Your Java source directory:

```text
app/src/main/java/
```

### B

Your generated Java class:

```text
MainActivity.java
```

or whatever your generated Activity is called.

### C

Your resources directory:

```text
app/src/main/res/
```

### D

Your XML layout:

```text
app/src/main/res/layout/
```

if your selected template generated one.

### E

Your manifest:

```text
app/src/main/AndroidManifest.xml
```

Then open the generated Java class and XML layout **side by side**.

Don't modify anything yet.

Try to identify:

```text
Java code
     ↓
MainActivity.java

UI description
     ↓
activity_main.xml
```

***

# One important warning

If your generated project **doesn't look exactly like these examples**, don't immediately assume something is wrong.

Android Studio templates change over time.

For example, you may see:

```text
build.gradle.kts
```

instead of:

```text
build.gradle
```

or slightly different generated Java/XML files.

**That's normal.**

If your project is Java + XML/View-based and builds successfully, we'll work with **your actual generated project**, rather than forcing it to look like an older tutorial.

***

## Next step

Before we modify anything, I want you to open:

```text
MainActivity.java
```

and the generated XML layout file.

**Paste both files here** (or at least their contents).

Then I'll walk through **your exact generated code line-by-line**, including why Android Studio created each part, without jumping ahead into the full Activity section.

### ↪️ Paste yours here. Then continue reading below 👇🏻

Perfect. This is exactly what I wanted to see because now we can learn from **your actual generated project**, rather than a generic older Android tutorial.

Your project is using:

* **Java**
* **XML Views**
* **AppCompat**
* **ConstraintLayout**
* **Edge-to-edge UI**
* modern AndroidX APIs

So your setup matches the direction of this course.

# 1. First, see the relationship

You have two files:

```text
MainActivity.java
        │
        │ references
        ↓
activity_main.xml
```

The Java file contains application behavior/code.

The XML file describes the UI structure.

The connection is this line:

```java
setContentView(R.layout.activity_main);
```

We'll unpack that carefully.

***

# 2. `MainActivity.java`

Let's go from the top.

```java
package com.example.androidlearning;
```

This is standard Java.

It tells Java that `MainActivity` belongs to:

```text
com.example.androidlearning
```

You already know the basic idea from Java packages and from your Spring projects.

For example, you've seen packages such as:

```text
com.lord.LandLord.Controller
```

Android uses the same Java package system.

***

# 3. Imports

You have:

```java
import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
```

These are classes provided by Android/the AndroidX libraries.

You don't need to memorize these imports.

But notice something important:

```java
import ...
```

is still ordinary Java.

Android development doesn't replace Java.

It gives you Android-specific classes that your Java code uses.

***

# 4. The class

You have:

```java
public class MainActivity extends AppCompatActivity {
```

There are two things here.

### `class MainActivity`

That's ordinary Java.

You're defining a class called:

```text
MainActivity
```

### `extends AppCompatActivity`

This means inheritance.

In simplified form:

```text
AppCompatActivity
       ↑
       │ extends
       │
MainActivity
```

Your `MainActivity` gets functionality from `AppCompatActivity`.

You already know what inheritance means from Java, so don't overthink this part yet.

### But what is an Activity?

That's an Android concept.

For **this section**, remember only:

> An Activity is an Android application component associated with a user-facing screen.

We will properly study Activities in the dedicated Activity section.

***

# 5. `onCreate()`

You have:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
```

This is one of the most important pieces of generated Android code.

But we're going to carefully avoid going too deep into the Activity lifecycle yet.

For now:

```text
onCreate()
```

is a method Android calls when this Activity is being created.

The generated project puts initial setup code here.

***

# 6. `@Override`

You already know this from Java.

```java
@Override
```

means:

> This class is providing its own implementation of a method inherited from its parent class.

So conceptually:

```text
AppCompatActivity
       │
       └── has onCreate()
              ↓
       MainActivity
              │
              └── overrides onCreate()
```

That's standard Java inheritance + method overriding.

***

# 7. `Bundle savedInstanceState`

You have:

```java
Bundle savedInstanceState
```

`Bundle` is an Android class used for passing/storing a collection of key-value data.

For example, conceptually:

```text
key → value
```

like:

```text
"userName" → "Araf"
"score"    → 50
```

You don't need to study `Bundle` deeply right now.

For this section, recognize:

```java
Bundle savedInstanceState
```

as information Android can provide when creating the Activity.

We'll return to it when lifecycle/state becomes relevant.

***

# 8. `super.onCreate(...)`

You have:

```java
super.onCreate(savedInstanceState);
```

This is another piece of ordinary Java.

`super` refers to the parent class.

So you're essentially saying:

> "Run the parent class's `onCreate()` implementation too."

Conceptually:

```text
MainActivity.onCreate()
        │
        ├── parent initialization
        │
        └── MainActivity initialization
```

Again, this is Java inheritance.

***

# 9. `EdgeToEdge.enable(this)`

Your generated project contains:

```java
EdgeToEdge.enable(this);
```

This configures the application for **edge-to-edge display**, allowing app content to extend into areas near system bars.

This is part of modern Android UI behavior.

You don't need to master edge-to-edge yet.

The important thing is that your Android Studio template generated this because current Android UI conventions are different from old tutorials.

This is one reason we should **not blindly copy old Android tutorials**.

***

# 10. The most important line for today

Now:

```java
setContentView(R.layout.activity_main);
```

This line is extremely important.

Let's break it apart.

### `setContentView(...)`

You're telling the Activity:

> "Use this layout as the content of this screen."

And:

```java
R.layout.activity_main
```

refers to:

```text
res/layout/activity_main.xml
```

So:

```text
activity_main.xml
        ↓
R.layout.activity_main
        ↓
setContentView(...)
        ↓
MainActivity displays that layout
```

This is the fundamental relationship between your Java code and XML layout.

***

# 11. What is `R`?

This may initially look strange:

```java
R.layout.activity_main
```

What is `R`?

Android generates a class called:

```text
R
```

that provides references to your application's resources.

For example:

```text
res/layout/activity_main.xml
```

becomes accessible through something conceptually like:

```java
R.layout.activity_main
```

Similarly, your XML contains:

```xml
android:id="@+id/main"
```

which allows Java to refer to that resource as:

```java
R.id.main
```

So think:

```text
res/
   ↓
Android resource system
   ↓
R
   ↓
Java can reference resources
```

This is an **Android-specific mechanism** built around your resources.

***

# 12. Now look at your XML

You have:

```xml
<androidx.constraintlayout.widget.ConstraintLayout
```

This is your root UI element.

It is a `ConstraintLayout`.

Think of it as a container that can hold other UI elements.

Inside it you have:

```xml
<TextView
```

So your structure is:

```text
ConstraintLayout
    │
    └── TextView
```

This is called a **View hierarchy**.

Don't worry about the full View system yet. We'll learn it properly in the UI section.

***

# 13. `TextView`

You have:

```xml
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Hello World!"
```

A `TextView` displays text.

So this:

```xml
android:text="Hello World!"
```

is responsible for the visible:

```text
Hello World!
```

on the screen.

You can think of it somewhat like an HTML element:

```html
<p>Hello World!</p>
```

But remember:

**TextView is an Android View, not an HTML element.**

***

# 14. `layout_width` and `layout_height`

You have:

```xml
android:layout_width="wrap_content"
android:layout_height="wrap_content"
```

`wrap_content` basically means:

> Make the View large enough to contain its content.

Since your TextView contains:

```text
Hello World!
```

it only needs enough space to display that text.

You'll encounter another important value later:

```xml
match_parent
```

which means the View attempts to occupy the available space from its parent.

Don't worry about mastering layouts yet.

***

# 15. The `id`

Your root layout has:

```xml
android:id="@+id/main"
```

This creates an ID called:

```text
main
```

Android then makes it accessible through:

```java
R.id.main
```

And your Java code uses exactly that:

```java
findViewById(R.id.main)
```

So we now have another connection:

```text
XML:

android:id="@+id/main"
          ↓
Java:

R.id.main
```

This is a very important Android concept.

***

# 16. Why does `findViewById()` appear?

Your Java contains:

```java
findViewById(R.id.main)
```

This means, roughly:

> "Find the View in the current layout that has this ID."

The XML says:

```xml
android:id="@+id/main"
```

and Java searches for:

```java
R.id.main
```

So:

```text
XML
│
├── View exists
└── ID = main
       ↓
Java
│
└── findViewById(R.id.main)
       ↓
gets that View
```

We'll use this concept extensively when working with UI.

***

# 17. What is this giant `ViewCompat` code?

Your generated project contains:

```java
ViewCompat.setOnApplyWindowInsetsListener(
    findViewById(R.id.main),
    (v, insets) -> {
        Insets systemBars =
            insets.getInsets(
                WindowInsetsCompat.Type.systemBars()
            );

        v.setPadding(
            systemBars.left,
            systemBars.top,
            systemBars.right,
            systemBars.bottom
        );

        return insets;
    }
);
```

Don't panic.

This looks much more complicated than the "Hello World" application actually is.

Its purpose is related to **window/system-bar insets** and ensuring your content gets appropriate padding when the app is displayed edge-to-edge.

The important pieces for **this section** are:

```text
EdgeToEdge
ViewCompat
WindowInsetsCompat
Insets
```

These are modern Android UI infrastructure.

You don't need to master them now.

***

# 18. One Java concept hiding inside it

You have:

```java
(v, insets) -> {
    ...
}
```

That's a **lambda expression**.

It's Java syntax for providing behavior to something expecting a functional interface/callback.

Conceptually:

```text
something happens
      ↓
Android calls your callback
      ↓
your lambda runs
```

You've probably encountered callbacks/events in JavaScript or Angular.

For example, conceptually:

```text
event happens
    ↓
callback executes
```

Same general programming idea.

We will use Java callbacks/listeners frequently in Android.

***

# 19. Your actual application structure

Now we can accurately describe what you created.

```text
AndroidLearning
│
└── app
    │
    └── src
        │
        └── main
            │
            ├── java
            │   │
            │   └── com.example.androidlearning
            │       │
            │       └── MainActivity.java
            │
            ├── res
            │   │
            │   └── layout
            │       │
            │       └── activity_main.xml
            │
            └── AndroidManifest.xml
```

And the important relationship is:

```text
MainActivity.java
       │
       │ setContentView()
       ↓
activity_main.xml
       │
       ↓
ConstraintLayout
       │
       └── TextView
```

***

# 20. Why Android Studio generated all this

You might wonder:

> "Why didn't Android Studio just create one Java file?"

Because Android applications aren't just Java classes.

An Android application consists of multiple kinds of resources and configuration:

```text
Java
+
XML
+
resources
+
manifest
+
Gradle/build configuration
+
Android SDK
```

Gradle combines/builds these pieces into an Android application that can be installed and executed.

This is the important mental model.

***

# 21. Don't memorize the project tree

I don't want you memorizing:

```text
app/src/main/res/...
```

just because I told you to.

Instead, remember the **roles**:

```text
JAVA
↓
application code

XML/resources
↓
UI and other resources

MANIFEST
↓
information about the application/components

GRADLE
↓
build/configuration/dependencies

SDK
↓
Android APIs + development tools

EMULATOR
↓
runs a virtual Android device
```

If you understand those relationships, the folder structure becomes much easier.

***

# One small practical exercise

Let's make one **very small change** to prove that you understand which file controls what.

Open:

```text
app
└── src
    └── main
        └── res
            └── layout
                └── activity_main.xml
```

Find:

```xml
android:text="Hello World!"
```

Change it to:

```xml
android:text="My First Java Android App"
```

**Do not modify `MainActivity.java`.**

Run the application again.

You should see:

```text
My First Java Android App
```

instead of:

```text
Hello World!
```

### What this proves

You changed:

```text
XML
```

and the displayed UI changed.

That gives us our first concrete distinction:

```text
MainActivity.java
→ Java/application behavior

activity_main.xml
→ UI structure/content
```

Run it and tell me what appears on the emulator. Then we'll continue with the remaining Section 02 concepts.
