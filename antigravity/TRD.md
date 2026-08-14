# College ERP — Technical Requirements Document (TRD)

**Current scope:** Backend semester
**Technology:** Java + Spring Boot + PostgreSQL
**Document status:** Baseline v1.0

---

## 1. Technology Stack
- **Language:** Java (stable LTS version)
- **Framework:** Spring Boot (Spring Web, Spring Data JPA, Validation, Springdoc OpenAPI)
- **Build Tool:** Maven
- **Database:** PostgreSQL
- **ORM:** JPA with Hibernate
- **API Documentation:** OpenAPI / Swagger UI
- **Testing:** Spring Boot testing tools, API client (Postman/Bruno)

## 2. Architecture & Package Structure
Use a conventional layered architecture without unnecessary abstractions (DTOs only when providing clear value):
```
Client -> Controller -> Service -> Repository -> JPA/Hibernate -> PostgreSQL
```
- **Controller:** HTTP requests, path/query params, status codes. No heavy business logic.
- **Service:** Business rules, orchestration, validation-related decisions.
- **Repository:** Database queries and CRUD via Spring Data JPA.
- **Entity:** Persistent domain data.

**Package Structure:**
```
com.college.erp
├── controller
├── service
├── repository
├── entity
├── dto
├── exception
├── config
└── util
```

## 3. Database Design Principles & Configuration
- Use PostgreSQL. Use externalized configuration (environment variables) for credentials; do not hardcode secrets.
- Define primary keys, foreign keys, unique constraints, and non-nullable fields based on the ERD.
- Do not add indexes without a specific performance reason.

## 4. API Conventions & PATCH Strategy
Expose REST endpoints using consistent naming:
```
GET     /api/<resource>
GET     /api/<resource>/{id}
POST    /api/<resource>
PUT     /api/<resource>/{id}   (Full update/replacement)
PATCH   /api/<resource>/{id}   (Partial update)
DELETE  /api/<resource>/{id}
```
For `PATCH`, update only the provided fields subject to validation.

## 5. JPA & Relationship Mapping Strategy
The project must demonstrate all mapping categories (required by PBL Week 4). The V1 entities are defined in `PRD.md`. Their technical mapping requirements are:
- **One-to-One:** A dedicated mapping is required. Since it's not in the core 10 V1 entities, it must be finalized during ERD design (e.g., `Student <-> StudentProfile`).
- **One-to-Many:** e.g., `Department -> Student`, `Subject -> Enrollment`.
- **Many-to-One:** e.g., `Student -> Division`.
- **Many-to-Many:** `Faculty <-> Subject`. (Direct many-to-many is acceptable for V1 without a join entity unless additional attributes are needed).

## 6. Validation
Use Jakarta Bean Validation for rules such as required fields, valid emails, numeric ranges, non-null relationships, and valid enum values. Document rules in `PROJECT_EXPLAINER.md`.

## 7. Exception Handling
Implement centralized exception handling using `@ControllerAdvice`.
Create standard exceptions (e.g., `ResourceNotFoundException`, `BadRequestException`) and ensure a consistent JSON error response structure.

## 8. Logging
Use Spring Boot's logging ecosystem. Log application startup, CRUD operations, validation failures, and unexpected exceptions. Do not log sensitive data (credentials, secrets, PII).

## 9. OpenAPI / Swagger
Expose documentation via Swagger UI. Document endpoints, methods, request/response bodies, parameters, and error responses.

## 10. Testing & Packaging
- **Testing:** Test entity/persistence behavior, REST endpoints (valid/invalid requests), and JPA relationship mappings.
- **Packaging:** Use `mvn clean package` to generate the executable artifact (JAR preferred unless WAR is required).

## 11. Technical Constraints
No major architecture changes (e.g., changing DB, framework, adding/removing entities, changing relationship strategy) should be made silently. Any such change must be justified and recorded in `PROJECT_EXPLAINER.md`. Frontend and Security remain explicitly out of scope.
