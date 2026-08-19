Look at this:

```java
class EmailService {
    public void sendEmail() {
        System.out.println("Email sent");
    }
}

class UserController {

    private EmailService emailService;

    public UserController() {
        emailService = new EmailService();
    }
}
```

***

**Yes, it is still a dependency.**

In software development, a dependency isn't determined by whether you call a method right now. It is determined by **structural relationship** (or *coupling*): `UserController` *has-a* `EmailService` field.

Even if the `sendEmail()` method is never invoked, `UserController` relies on the `EmailService` class to even exist and compile. If you deleted the `EmailService` class entirely, `UserController` would immediately fail to compile.

That is why it's a tight dependency—and it's precisely the kind of rigid coupling that Spring's **Dependency Injection** solves by managing these relationships from the outside rather than hardcoding them with `new`.