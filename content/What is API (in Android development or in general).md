# API Explained Simply

**API** stands for "Application Programming Interface." Think of it as a **set of instructions for how to ask for something**.

## The Restaurant Analogy

Imagine a restaurant:
- You (the customer) don't go into the kitchen and cook your own meal
- You look at the **menu** (the API)
- You order from the menu (call the API)
- The kitchen handles the work and gives you food (the result)

The **menu is the interface**—it defines what you can ask for and how to ask for it. You don't need to know *how* they cook; you just need to know the menu.

## In Android/Java

An API is how your app **asks Android to do things**. Examples:

- **Camera API** → tells Android "I want to use the camera"
- **Location API** → tells Android "I want the user's location"
- **Notification API** → tells Android "show a notification"

Your code doesn't directly access the camera hardware. Instead, you use the API—Android's pre-written code—which handles all the complexity.

## In Spring (your focus)

When you use Spring's **dependency injection**, you're using an API. You ask Spring: "Give me a database connection object" and Spring handles creating it and giving it to you.

***

**Core idea:** An API is a contract that says "if you ask for something *this way*, I'll give you that result." It abstracts away the messy details so you can focus on your app's logic.