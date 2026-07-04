# ADR-007: Architecture Style — Microservices with Hexagonal Architecture

---

# 1. Title Page

| Field       | Value                                           |
| ----------- | ----------------------------------------------- |
| Document ID | ADR-007                                         |
| Project     | StarOne Galaxy                                  |
| Decision    | Architecture Style                              |
| Author      | Sachin Salunke                                  |
| Date        | Jan 2026                                        |
| Status      | Accepted                                        |

---

# 2. Context

StarOne Galaxy is designed as a multi-domain enterprise platform consisting of independently evolving business systems, including:

- DHS (Distributed Hub & Sales)
- Bookshow
- Future business domains

The platform must support:

- Independent deployment
- Business domain isolation
- Maintainable codebases
- Testability
- Technology evolution
- Scalability
- Clear separation of business logic from infrastructure

The architecture must also support future migration of services without impacting business rules.

---

## 2.1 Problem Statement

```text
Which application architecture should be adopted to ensure
maintainability, scalability, testability, and long-term
evolution of the platform?
```

---

## 2.2 Key Challenges

- Avoiding tightly coupled application layers
- Protecting business logic from framework dependencies
- Supporting independent microservice evolution
- Enabling unit testing without infrastructure dependencies
- Maintaining consistency across all services

---

# 3. Decision

StarOne Galaxy adopts:

```text
Microservice Architecture

combined with

Hexagonal Architecture (Ports & Adapters)

following Clean Architecture principles.
```

Each business capability shall be implemented as an independent microservice.

Within each service, business logic shall remain independent of:

- Spring Framework
- Database
- Messaging
- External APIs
- Infrastructure technologies

---

## 3.1 Service Architecture

Each microservice shall contain:

```text
API Layer

↓

Application Layer

↓

Domain Layer

↓

Ports

↓

Adapters

↓

Infrastructure
```

Business rules always remain inside the Domain Layer.

---

## 3.2 Dependency Rule

Dependencies flow inward only.

```text
Infrastructure
      │
      ▼
Adapters
      │
      ▼
Application
      │
      ▼
Domain
```

The Domain Layer shall never depend on external frameworks.

---

## 3.3 Business Isolation

Each microservice owns:

- Business logic
- Domain model
- Application services
- Repository interfaces
- Integration ports

Infrastructure implementations remain replaceable.

---

## 3.4 Technology Independence

Business rules must remain independent of:

- Spring Boot
- PostgreSQL
- Kafka
- Redis
- REST Controllers

Technology changes shall not require modifications to business logic.

---

# 4. Alternatives Considered

---

## 4.1 ❌ Traditional Layered Architecture

**Rejected Because**

- Business logic becomes coupled with infrastructure
- Difficult testing
- Reduced flexibility
- Harder technology replacement

---

## 4.2 ❌ Framework-Centric Architecture

**Rejected Because**

- Heavy Spring dependency
- Difficult migration
- Reduced portability

---

## 4.3 ✅ Microservices + Hexagonal Architecture (Chosen)

**Reasons**

- Strong separation of concerns
- Better maintainability
- Improved testability
- Independent technology evolution
- Supports Domain Driven Design
- Suitable for enterprise-scale systems

---

# 5. Consequences

---

## 5.1 ✅ Positive

- Independent business logic
- Framework independence
- Better unit testing
- Improved maintainability
- Easier technology replacement
- Consistent architecture across services

---

## 5.2 ⚠️ Negative

- More initial structure
- Higher learning curve
- Additional abstraction layers

---

# 6. Trade-offs

| Trade-off | Decision |
|-----------|----------|
| Simplicity vs Maintainability | Chose Maintainability |
| Initial Development Speed vs Long-Term Flexibility | Chose Flexibility |
| More Abstraction vs Better Testability | Chose Testability |

---

# 7. Impact

---

## Affects

- All microservices
- Project structure
- Coding standards
- Testing strategy
- Repository organization

---

## Enables

- Domain Driven Design
- Independent deployment
- Better testing
- Easier refactoring
- Future technology migration

---

# 8. Rules Enforced

```text
1. Every service shall follow Hexagonal Architecture.

2. Business logic shall remain framework independent.

3. Domain Layer shall not depend on Infrastructure.

4. Infrastructure communicates through Ports.

5. Business rules remain inside the Domain Layer.

6. Technology changes shall not modify business logic.
```

---

# 9. Related Artifacts

- ADR-001 Repository Taxonomy
- ADR-004 Configuration Management Strategy
- ADR-005 Messaging Strategy
- ADR-006 Identity Strategy
- HLD-001 Enterprise Architecture
- LLD Service Design Documents

---

# 10. Decision Summary

```text
StarOne Galaxy adopts a Microservice Architecture using
Hexagonal Architecture (Ports & Adapters) and Clean
Architecture principles to ensure maintainability,
technology independence, scalability, and long-term
evolution of enterprise services.
```

---

# 11. Status

```text
ACCEPTED — This architecture style is mandatory for all
business services developed within the StarOne Galaxy ecosystem.
```

---