# java-101

A structured, public log of my Java and Spring Boot learning — core language fundamentals, Spring ecosystem concepts, and small hands-on projects, documented as I build them.

---

## 📖 About

This repo is where I track my progress learning **Java** and the **Spring** ecosystem from the ground up. Each topic gets a short write-up (with runnable code where relevant) so the repo doubles as both a personal reference and a portfolio of what I actually understand — not just what I've read.

Current focus: building a REST API (a "Cash Card" service) while working through core Spring Boot concepts — controllers, routing, serialization, persistence, and testing.

---

## 🗺️ Roadmap / Topics Covered

| Area | Topic | Status |
|---|---|---|
| Core Java | OOP fundamentals, collections, streams | 🔄 In Progress |
| Core Java | Exception handling, generics | ⏳ Planned |
| Spring Core | IoC container, Beans, Dependency Injection | 🔄 In Progress |
| Spring Boot | REST controllers & routing (`@RestController`, `@GetMapping`) | ✅ Done |
| Spring Boot | Request/response bodies, `ResponseEntity` | ✅ Done |
| Spring Boot | JSON serialization/deserialization (Jackson) | ✅ Done |
| Spring Data | Spring Data JPA, repositories | ⏳ Planned |
| Spring Security | Authentication & authorization basics | ⏳ Planned |
| Testing | JUnit 5, Mockito, AssertJ, `@SpringBootTest` | 🔄 In Progress |
| Build Tools | Maven / Gradle fundamentals | ⏳ Planned |

Legend: ✅ Done · 🔄 In Progress · ⏳ Planned

---

## 🛠️ Tech Stack

- **Language:** Java 17+
- **Framework:** Spring Boot
- **Build Tool:** Maven
- **Testing:** JUnit 5, AssertJ, Mockito
- **Database (upcoming):** H2 (dev), PostgreSQL (planned)

---

## 📂 Repo Structure

```
java-101/
├── core-java/          # Fundamentals: OOP, collections, streams, generics
├── spring-boot/
│   └── cashcard-api/    # REST API project — Cash Card service
│       ├── src/
│       └── notes/
│           └── implementing-get.md   # Lesson notes: REST, CRUD, GET endpoint
├── notes/               # General concept write-ups not tied to a specific project
└── README.md
```

> Structure will grow as new topics and projects are added — this reflects the current state, not a fixed plan.

---

## 🚀 Getting Started

Clone the repo and open any project folder independently (each is a self-contained Maven project):

```bash
git clone https://github.com/<your-username>/java-101.git
cd java-101/spring-boot/cashcard-api
./mvnw spring-boot:run
```

Run tests for a given project:

```bash
./mvnw test
```

---

## 📝 Notes & Lessons

Concept write-ups live alongside the code they relate to, e.g.:

- [`spring-boot/cashcard-api/notes/implementing-get.md`](./spring-boot/cashcard-api/notes/implementing-get.md) — REST, CRUD, HTTP, and implementing a `GET` endpoint with Spring Boot

More will be added as topics are covered.

---

## 🎯 Purpose

This is a learning-in-public repo — expect incremental commits, refactors, and the occasional rewrite as understanding deepens. Feedback and suggestions are welcome via issues.

---

## 📄 License

MIT — feel free to reference or reuse anything here for your own learning.