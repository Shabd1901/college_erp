# College ERP — Project Explainer / Living Learning Document

> **AI SESSION INSTRUCTION:** This is the project's **living textbook**. After every meaningful code change, automatically update this file with what was actually built, implementation decisions, code explanations, database/API changes, concepts the developer needs to learn, and testing performed. Do not explain hypothetical code—only document what currently exists in the project.

---

## 1. Current Project Status

**Phase:** Backend semester
**PBL Week:** Week 1
**Current milestone:** ERD and Database Setup

### Completed
- V1 entity scope defined (see `PRD.md`)
- Technical mapping strategy defined (see `TRD.md`)
- Project documentation optimized
- ER diagram and field-level entity design completed
- PostgreSQL database creation script added
- Spring Boot project setup & database connectivity

### Pending (Next Logical Steps)
- Entity implementation (Week 1)
- REST APIs (Week 2)
- Logging, Validation, Exception Handling, Swagger (Week 3)
- Relationship mappings, testing, and packaging (Week 4)

---

## 2. Decision Log

Important architectural and scope decisions are recorded here.

### Decision 001 — V1 Entity Scope
**Decision:** The project uses 10 primary domain entities: Student, Faculty, Department, Course, Subject, Division, Enrollment, Attendance, Examination, Result.
**Reasoning:** This fulfills the PBL relationship requirements while representing a realistic academic model.

### Decision 002 — Student to Division Relationship
**Decision:** Student belongs to Division (Many-to-One).
**Reasoning:** Retains the `Course -> Division -> Student` academic hierarchy instead of a flat model.

### Decision 003 — Enrollment Entity
**Decision:** Use `Enrollment` for Student-Subject assignments (One-to-Many from Student and Subject).
**Reasoning:** Avoids a vague Many-to-Many mapping and allows for future assignment attributes (academic year, semester).

### Decision 004 — Faculty to Subject Relationship
**Decision:** Faculty and Subject have a Many-to-Many relationship for V1.
**Reasoning:** Simple assignment. A dedicated assignment entity can be added in future semesters if workload tracking is needed.

### Decision 005 — Out of Scope
**Decision:** Frontend UI and Security (Auth/JWT) are explicitly excluded for this semester.

### Decision 006 — One-to-One Relationship Entity
**Decision:** A new `StudentProfile` entity was introduced specifically to satisfy the Week 4 One-to-One PBL requirement.
**Reasoning:** The core 10 academic entities don't naturally form a 1-to-1 relationship. Introducing a profile entity allows us to cleanly map a dedicated 1-to-1 relationship with `Student`.

---

## 3. Implementation Explanations
*(This section will grow. When an entity, controller, or architectural layer is actually implemented in code, explain how it works here.)*

---

## 4. API & Database Changes
*(This section will grow. Document specific endpoints, validation rules, and schema changes when implemented.)*

---

## 5. AI Implementation Log
*(Every meaningful change must add an entry here. Use the format below.)*

```
## YYYY-MM-DD — Short Change Title
### What changed
### Why
### Files changed
### Technical explanation
### Database / API impact
### Concepts to learn
### Testing performed
### Next step
```



--------------------



## 2026-08-14 — Week 1 Phase 1: ERD and Field-Level Design
### What changed
Created an ERD and defined the exact fields, data types, and keys for the database. Also introduced a `StudentProfile` entity.
### Why
To map out the relationships logically before generating any code or SQL, and to fulfill the PBL requirement for a 1-to-1 relationship.
### Files changed
- `ERD.md` created
- `PROJECT_EXPLAINER.md` updated
### Technical explanation
The design uses standard RDBMS patterns. We established primary keys, mapped one-to-many references using foreign keys on the "many" side, mapped a join table for the faculty-subject many-to-many relationship, and enforced a unique one-to-one mapping for the student profile.
### Database / API impact
Database design is now finalized. No APIs yet.
### Concepts to learn
- Entity Relationship Diagrams (ERD)
- Primary Keys vs Foreign Keys
- Database normalization
### Testing performed
Reviewed relationships against the TRD mapping requirements.
### Next step
Create the PostgreSQL database and set up the Spring Boot project.



--------------------



## 2026-08-14 — Week 1 Phase 2: Spring Boot Setup & DB Connectivity
### What changed
Created the base Spring Boot project structure (Maven `pom.xml`, Main Application class) and initialized PostgreSQL database configurations via `application.properties`. Added an `init.sql` script for creating the database.
### Why
To lay the technical foundation of the project before writing domain entities and to establish the connection between the application and the PostgreSQL server.
### Files changed
- `pom.xml`
- `src/main/java/com/college/erp/CollegeErpApplication.java`
- `src/main/resources/application.properties`
- `init.sql`
### Technical explanation
Used Maven to define the Spring Boot application and its dependencies: Spring Web (for REST APIs), Spring Data JPA (for database ORM), PostgreSQL Driver, and Validation. The `application.properties` file is configured to connect to `jdbc:postgresql://localhost:5432/college_erp` with `spring.jpa.hibernate.ddl-auto=update` so JPA will automatically generate our tables based on our future entities.
### Database / API impact
The database `college_erp` is expected to exist. The user can create it manually or by running `init.sql`. No tables exist yet.
### Concepts to learn
- Maven `pom.xml` and dependency management
- Spring Boot main class (`@SpringBootApplication`)
- `application.properties` configuration
- Hibernate `ddl-auto` (table auto-generation)
### Testing performed
Verified the standard Spring Boot structure.
### Next step
Implement the Entity classes in Java based on the ERD (Week 1 Phase 3).



--------------------


