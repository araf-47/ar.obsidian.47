# Section 03: Anatomy of an Android Application + Components

We'll go step by step. This first part covers the big idea and gets a project in front of you. The exercise at the end is small, and we only continue once you report back.

***

## 1. The big idea: you don't start your app, Android does

I'll drop the servlet and Spring comparison and build this from plain Java instead.

### Start with what you already know

A normal Java program looks like this:

```java
public class Hello {
    public static void main(String[] args) {
        Screen screen = new Screen();   // YOU create the object
        screen.show();                  // YOU decide when it runs
    }
}
```

There's one entry point, `main`. Your code starts first, creates what it needs, and calls things in the order you choose. **You are in control.**

***

### Why that can't work on a phone

Think about what a phone is actually doing at any moment:

- Dozens of apps are installed, but memory is limited.
- You're in your app, and a phone call arrives.
- You press Home, and your app disappears from the screen.
- You rotate the phone.
- Battery gets low.
- Another app wants to open your app's screen (for example, "share this photo to TaskNest").

If every app ran its own `main()` and did whatever it wanted, the phone would crash or freeze. So someone has to be in charge of **starting, pausing, and shutting down apps**. That someone is the **Android operating system**.

So Android **reverses the control**:

> **Plain Java:** your code creates objects and calls them.  
> **Android:** the OS creates your objects and calls them, when it decides the moment is right.

You'll hear this called _"Don't call us, we'll call you."_

***

### An everyday picture

Imagine a company with a **reception desk**.

- The **reception desk** is the **Android OS**. It's the only one who lets people in and sends them to the right place.
- Each **department** (billing, support, shipping) is a **component** of your app: a screen, a background job, and so on.
- The **company directory** hanging at reception is the **`AndroidManifest.xml`**. It lists which departments exist. If a department isn't in the directory, reception says "we have no such department."
- A **visitor's request** ("I'd like to talk to billing") is an **Intent**.

You never walk into the billing department and start their day yourself. The desk decides when a department starts working, and when it goes home.

***

### What this looks like in real code

Here is the class Android Studio generated for you (`MainActivity.java`). Look for what's _missing_:

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

- **There is no `main()` method** anywhere in your app.
- **You never write `new MainActivity()`.** Android creates it.
- `onCreate(...)` is a method you **override**, but you never call it yourself. Android calls it when the screen is being born. It's Android saying "you now exist, set yourself up."
- `extends AppCompatActivity` is what makes this class an _Activity_, meaning something the OS knows how to manage. (An **Activity** = one screen. We go deeper in Section 06.)

So your job changes from "write the program flow" to "**write the reactions**": fill in the methods that Android will call at the right moments.

***

### Summary in one line each

|Term|Plain meaning|
|---|---|
|**Android OS**|The manager. Starts, pauses and kills your app's parts.|
|**Component**|A part of your app that the OS can start (screen, background job, and so on).|
|**`AndroidManifest.xml`**|The directory: the list of components your app has.|
|**Intent**|A request: "start this part" or "someone handle this."|

***

### Quick check

Format is question, options, then the answer:

```
Q1. Why doesn't an Android app have its own main() method that runs everything?

    A) Java doesn't allow main() on phones  
    B) The OS must control when each part of the app starts, pauses, and stops  
    C) Android apps only have one screen, so no entry point is needed  
    D) main() is only for desktop apps in a different language

Correct answer: B

Q2. Who creates the MainActivity object?

    A) You, with new MainActivity()  
    B) The manifest file  
    C) The Android OS  
    D) The Gradle build tool

Correct answer: C
```

***

## 2. The components (a first look only)

There are four component types. Each has its own section later, so today is only orientation:

- **Activity** is one screen the user interacts with. We go deep in Section 06.
- **Service** is work that runs without a screen. Section 09.
- **Broadcast Receiver** reacts to system or app-wide announcements (battery low, boot completed). Section 09.
- **Content Provider** shares data between apps through a standard interface. Section 10.

The glue is the **Intent**, a message object saying "I want something done." An Intent can say "open this screen," "start this service," or "someone should handle this." We'll use it properly in Section 06.

Also, **Resources** (layouts, strings, images, colors) are everything in your app that isn't Java code. Android keeps them separate from code on purpose, and you'll see why in the exercise.

***

## 3. Practical Step 1: create the project

We'll use **one project through the whole course**, a small task-tracking app called **TaskNest**.

1. Open **Android Studio** → **New Project**.
2. Pick the template **Empty Views Activity**. Be careful to avoid "Empty Activity" if it shows a Compose icon, because we deliberately use XML Views, not Compose.
3. Fill in:
   - **Name:** `TaskNest`
   - **Package name:** `com.afar.tasknest`
   - **Language:** **Java**
   - **Minimum SDK:** API 24 (or whatever default Studio suggests)
   - **Build configuration language:** Groovy DSL if offered
4. Click **Finish** and wait for **Gradle sync** to complete (progress bar at the bottom). The first sync can take a few minutes.

Two words to know already:
- **Project** is the whole thing you just created (the top-level folder).
- **Module** is a buildable unit inside the project. Yours is named **`app`**, and nearly all your code lives there.

***

## 4. Practical Step 2: read the manifest

In the left **Project** panel, switch the dropdown at the top to **Android** view, then open:

`app` → `manifests` → **`AndroidManifest.xml`**

(On disk this is `app/src/main/AndroidManifest.xml`.)

It should look roughly like this. Don't worry about tiny differences between Studio versions:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.TaskNest"
        tools:targetApi="31">

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>
</manifest>
```

**What each important part means**

- `<manifest>` is the root. It describes the app to the OS *before any of your code runs*.
- `<application>` appears **once per app** and holds app-wide settings (icon, name, theme) plus all your components.
- `<activity android:name=".MainActivity">` **registers** your `MainActivity` class (the leading `.` means "in this app's package," so `com.afar.tasknest.MainActivity`). An Activity that isn't declared here can't be launched, and Android will crash with an error.
- `<intent-filter>` with `MAIN` + `LAUNCHER` says "this is the front door: show this Activity as the app icon on the home screen."
- `android:exported="true"` means components outside your app (here, the launcher) are allowed to start this Activity. Without it, the icon tap would fail.
- `@string/app_name` and `@mipmap/ic_launcher` are **resource references**. The `@` means "look this up in the `res` folder" instead of hardcoding a value.

Notice the manifest is the *only* place that lists which components exist. It's your `web.xml`.

***

## 5. Exercise (run and observe)

**Part A. Change a resource:**

1. Open `app` → `res` → `values` → **`strings.xml`**.
2. Find the line `<string name="app_name">TaskNest</string>`.
3. Change the value to `TaskNest Dev`.

**Part B. Run it:**

1. Start an emulator (**Device Manager** → pick a device → ▶). If you have none, create one via **Create Device**.
2. Click the green **Run** ▶ button with `app` selected.
3. Look at the top of the app screen, then close the app and check its name in the emulator's home/app drawer.

**What success looks like:** the name `TaskNest Dev` appears in both places, and you changed it *without touching any Java or the manifest*. That's the point of resources.

**Common errors:**
- *Gradle sync failed*: usually a network or JDK issue. Paste the error to me.
- *"No device selected"*: the emulator isn't running yet.
- *Blank screen or template mismatch*: you likely picked a Compose template. Recreate with **Empty Views Activity**.

***

## 6. Report back with

1. What did you see when you ran it (did the name change in both places)?
2. **Prediction question (answer before trying anything):** if you deleted the entire `<activity>...</activity>` block from the manifest, what do you think would happen when you run the app, and why?

Once you reply, we'll test your prediction for real, then move on to `MainActivity.java`, the `res` folder structure, and the lifecycle.

#### After my answer : 👇

# Section 03: Testing Your Prediction

**1. The name change:** the launcher label changed, which proves the point. You edited one line in `strings.xml`, and the manifest picked it up through `@string/app_name` without touching any Java.

One correction to my earlier instructions: newer Empty Views Activity templates often use a theme with **no title bar**, so you may not have seen the name at the top of the screen. That's normal, not a mistake on your side.

***

## 2. Your prediction

You're close on the idea (the manifest controls what Android recognizes), but one part needs adjusting:

- **Not quite:** the `app` module and project won't disappear. The manifest doesn't define your project. Gradle and Android Studio still see all your files.
- **Right in spirit:** Android would no longer recognize `MainActivity` as a component of your app. The class still exists in your code, but the OS's "directory" no longer lists it.

I won't tell you the exact result, because you can observe it directly.

***

## 3. Experiment: break it on purpose

We'll comment out the block instead of deleting it, so restoring it is easy.

1. Open `AndroidManifest.xml`.
2. Wrap the whole `<activity>...</activity>` block in an XML comment:

```xml
<!--
<activity
    android:name=".MainActivity"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
-->
```

3. Click the green **Run** ▶ button.
4. Watch the **Run** panel at the bottom of Android Studio, then look at the emulator.

**Common thing you might see:** a warning or error such as *"Default Activity not found"* or *"No activity found."*

***

## 4. Report back with

1. Did the build succeed? What did the **Run** panel say (paste the exact message)?
2. Did the app icon appear in the emulator's app drawer?
3. **Why do you think that happened?** Use the words "intent-filter" or "LAUNCHER" in your explanation.

When you're done, **remove the comment markers** so the manifest is back to normal.

***

## 5. Quick check

```
Q3. What does the leading dot in android:name=".MainActivity" mean?

    A) The class is hidden from other apps
    B) The class is inside the app's own package (com.afar.tasknest)
    C) The class is a Java interface
    D) The class is loaded from the internet

Correct answer: B
```

Once you report the result, we'll move on to `MainActivity.java` and the `res` folder structure.

### After my answer : 👇

# Section 03: Reading the Result

Your observations are exactly right, and your guess was close.

***

## 1. What actually happened

Two facts from your report:

- **"Default Activity not found"** is Android Studio's message. Studio wanted to *launch* your app, looked in the manifest for the front door, and found none.
- **No icon in the app drawer.** The launcher builds its icons from apps that declare a front door.

Your explanation was on the right track, with one adjustment. It's not that the intent-filter "points toward" MAIN and LAUNCHER. The intent-filter **declares** two things about the Activity:

- `MAIN` means "this is an entry point of the app."
- `LAUNCHER` means "list this entry point as an icon on the home screen or app drawer."

With the whole `<activity>` block commented out, Android had no record that `MainActivity` exists, let alone that it's a front door. The class still sits in your Java code, but the OS's directory doesn't mention it.

Think of the reception desk again: the department exists in the building, but it isn't in the directory, so reception can't send anyone there.

**Small distinction worth remembering:** if you had kept `<activity>` but removed only the `<intent-filter>`, the Activity would be registered but have no icon. Registering a component and making it launchable from the home screen are two separate things.

***

## 2. Restore the manifest

Remove the `<!--` and `-->` markers so the `<activity>` block is active again. Run the app once to confirm the icon returns.

***

## 3. Quick check

```
Q3. Which part of the manifest makes your app show an icon in the app drawer?

    A) android:exported="true" alone
    B) The intent-filter with MAIN and LAUNCHER
    C) The @string/app_name resource
    D) The Gradle sync

Correct answer: B
```

***

## 4. Now open MainActivity.java

Path: `app` → `java` → `com.afar.tasknest` → **`MainActivity.java`**

(Studio may show two extra `com.afar.tasknest` entries in grey with `(androidTest)` and `(test)`. Those are test folders, so ignore them for now.)

You saw this earlier:

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

The interesting line is `setContentView(R.layout.activity_main);`. It means: "Android, for this screen, display the layout called `activity_main`."

Two things to understand:

- **`R`** is a class Android **generates automatically** from your `res` folder. Every resource you add gets a numeric ID inside it. You never edit `R` yourself.
- **`R.layout.activity_main`** points to the file `app/src/main/res/layout/activity_main.xml`. Java doesn't contain the screen's appearance. The XML file does.

That's the separation I promised: **Java holds behavior, XML holds appearance.** If you know Angular, it's like a component's `.ts` file and its `.html` file.

***

## 5. The res folder

Under `app` → `res`, the main folders are:

- `layout/` holds screen designs (XML), for example `activity_main.xml`.
- `values/` holds strings, colors and themes, for example `strings.xml`, which you already edited.
- `drawable/` holds images and vector graphics.
- `mipmap/` holds launcher icons only.

Each folder name has a meaning. Android looks resources up by **folder type and file name**, which is why `R.layout.activity_main` and `@string/app_name` work.

***

## 6. Exercise: connect the pieces

**Goal:** prove that the layout file, the string resource and the Activity are linked.

**Step 1.** Open `app/src/main/res/values/strings.xml` and add one line inside `<resources>`:

```xml
<string name="welcome_message">Welcome to TaskNest</string>
```

**Step 2.** Open `app/src/main/res/layout/activity_main.xml`. Studio may show a Design view, so use the **Code** tab at the top right. Find the `<TextView>` (it likely says "Hello World!") and change its text line to:

```xml
android:text="@string/welcome_message"
```

**Step 3.** Run the app.

**Expected result:** the screen shows "Welcome to TaskNest".

**Common errors:**

- *Red text in `activity_main.xml`*: check that the string name matches exactly, including the underscore and lowercase.
- *No TextView in your layout*: paste me what your `activity_main.xml` contains and we'll adapt.

**Then break it:** in `activity_main.xml`, temporarily change the reference to `@string/welcome_messag` (missing the last letter) and try to run. Tell me what error you get, and where.

***

## 7. Report back with

1. Did the screen show the new text?
2. What error did the deliberate typo produce, and in which panel did you see it?
3. **Prediction:** `MainActivity.java` calls `setContentView(R.layout.activity_main)`. If you renamed the layout file to `main_screen.xml` using Studio's plain rename, what would you expect to happen, and why?

After that, we'll cover the **lifecycle at a high level** and the section checkpoint.