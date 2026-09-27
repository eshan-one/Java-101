# Implementing GET — REST, CRUD & Spring Boot

> Learning notes on building a RESTful `GET` endpoint with Spring Boot.

---

## 📚 Table of Contents

- [What is REST?](#what-is-rest)
- [CRUD and HTTP](#crud-and-http)
- [Anatomy of a Request & Response](#anatomy-of-a-request--response)
- [Example: Reading a Cash Card](#example-reading-a-cash-card)
- [REST in Spring Boot](#rest-in-spring-boot)
  - [Spring Beans & Component Scan](#spring-beans--component-scan)
  - [The `@RestController`](#the-restcontroller)
  - [Handling GET with `@GetMapping`](#handling-get-with-getmapping)
  - [Binding the Path Variable](#binding-the-path-variable)
  - [Returning a Proper Response](#returning-a-proper-response)
- [Final Implementation](#final-implementation)
- [Key Takeaways](#key-takeaways)

---

## What is REST?

**REST** = **Re**presentational **S**tate **T**ransfer.

In a RESTful system:

| Concept | Think of it as |
|---|---|
| **Resource Representation** | An "object" or "thing" |
| **State** | The "value" of that thing |
| **REST** | A way to manage the values of things, usually over HTTP, usually backed by a database |

A RESTful API exposes these Resources so clients can create, read, update, and delete them in a predictable, standardized way.

```
Client  --- HTTP Request --->  Web Server --- routes to --->  Handler
Client  <--- HTTP Response ---  Web Server  <--- creates ---   Handler
```

---

## CRUD and HTTP

**CRUD** = **C**reate, **R**ead, **U**pdate, **D**elete — the four basic operations you can perform on any resource in a data store.

REST maps each CRUD operation to a specific **HTTP method** (verb), **endpoint**, and expected **response status**:

| Operation | Endpoint | HTTP Method | Response Status |
|---|---|---|---|
| Create | `/cashcards` | `POST` | `201 CREATED` |
| Read | `/cashcards/{id}` | `GET` | `200 OK` |
| Update | `/cashcards/{id}` | `PUT` | `204 NO CONTENT` |
| Delete | `/cashcards/{id}` | `DELETE` | `204 NO CONTENT` |

📌 **Note:** `READ`, `UPDATE`, and `DELETE` all require a unique identifier (`{id}`) so the server knows *exactly* which resource to act on. `CREATE` does **not** — the server generates a new unique ID as a side effect of creation.

---

## Anatomy of a Request & Response

| Request | Response |
|---|---|
| Method (Verb) | Status Code |
| URI (Endpoint) | Body |
| Body | |

- `CREATE` and `UPDATE` require a **request body** — the data needed to build or change the resource.
- `READ` and `DELETE` requests typically have an **empty body**.

---

## Example: Reading a Cash Card

Reading the Cash Card with `id = 123`:

**Request**

```http
GET http://cashcard.example.com/cashcards/123
Body: (empty)
```

**Response**

```http
Status Code: 200 OK

{
  "id": 123,
  "amount": 25.00
}
```

Simple, predictable, and exactly what REST promises: a `GET` to `/cashcards/{id}` returns the JSON representation of that resource with a `200 OK`.

---

## REST in Spring Boot

### Spring Beans & Component Scan

Spring's **IoC (Inversion of Control) container** creates and manages objects for you — these are called **Spring Beans**. Instead of instantiating classes yourself with `new`, you annotate a class and let Spring do it during **Component Scan** (which happens at application startup). Once created, a Bean can be **injected** anywhere it's needed.

### The `@RestController`

To tell Spring "this class handles REST requests," annotate it with `@RestController`:

```java
@RestController
class CashCardController {
}
```

Spring registers this Controller and routes matching API requests to it.

### Handling GET with `@GetMapping`

Start with a plain handler method:

```java
private CashCard findById(Long requestedId) {
}
```

Since `READ` maps to `GET`, tell Spring to route `GET` requests for a specific path to this method using `@GetMapping`:

```java
@GetMapping("/cashcards/{requestedId}")
private CashCard findById(Long requestedId) {
}
```

### Binding the Path Variable

Spring needs to know how to populate `requestedId` from the URL. The `@PathVariable` annotation does this — because the parameter name matches the `{requestedId}` placeholder in the path, Spring auto-injects the value:

```java
@GetMapping("/cashcards/{requestedId}")
private CashCard findById(@PathVariable Long requestedId) {
}
```

### Returning a Proper Response

REST requires the response to have:

- a **body** containing the resource (as JSON)
- a **status code** of `200 OK`

Spring Web's `ResponseEntity` class handles both, with convenient factory methods like `ResponseEntity.ok(...)`.

---

## Final Implementation

```java
@RestController
class CashCardController {

  @GetMapping("/cashcards/{requestedId}")
  private ResponseEntity<CashCard> findById(@PathVariable Long requestedId) {
    CashCard cashCard = /* retrieve the CashCard here */;
    return ResponseEntity.ok(cashCard);
  }
}
```

**What each piece does:**

| Annotation / Type | Purpose |
|---|---|
| `@RestController` | Marks the class as a Spring Bean that handles REST requests |
| `@GetMapping("/cashcards/{requestedId}")` | Routes `GET` requests matching this URI to this method |
| `@PathVariable` | Extracts `{requestedId}` from the URL into the method parameter |
| `ResponseEntity<CashCard>` | Wraps the response body + status code (`200 OK` via `ResponseEntity.ok(...)`) |

---

## Key Takeaways

- REST maps CRUD operations to HTTP verbs: `POST` → Create, `GET` → Read, `PUT` → Update, `DELETE` → Delete.
- `READ`/`UPDATE`/`DELETE` need a resource `{id}`; `CREATE` does not (the server generates it).
- A successful `GET` returns `200 OK` with the resource as the JSON body.
- Spring Boot turns this into a few annotations: `@RestController`, `@GetMapping`, `@PathVariable`, and `ResponseEntity`.

---

*Part of my Spring Boot learning journey — see the rest of this repo for more.*