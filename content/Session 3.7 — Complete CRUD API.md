# Session 3.7 — Complete CRUD API

This is where the pieces you've learned finally connect:

```text
HTTP Request
     ↓
Controller
     ↓
Service
     ↓
Repository
     ↓
Database
```

And the database result travels back up:

```text
Database
     ↓
Repository
     ↓
Service
     ↓
Controller
     ↓
HTTP Response
```

For this session, we will build **actual CRUD for `Tenant`**.

We will **use the Entity directly for now**. DTOs are not part of this implementation yet.

***

# 1. What we're building

Our API will have these five endpoints:

| HTTP   | URL                 | Purpose         |
| ------ | ------------------- | --------------- |
| GET    | `/api/tenants`      | Get all tenants |
| GET    | `/api/tenants/{id}` | Get one tenant  |
| POST   | `/api/tenants`      | Create a tenant |
| PUT    | `/api/tenants/{id}` | Update a tenant |
| DELETE | `/api/tenants/{id}` | Delete a tenant |

We'll use your existing `Tenant` entity.

The important thing is that **you are going to create each layer yourself**, so I won't just dump five classes on you.

***

# 2. First: check your project structure

Before writing anything, your project should roughly look like this:

```text
src
└── main
    └── java
        └── com.lord.LandLord
            ├── Controller
            │   └── TenantController.java
            │
            ├── Entity
            │   └── Tenant.java
            │
            ├── Repository
            │   └── TenantRepository.java
            │
            └── Service
                └── TenantService.java
```

Your package names may differ slightly.

The important part is that you have these four Java classes:

```text
Tenant.java
TenantRepository.java
TenantService.java
TenantController.java
```

And PostgreSQL is your database.

***

# 3. Our Tenant Entity

You should already have a `Tenant` entity from Session 3.3.

For this exercise, let's assume it looks approximately like:

```java
@Entity
@Table(name = "tenants")
public class Tenant {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long tenantID;

    private String name;
    private String phone;
    private String email;

    // constructors
    // getters
    // setters
}
```

Your actual fields may be different.

**Do not replace your existing entity just because mine looks different.**

The CRUD logic works with whatever fields your existing `Tenant` entity has.

***

# 4. Repository — our database access layer

You already learned this in Session 3.5.

Open:

```text
Repository/TenantRepository.java
```

It should contain:

```java
package com.lord.LandLord.Repository;

import com.lord.LandLord.Entity.Tenant;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TenantRepository extends JpaRepository<Tenant, Long> {
}
```

That's it.

Notice something important:

**We aren't writing SQL.**

For example:

```java
findAll()
findById()
save()
deleteById()
```

are provided by `JpaRepository`.

So:

```text
TenantRepository
       ↓
JpaRepository
       ↓
Hibernate/JPA
       ↓
SQL
       ↓
PostgreSQL
```

You don't manually write:

```sql
SELECT * FROM tenants;
```

for this CRUD operation.

***

# 5. Service — where CRUD operations are coordinated

Open:

```text
Service/TenantService.java
```

Previously we only had something like:

```java
@Service
public class TenantService {

}
```

Now we're going to actually put operations inside it.

First, we need the repository.

```java
@Service
public class TenantService {

    private final TenantRepository tenantRepository;

    public TenantService(TenantRepository tenantRepository) {
        this.tenantRepository = tenantRepository;
    }
}
```

### Why?

Spring creates `TenantRepository` and injects it into the `TenantService` constructor.

So:

```text
TenantService
      |
      | needs
      ↓
TenantRepository
```

Now we can use:

```java
tenantRepository.findAll();
tenantRepository.findById(...);
tenantRepository.save(...);
tenantRepository.deleteById(...);
```

***

# 6. CRUD #1 — GET all tenants

We want:

```http
GET /api/tenants
```

to return all tenants.

## Service

Add:

```java
public List<Tenant> getAllTenants() {
    return tenantRepository.findAll();
}
```

You'll need:

```java
import java.util.List;
```

So your service now becomes:

```java
@Service
public class TenantService {

    private final TenantRepository tenantRepository;

    public TenantService(TenantRepository tenantRepository) {
        this.tenantRepository = tenantRepository;
    }

    public List<Tenant> getAllTenants() {
        return tenantRepository.findAll();
    }
}
```

### What's happening?

When this runs:

```java
tenantRepository.findAll();
```

Spring Data JPA retrieves all Tenant records.

Conceptually:

```sql
SELECT * FROM tenants;
```

Then JPA converts the database rows into Java `Tenant` objects.

***

# 7. Controller for GET all

Open:

```text
Controller/TenantController.java
```

We'll inject the service:

```java
@RestController
@RequestMapping("/api/tenants")
public class TenantController {

    private final TenantService tenantService;

    public TenantController(TenantService tenantService) {
        this.tenantService = tenantService;
    }
}
```

Now add:

```java
@GetMapping
public List<Tenant> getAllTenants() {
    return tenantService.getAllTenants();
}
```

You'll need:

```java
import java.util.List;
```

Now:

```http
GET /api/tenants
```

flows like this:

```text
GET /api/tenants
       ↓
TenantController
       ↓
tenantService.getAllTenants()
       ↓
tenantRepository.findAll()
       ↓
PostgreSQL
```

### Test it

Run your Spring Boot application.

Then in Postman:

```text
GET
http://localhost:8080/api/tenants
```

If you already have tenants in the database, you should get something similar to:

```json
[
    {
        "tenantID": 1,
        "name": "Rahim",
        "phone": "01700000000",
        "email": "rahim@example.com"
    },
    {
        "tenantID": 2,
        "name": "Karim",
        "phone": "01800000000",
        "email": "karim@example.com"
    }
]
```

***

# 8. CRUD #2 — GET one tenant

Now:

```http
GET /api/tenants/1
```

means:

> Find the tenant whose ID is 1.

## Service

Add:

```java
public Tenant getTenantById(Long id) {
    return tenantRepository.findById(id).orElse(null);
}
```

### The new thing: `findById()`

```java
tenantRepository.findById(id)
```

returns:

```java
Optional<Tenant>
```

rather than directly returning a `Tenant`.

For now, we're keeping this simple:

```java
.orElse(null)
```

means:

> If the tenant exists, give me the Tenant. Otherwise give me `null`.

We're not going deep into `Optional` in this session.

***

## Controller

Add:

```java
@GetMapping("/{id}")
public Tenant getTenantById(@PathVariable Long id) {
    return tenantService.getTenantById(id);
}
```

Now notice how the pieces connect:

```text
GET /api/tenants/5
          ↓
@PathVariable Long id
          ↓
tenantService.getTenantById(5)
          ↓
tenantRepository.findById(5)
```

### Test

```text
GET http://localhost:8080/api/tenants/1
```

You should get tenant `1`.

Try a nonexistent ID too:

```text
GET http://localhost:8080/api/tenants/999
```

With our deliberately simple implementation, you'll get:

```text
null
```

That's not our final production-style error handling; we're keeping today's CRUD implementation focused.

***

# 9. CRUD #3 — POST / Create

Now we create a tenant.

Request:

```http
POST /api/tenants
```

with JSON such as:

```json
{
    "name": "Hasan",
    "phone": "01900000000",
    "email": "hasan@example.com"
}
```

## Service

Add:

```java
public Tenant createTenant(Tenant tenant) {
    return tenantRepository.save(tenant);
}
```

That's all.

`save()` tells JPA:

> Persist this entity.

For a new entity, Hibernate will generate an appropriate SQL `INSERT`.

***

# 10. Controller

Add:

```java
@PostMapping
public Tenant createTenant(@RequestBody Tenant tenant) {
    return tenantService.createTenant(tenant);
}
```

Now the complete flow is:

```text
POST /api/tenants
       ↓
JSON
       ↓
@RequestBody
       ↓
Tenant object
       ↓
TenantController
       ↓
TenantService
       ↓
TenantRepository.save()
       ↓
Hibernate/JPA
       ↓
PostgreSQL
```

### Test in Postman

Method:

```text
POST
```

URL:

```text
http://localhost:8080/api/tenants
```

Body → raw → JSON:

```json
{
    "name": "Hasan",
    "phone": "01900000000",
    "email": "hasan@example.com"
}
```

Then send.

You should receive the saved tenant.

The database generates the ID, so the response might contain:

```json
{
    "tenantID": 3,
    "name": "Hasan",
    "phone": "01900000000",
    "email": "hasan@example.com"
}
```

***

# 11. CRUD #4 — PUT / Update

Now we want:

```http
PUT /api/tenants/3
```

to update tenant `3`.

For example:

```json
{
    "name": "Hasan Ahmed",
    "phone": "01911111111",
    "email": "hasan.ahmed@example.com"
}
```

There is an important difference here.

We have:

```text
ID from URL
       +
new Tenant data from request body
```

So:

```http
PUT /api/tenants/3
```

and:

```json
{
    "name": "Hasan Ahmed",
    ...
}
```

***

# 12. Service method for update

Add:

```java
public Tenant updateTenant(Long id, Tenant tenant) {

    Tenant existingTenant = tenantRepository.findById(id).orElse(null);

    if (existingTenant == null) {
        return null;
    }

    existingTenant.setName(tenant.getName());
    existingTenant.setPhone(tenant.getPhone());
    existingTenant.setEmail(tenant.getEmail());

    return tenantRepository.save(existingTenant);
}
```

This deserves careful attention.

We first search:

```java
Tenant existingTenant =
        tenantRepository.findById(id).orElse(null);
```

Suppose:

```text
id = 3
```

We find tenant 3.

Then:

```java
existingTenant.setName(tenant.getName());
```

changes the existing object's name.

Same for phone and email.

Finally:

```java
tenantRepository.save(existingTenant);
```

saves the modified entity.

***

# 13. Why not just `save(tenant)`?

You might wonder why we're doing all this.

Because the URL says:

```text
/api/tenants/3
```

The operation means:

> Update tenant whose ID is 3.

We therefore first locate **tenant 3**.

We're keeping the ID controlled by the URL rather than blindly trusting an ID supplied in the JSON body.

This also gives us a chance to check whether tenant 3 exists.

***

# 14. Controller for PUT

Add:

```java
@PutMapping("/{id}")
public Tenant updateTenant(
        @PathVariable Long id,
        @RequestBody Tenant tenant) {

    return tenantService.updateTenant(id, tenant);
}
```

Notice we have **two inputs**:

```java
@PathVariable Long id
```

comes from:

```text
/api/tenants/3
```

and:

```java
@RequestBody Tenant tenant
```

comes from:

```json
{
    "name": "Hasan Ahmed",
    "phone": "01911111111",
    "email": "hasan.ahmed@example.com"
}
```

***

# 15. CRUD #5 — DELETE

Finally:

```http
DELETE /api/tenants/3
```

## Service

Add:

```java
public void deleteTenant(Long id) {
    tenantRepository.deleteById(id);
}
```

That's it.

***

# 16. Controller

Add:

```java
@DeleteMapping("/{id}")
public void deleteTenant(@PathVariable Long id) {
    tenantService.deleteTenant(id);
}
```

Now:

```text
DELETE /api/tenants/3
       ↓
TenantController
       ↓
TenantService
       ↓
TenantRepository.deleteById(3)
       ↓
Database
```

***

# 17. Your complete Service

At this point your `TenantService` should look approximately like this:

```java
@Service
public class TenantService {

    private final TenantRepository tenantRepository;

    public TenantService(TenantRepository tenantRepository) {
        this.tenantRepository = tenantRepository;
    }

    public List<Tenant> getAllTenants() {
        return tenantRepository.findAll();
    }

    public Tenant getTenantById(Long id) {
        return tenantRepository.findById(id).orElse(null);
    }

    public Tenant createTenant(Tenant tenant) {
        return tenantRepository.save(tenant);
    }

    public Tenant updateTenant(Long id, Tenant tenant) {

        Tenant existingTenant =
                tenantRepository.findById(id).orElse(null);

        if (existingTenant == null) {
            return null;
        }

        existingTenant.setName(tenant.getName());
        existingTenant.setPhone(tenant.getPhone());
        existingTenant.setEmail(tenant.getEmail());

        return tenantRepository.save(existingTenant);
    }

    public void deleteTenant(Long id) {
        tenantRepository.deleteById(id);
    }
}
```

And your Controller approximately:

```java
@RestController
@RequestMapping("/api/tenants")
public class TenantController {

    private final TenantService tenantService;

    public TenantController(TenantService tenantService) {
        this.tenantService = tenantService;
    }

    @GetMapping
    public List<Tenant> getAllTenants() {
        return tenantService.getAllTenants();
    }

    @GetMapping("/{id}")
    public Tenant getTenantById(@PathVariable Long id) {
        return tenantService.getTenantById(id);
    }

    @PostMapping
    public Tenant createTenant(@RequestBody Tenant tenant) {
        return tenantService.createTenant(tenant);
    }

    @PutMapping("/{id}")
    public Tenant updateTenant(
            @PathVariable Long id,
            @RequestBody Tenant tenant) {

        return tenantService.updateTenant(id, tenant);
    }

    @DeleteMapping("/{id}")
    public void deleteTenant(@PathVariable Long id) {
        tenantService.deleteTenant(id);
    }
}
```

***

# 18. Now YOU do the practical exercise

Don't just copy the finished code and move on.

Your exercise is to build/test the CRUD API in this order.

### Step 1 — GET all

```text
GET /api/tenants
```

Confirm you can see your existing tenants.

### Step 2 — GET one

```text
GET /api/tenants/1
```

Use an ID that actually exists in your database.

### Step 3 — POST

Create a new tenant.

```text
POST /api/tenants
```

Use your actual `Tenant` fields.

### Step 4 — GET all again

Confirm the new tenant appears.

### Step 5 — PUT

Update that newly created tenant.

```text
PUT /api/tenants/{new-id}
```

### Step 6 — GET one again

Confirm the changed data.

### Step 7 — DELETE

```text
DELETE /api/tenants/{new-id}
```

### Step 8 — GET all again

Confirm the tenant disappeared.

Your CRUD lifecycle should therefore be:

```text
POST
 ↓
CREATE

GET
 ↓
READ

PUT
 ↓
UPDATE

DELETE
 ↓
DELETE
```

***

# 19. The most important thing to understand

Don't memorize the five controller methods.

Understand the **responsibility of each layer**.

### Entity

Represents the data:

```text
Tenant Java object
       ↕
tenants database row
```

### Repository

Talks to the database through Spring Data JPA:

```text
findAll()
findById()
save()
deleteById()
```

### Service

Coordinates the operation:

```text
"Get this tenant"
"Create this tenant"
"Update this tenant"
"Delete this tenant"
```

### Controller

Deals with HTTP:

```text
GET
POST
PUT
DELETE
```

So if Angular eventually sends:

```http
PUT /api/tenants/5
```

the architecture is:

```text
Angular
   │
   │ HTTP PUT
   ↓
┌─────────────────┐
│   Controller    │ ← HTTP
└────────┬────────┘
         ↓
┌─────────────────┐
│     Service     │ ← application logic
└────────┬────────┘
         ↓
┌─────────────────┐
│   Repository    │ ← database access
└────────┬────────┘
         ↓
┌─────────────────┐
│   PostgreSQL    │
└─────────────────┘
```

That's the core of **Session 3.7**.

***

# Checkpoint

Answer these **without looking back** if possible.

### 1.

What is the difference between:

```java
tenantRepository.findAll();
```

and:

```java
tenantService.getAllTenants();
```

Why don't we normally call the repository directly from the Controller?

### 2.

For:

```http
GET /api/tenants/7
```

what does:

```java
@PathVariable Long id
```

contain?

### 3.

For:

```http
POST /api/tenants
```

with:

```json
{
    "name": "Rahim"
}
```

what does:

```java
@RequestBody Tenant tenant
```

do?

### 4.

In:

```java
updateTenant(Long id, Tenant tenant)
```

where does each piece of information come from?

```text
id       → ?
tenant   → ?
```

### 5. Prove it

Without copying the CRUD code, explain this request in your own words:

```http
PUT /api/tenants/5
```

with:

```json
{
    "name": "Karim",
    "phone": "01712345678"
}
```

Trace it from **Controller → Service → Repository → Database**, including what the Service needs to do before saving the update.
