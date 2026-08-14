# College ERP — Product Requirements Document (PRD)

**Project type:** Java Full Stack Development (FSD) — Project-Based Learning (PBL)
**Current semester scope:** Backend only
**Future semesters:** Frontend, then Security
**Document status:** Baseline v1.0

---

## 1. Project Purpose & Overview
The College ERP is an academic backend system developed as a Spring Boot Project-Based Learning activity. It models common academic operations of a college.
This project is primarily an **academic learning project**, not a production ERP intended for deployment in a real college. The developer must progressively understand the implementation to write similar code independently.

## 2. Actors
The system models the following conceptual actors:
- **Student**: Consumes academic information (enrollment, attendance, examinations, results).
- **Faculty**: Represents teaching staff and their relationship with subjects.
- **Academic Administration**: Conceptually manages departments, courses, divisions, subjects, examinations, and results.
*(Note: Authentication/authorization are not implemented in the current semester.)*

## 3. V1 Features & Functional Requirements
The core functional requirement is to provide RESTful CRUD (Create, Read, Update, Delete) and partial-update (PATCH) APIs for the core academic entities. The system must maintain referential integrity based on the defined relationships.

## 4. V1 Scope & Entities
The agreed V1 entity set is strictly limited to the following 10 entities. 
*(For technical mappings and JPA relationships, see `TRD.md`.)*

1. **Student**: Represents an enrolled student. Belongs to one Division.
2. **Faculty**: Represents a faculty member. Has a Many-to-Many teaching relationship with Subject for V1.
3. **Department**: Represents an academic department. Can contain multiple students, faculty, and courses.
4. **Course**: Represents an academic program (e.g., B.E. Information Technology). Contains multiple divisions.
5. **Subject**: Represents an academic subject. Taught by faculty; students enroll in it.
6. **Division**: Represents a class/division within a course. Contains multiple students.
7. **Enrollment**: Represents a student's academic association with a subject (Student–Subject assignment).
8. **Attendance**: Represents attendance recorded for a student and subject.
9. **Examination**: Represents an examination event (e.g., Mid-Semester).
10. **Result**: Represents a student's result for a subject in an examination. Grade belongs to Result in V1.

## 5. Non-Functional Requirements
- **Modular & Maintainable**: Code should prioritize readability over unnecessary enterprise complexity.
- **RESTful**: APIs should follow REST conventions.
- **Robust**: Must include centralized exception handling and request validation.
- **Observable**: Must include application logging.
- **Documented**: API documentation via OpenAPI/Swagger.

## 6. PBL Schedule and Deliverables
The project must be built incrementally following this 4-week schedule:

- **Week 1 (Foundation):** Requirement analysis, ERD preparation, PostgreSQL database creation, Spring Boot project setup, database connectivity, and entity creation.
- **Week 2 (REST APIs):** REST API implementations (GET, POST, PUT, PATCH, DELETE) for selected entities.
- **Week 3 (Backend Quality):** Application logging, global exception handling, validation, Swagger/OpenAPI documentation, API testing.
- **Week 4 (Relationships & Completion):** Implement and test all mapping types (One-to-One, One-to-Many, Many-to-One, Many-to-Many). JAR/WAR generation, final backend testing.

## 7. Future Scope
Explicitly out of scope for the current semester but planned for future phases:
- Frontend UI (React)
- Security (Authentication, JWT, role-based authorization)
- Finance, Library, Campus Management, and Advanced Analytics.
