Yes. Since you're using:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
```

the easiest way is to use the **H2 web console**.

## 1. Enable the H2 console

In `application.properties`, add:

```properties
spring.h2.console.enabled=true
```

So your configuration becomes:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver

spring.jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true

spring.h2.console.enabled=true
```

***

## 2. Start your Spring Boot application

Keep the application **running**.

This is important because:

```text
jdbc:h2:mem:testdb
```

means the database exists **only while your application is running**.

***

## 3. Open the H2 console

In your browser, go to:

```text
http://localhost:8080/h2-console
```

You'll get an H2 login page.

Use:

```text
JDBC URL:
jdbc:h2:mem:testdb
```

For username, normally:

```text
sa
```

For password, leave it empty unless you configured one.

Then click **Connect**.

***

## 4. Look for the `PRODUCT` table

If Hibernate successfully created your Entity's table, you should see something like:

```text
TESTDB
└── PUBLIC
    └── PRODUCT
```

Click/expand `PRODUCT`.

Then you can run SQL manually.

For example:

```sql
SELECT * FROM PRODUCT;
```

If your `TestData` class successfully saved:

```java
new Product(1L, "Keyboard", 1200);
```

you should see something similar to:

```text
ID | NAME     | PRICE
---+----------+------
1  | Keyboard | 1200
```

***

## 5. You can also manually run SQL

Because H2 is a relational database, you can interact with it using SQL just like you're accustomed to with PostgreSQL.

For example:

```sql
SELECT * FROM PRODUCT;
```

or:

```sql
SELECT NAME, PRICE
FROM PRODUCT;
```

You can even insert something manually:

```sql
INSERT INTO PRODUCT (ID, NAME, PRICE)
VALUES (2, 'Mouse', 800);
```

Then:

```sql
SELECT * FROM PRODUCT;
```

would show both rows.

***

### One important thing to understand

With your current configuration:

```text
Spring Boot running
       ↓
H2 database exists
       ↓
H2 Console can see it
```

But:

```text
Stop Spring Boot
       ↓
H2 in-memory database disappears
```

So if you stop the application and start it again, the manually inserted `Mouse` will be gone.

That's **exactly what "in-memory" means** in this context.


# in case of error page

That means Spring Boot is **not serving the H2 Console at `/h2-console` yet**. Let's check the configuration first.

Make sure your `application.properties` contains **exactly these H2-related lines**:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver

spring.jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true

spring.h2.console.enabled=true
```

### Then do this

1. **Stop** your Spring Boot application completely.
2. Start it again.
3. Wait until you see that Tomcat has started, e.g.:

   ```text
   Tomcat started on port 8080
   ```
4. Open:

   ```text
   http://localhost:8080/h2-console
   ```

### If you still get the white error page

The most useful thing is to see **what Spring Boot actually says in your console** when it starts.

You can paste the startup output here, especially anything containing:

```text
H2
h2-console
ERROR
Exception
Tomcat
```

Or upload a screenshot of the browser error and/or terminal output, and I can pinpoint what's wrong.
