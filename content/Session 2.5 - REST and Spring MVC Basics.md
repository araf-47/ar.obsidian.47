# Session 2.5 — REST and Spring MVC Basics

This session is important because **this is where your Spring Boot application starts behaving like a backend API**.

We’ll build toward this:

```text
Angular
   ↓ HTTP request
Spring Boot REST API
   ↓
Controller
   ↓
HTTP response
   ↓
Angular
```

We will **not** go into databases, services, repositories, JPA, or Angular integration yet.

***

# 1. What is a REST API?

Let's start without Spring.

Suppose you have a website for managing students.

The frontend might need to:

* get all students
* get one student
* create a student
* update a student
* delete a student

The frontend communicates with the backend using **HTTP requests**.

For example:

```text
GET /students
```

means:

> "Backend, give me the students."

The backend sends an HTTP response:

```json
[
  {
    "id": 1,
    "name": "Rahim"
  },
  {
    "id": 2,
    "name": "Karim"
  }
]
```

That is a **REST API**.

### Simple definition

A **REST API** is a backend interface where clients communicate with resources using standard HTTP methods and URLs.

You can think of it as a contract between frontend and backend.

***

# 2. What is a Resource?

In REST, we usually think about the things our application manages as **resources**.

For example:

```text
Student
Teacher
Product
Order
Customer
```

For our example:

```text
Student
```

is a resource.

The URL representing the collection of students could be:

```text
/students
```

A specific student:

```text
/students/5
```

means:

> Student whose ID is 5.

So:

```text
/students
```

and

```text
/students/5
```

are **endpoints**.

***

# 3. What is an Endpoint?

An endpoint is basically a **URL through which the client can interact with the backend**.

For example:

```text
GET /students
```

is an endpoint.

Another:

```text
GET /students/5
```

Another:

```text
POST /students
```

Notice something important:

The URL can be the same:

```text
/students
```

but the HTTP method can be different.

For example:

```text
GET  /students
POST /students
```

They represent different operations.

We'll see why shortly.

***

# 4. HTTP Request and Response

You already know HTTP from JSP, so let's connect it to what you're learning now.

When Angular/browser talks to Spring Boot:

```text
Client                         Server

   HTTP Request
       ────────────────>
                         Spring Boot
                              |
                              |
       <────────────────
          HTTP Response
```

### Request

A request can contain things such as:

```text
HTTP method
URL
Headers
Body
```

For example:

```http
GET /students
```

or:

```http
POST /students
Content-Type: application/json

{
  "name": "Rahim"
}
```

The important new part for REST is that the **request body often contains JSON**.

***

# 5. What is JSON?

JSON is a common format for exchanging data between frontend and backend.

Example:

```json
{
  "id": 1,
  "name": "Rahim",
  "age": 22
}
```

It looks somewhat like a JavaScript object:

```javascript
const student = {
    id: 1,
    name: "Rahim",
    age: 22
};
```

This is one reason JSON is very common in web APIs.

For example:

```text
Angular
   |
   | JSON
   ↓
Spring Boot
```

and:

```text
Spring Boot
   |
   | JSON
   ↓
Angular
```

You don't need to learn JSON deeply in this session. Just understand that **JSON is a text-based data format commonly used in REST APIs**.

***

# 6. The Four Main HTTP Methods

Now we get to the most important part.

REST commonly uses:

```text
GET
POST
PUT
DELETE
```

Think about a `students` resource.

***

## GET — Read

```http
GET /students
```

Means:

> Give me the students.

For one student:

```http
GET /students/5
```

Means:

> Give me student 5.

So:

```text
GET → Read data
```

Similar to:

```sql
SELECT
```

***

# 7. POST — Create

Suppose we want to create a student.

```http
POST /students
```

The request might contain:

```json
{
  "name": "Rahim",
  "age": 22
}
```

Meaning:

> Create a new student using this data.

So:

```text
POST → Create
```

You can roughly compare it to:

```sql
INSERT
```

***

# 8. PUT — Update

Suppose student 5 already exists.

We want to update the student:

```http
PUT /students/5
```

with:

```json
{
  "name": "Rahim Ahmed",
  "age": 23
}
```

Meaning:

> Update student 5.

So:

```text
PUT → Update
```

Rough SQL comparison:

```sql
UPDATE
```

***

# 9. DELETE — Delete

To delete student 5:

```http
DELETE /students/5
```

Meaning:

> Delete student 5.

So:

```text
DELETE → Delete
```

Rough SQL comparison:

```sql
DELETE
```

***

# 10. The REST CRUD Picture

You should remember this:

| HTTP   | Purpose | SQL comparison |
| ------ | ------- | -------------- |
| GET    | Read    | SELECT         |
| POST   | Create  | INSERT         |
| PUT    | Update  | UPDATE         |
| DELETE | Delete  | DELETE         |

These are commonly called **CRUD operations**:

```text
C → Create → POST
R → Read   → GET
U → Update → PUT
D → Delete → DELETE
```

Don't worry about the word CRUD beyond recognizing it.

***

# 11. Now Let's Bring Spring Boot Into It

So far, everything we've discussed works at the HTTP/REST level.

Now Spring Boot gives us annotations that allow us to create these endpoints easily.

You have already run a Spring Boot application on port `8080`.

Let's create a controller.

***
```Araf
src
└── main
    └── java
        └── com.example.demo
            ├── DemoApplication.java
            │
            └── controller
                └── StudentController.java
```

# 12. `@RestController`

Create a Java class:

```java
@RestController
public class StudentController {

}
```

What does this mean?

```java
@RestController
```

tells Spring:

> "This class is a controller that handles REST requests."

So Spring can use this class to handle things like:

```text
GET /students
POST /students
DELETE /students
```

### Don't confuse this with a normal Java class

This:

```java
public class StudentController {
}
```

is simply a Java class.

Adding:

```java
@RestController
```

gives the class a special meaning to Spring.

***

# 13. `@RequestMapping`

We can give our controller a common URL path:

```java
@RestController
@RequestMapping("/students")
public class StudentController {

}
```

Now this controller is associated with:

```text
/students
```

Think of it as saying:

> "Student-related endpoints live under `/students`."

***

# 14. `@GetMapping`

Now let's create our first endpoint.

```java
@RestController
@RequestMapping("/students")
public class StudentController {

    @GetMapping
    public String getStudents() {
        return "All students";
    }
}
```

Let's understand it piece by piece.

### This:

```java
@GetMapping
```

means:

> Handle an HTTP GET request.

And because the controller has:

```java
@RequestMapping("/students")
```

the endpoint becomes:

```text
GET /students
```

When someone sends:

```text
GET http://localhost:8080/students
```

Spring calls:

```java
getStudents()
```

and the response is:

```text
All students
```

***

# 15. Let's Run It

Your project should already be running.

Add:

```java
@RestController
@RequestMapping("/students")
public class StudentController {

    @GetMapping
    public String getStudents() {
        return "All students";
    }
}
```

Then open:

```text
http://localhost:8080/students
```

You should see:

```text
All students
```

🎯 **You just created your first REST endpoint.**

Notice what happened:

```text
Browser
   |
   | GET /students
   ↓
Spring Boot
   |
   ↓
StudentController
   |
   ↓
getStudents()
   |
   ↓
"All students"
```

***

# 16. `@PostMapping`

Now let's add POST.

```java
@PostMapping
public String createStudent() {
    return "Student created";
}
```

Our controller becomes:

```java
@RestController
@RequestMapping("/students")
public class StudentController {

    @GetMapping
    public String getStudents() {
        return "All students";
    }

    @PostMapping
    public String createStudent() {
        return "Student created";
    }
}
```

Now Spring has:

```text
GET  /students
POST /students
```

Both use the same URL:

```text
/students
```

but they represent different operations because the **HTTP methods are different**.

***

# 17. `@PutMapping`

Add:

```java
@PutMapping
public String updateStudent() {
    return "Student updated";
}
```

Now:

```text
PUT /students
```

calls:

```java
updateStudent()
```

***

# 18. `@DeleteMapping`

Finally:

```java
@DeleteMapping
public String deleteStudent() {
    return "Student deleted";
}
```

Now:

```text
DELETE /students
```

calls:

```java
deleteStudent()
```

***

# 19. Our Complete Controller

For now, we can make a deliberately simple controller:

```java
@RestController
@RequestMapping("/students")
public class StudentController {

    @GetMapping
    public String getStudents() {
        return "All students";
    }

    @PostMapping
    public String createStudent() {
        return "Student created";
    }

    @PutMapping
    public String updateStudent() {
        return "Student updated";
    }

    @DeleteMapping
    public String deleteStudent() {
        return "Student deleted";
    }
}
```

This gives us:

```text
GET     /students  → getStudents()
POST    /students  → createStudent()
PUT     /students  → updateStudent()
DELETE  /students → deleteStudent()
```

That's the basic idea of **Spring MVC + REST**.

***

# 20. One Important Thing: Browser vs Postman

You can easily test:

```text
GET /students
```

by typing it into your browser.

But a browser's address bar normally sends a **GET** request.

You can't conveniently type:

```text
POST /students
```

into the address bar.

That's why tools such as **Postman** or `curl` are useful for testing REST APIs.

For this session, just understand the distinction:

```text
Browser address bar → easy GET testing

Postman/curl → GET, POST, PUT, DELETE
```

We'll keep the actual API testing mechanics for the appropriate session.

***

# 21. Why is this called Spring MVC?

You may wonder:

> "We're building REST APIs. Why is MVC involved?"

Spring MVC is Spring's web framework for handling HTTP requests.

Very simplified:

```text
HTTP Request
     ↓
Spring MVC
     ↓
Controller
     ↓
Java method
     ↓
HTTP Response
```

For example:

```text
GET /students
       ↓
@GetMapping
       ↓
getStudents()
       ↓
"All students"
```

For now, **Controller = the part of our application that receives HTTP requests and produces responses.**

That's enough for this session.

***

# 22. Your Practical Exercise

Now **don't copy my complete controller**.

Build one yourself.

Create:

```java
ProductController
```

with:

```java
@RestController
@RequestMapping("/products")
```

Then create four methods:

### GET

```text
GET /products
```

Response:

```text
"All products"
```

### POST

```text
POST /products
```

Response:

```text
"Product created"
```

### PUT

```text
PUT /products
```

Response:

```text
"Product updated"
```

### DELETE

```text
DELETE /products
```

Response:

```text
"Product deleted"
```

Your goal is to write the controller yourself using:

```java
@RestController
@RequestMapping
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
```

**Don't worry about JSON request bodies yet.** We're only learning the REST/MVC structure here.

***

# Checkpoint 🧠

Before moving on, answer these **without looking back**:

### 1.

What is a REST API?

### 2.

What is the difference between:

```text
Resource
Endpoint
```

### 3.

What does this endpoint mean?

```text
GET /students
```

### 4.

What HTTP method would you normally use to create a new student?

```text
GET / POST / PUT / DELETE
```

### 5.

What does this annotation tell Spring?

```java
@RestController
```

### 6.

What does this do?

```java
@RequestMapping("/students")
```

### 7.

What is the difference between:

```java
@GetMapping
```

and

```java
@PostMapping
```

### 8.

If you write:

```java
@RequestMapping("/products")

@GetMapping
public String test() {
    return "Hello";
}
```

what HTTP endpoint does `test()` handle?

**Answer these 8 questions and show me your `ProductController`.** I'll check your understanding/code before we move to the next session.

> Try this in any Ai.