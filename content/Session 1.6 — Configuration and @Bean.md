# Session 1.6 — Configuration and `@Bean`

This session connects directly to what you've already learned about **Spring Beans**.

The key question today is:

> **We've seen that Spring can discover classes like `@Service` and `@Repository`. But what if we want to tell Spring explicitly: "Create this particular object as a Bean"?**

That's where `@Configuration` and `@Bean` come in.

***

## 1. Why does configuration exist?

Let's start with something you already understand from Java.

Suppose you have:

```java
class EmailService {
    public void sendEmail() {
        System.out.println("Email sent");
    }
}
```

In normal Java, you create the object yourself:

```java
EmailService emailService = new EmailService();
```

You are saying:

> "Create an `EmailService` object."

With Spring, we often want **Spring to create and manage the object**.

You already saw one way:

```java
@Service
public class EmailService {
}
```

Spring's component scanning can discover this class and create a Bean from it.

But sometimes you have a class where you **cannot or don't want to put `@Component` / `@Service` on the class**.

For example:

```java
class EmailService {
}
```

You can instead explicitly tell Spring:

> "Create an `EmailService` object and make it a Bean."

That's what `@Bean` does.

***

# 2. `@Configuration`

`@Configuration` tells Spring:

> **"This class contains configuration information for creating Beans."**

Example:

```java
@Configuration
public class AppConfig {

}
```

At this point, we've simply created a configuration class.

Think of it as a place where you can write:

```text
Spring configuration
       ↓
Which Beans should Spring create?
How should they be created?
```

But `@Configuration` by itself doesn't create our `EmailService`.

For that, we use `@Bean`.

***

# 3. `@Bean`

Here's the important part:

```java
@Configuration
public class AppConfig {

    @Bean
    public EmailService emailService() {
        return new EmailService();
    }
}
```

Look carefully at this:

```java
@Bean
public EmailService emailService() {
    return new EmailService();
}
```

The method is a normal Java method.

It returns:

```java
new EmailService()
```

Spring sees `@Bean` and says:

> "Whatever object this method returns, I should register as a Spring Bean."

So:

```java
return new EmailService();
```

creates the object.

And:

```java
@Bean
```

tells Spring to manage that returned object as a Bean.

***

# 4. A very important distinction

Don't confuse the **method** with the **Bean**.

```java
@Bean
public EmailService emailService() {
    return new EmailService();
}
```

Here:

* `emailService()` → Java method
* `new EmailService()` → creates an `EmailService` object
* returned `EmailService` object → becomes a Spring Bean
* `@Bean` → tells Spring about it

So you can mentally read it as:

```text
@Bean
   ↓
"Spring, take the object returned by this method
 and register it as a Bean."
```

***

# 5. Complete example

Imagine these two classes:

```java
public class EmailService {

    public void sendEmail() {
        System.out.println("Email sent");
    }
}
```

And:

```java
@Configuration
public class AppConfig {

    @Bean
    public EmailService emailService() {
        return new EmailService();
    }
}
```

Conceptually:

```text
AppConfig
   │
   │ @Bean
   ↓
emailService()
   │
   │ return new EmailService()
   ↓
EmailService object
   │
   ↓
Spring Container
   │
   ↓
EmailService Bean
```

This is **explicit Bean configuration**.

You explicitly told Spring how to create the Bean.

***

# 6. Component scanning vs `@Bean`

This is one of the most important parts of today's lesson.

You've already seen:

```java
@Service
public class EmailService {
}
```

This uses **component scanning**.

Spring scans your classes and discovers:

```java
@Service
```

Then Spring creates the Bean.

With `@Bean`:

```java
@Configuration
public class AppConfig {

    @Bean
    public EmailService emailService() {
        return new EmailService();
    }
}
```

You're explicitly telling Spring:

> "Here's exactly how you create this object."

### Compare them

| Component scanning              | `@Bean`                                     |
| ---------------------------- | ------------------------------------------- |
| `@Component`                    | `@Bean`                                     |
| `@Service`                      | Used inside `@Configuration`                |
| `@Repository`                   | Explicitly defines creation                 |
| Spring discovers the class      | You provide the creation method             |
| Convenient for your own classes | Useful when you need explicit configuration |

The important idea isn't memorizing the table.

Remember:

> **Component scanning = Spring discovers the class.**

> **`@Bean` = I explicitly tell Spring how to create the object.**

***

# 7. When is `@Bean` useful?

A common situation is when the class comes from **some library or framework**.

Imagine you use a library that provides:

```java
SomeLibraryClient
```

You didn't write that class.

You can't realistically go into the library's source code and add:

```java
@Component
```

to it.

So you can configure it yourself:

```java
@Configuration
public class AppConfig {

    @Bean
    public SomeLibraryClient client() {
        return new SomeLibraryClient();
    }
}
```

Now Spring manages that object as a Bean.

So a useful rule is:

> **Use component scanning when Spring can discover your class naturally.**

> **Use `@Bean` when you want explicit control over creating an object.**

Don't worry about library-specific configuration yet. The important thing today is understanding **why `@Bean` exists**.

***

# 8. Practical exercise

Since you don't have your Spring Boot project set up yet, **don't worry about running this right now**.

This is a conceptual coding exercise for today's Spring session. Your actual Spring Boot setup comes later.

Create these two classes.

### `GreetingService`

```java
public class GreetingService {

    public void sayHello() {
        System.out.println("Hello from GreetingService");
    }
}
```

### `AppConfig`

```java
@Configuration
public class AppConfig {

    @Bean
    public GreetingService greetingService() {
        return new GreetingService();
    }
}
```

Now answer these questions yourself:

### Question 1

What does this do?

```java
@Configuration
public class AppConfig
```

### Question 2

What does this do?

```java
@Bean
public GreetingService greetingService()
```

### Question 3

Who creates the object here?

```java
return new GreetingService();
```

### Question 4

Which object becomes the Spring Bean?

```java
return new GreetingService();
```

***

# 9. The mental model I want you to leave with

You can reduce today's entire lesson to this:

### Component scanning

```java
@Service
public class EmailService {
}
```

You say:

> "Spring, discover this class and make it a Bean."

### Explicit configuration

```java
@Configuration
public class AppConfig {

    @Bean
    public EmailService emailService() {
        return new EmailService();
    }
}
```

You say:

> "Spring, use this method to create the object and manage it as a Bean."

So:

```text
              Spring Bean
                  ↑
        ┌─────────┴─────────┐
        │                   │
Component scanning       @Bean
        │                   │
 @Service etc.        @Configuration
        │                   │
Spring discovers      You explicitly
the class             define creation
```

That's the core of Session 1.6.

***

# Checkpoint

Don't look back at the lesson if possible. Answer these in your own words:

1. **Why do we need `@Configuration`?**
2. **What does `@Bean` tell Spring to do?**
3. In this code, what is the difference between `greetingService()` and the `GreetingService` object?

```java
@Bean
public GreetingService greetingService() {
    return new GreetingService();
}
```

4. What's the main difference between:

```java
@Service
public class EmailService {
}
```

and:

```java
@Bean
public EmailService emailService() {
    return new EmailService();
}
```

If you can answer those four, **Session 1.6 is understood well enough to move on.**
