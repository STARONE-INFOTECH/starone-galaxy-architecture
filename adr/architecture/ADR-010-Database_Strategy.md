# ADR-010: Data Ownership & Database Strategy — Database per Bounded Context

---

# 1. Title Page

| Field       | Value                              |
| ----------- | ---------------------------------- |
| Document ID | ADR-010                            |
| Project     | StarOne Galaxy                     |
| Decision    | Data Ownership & Database Strategy |
| Author      | Sachin Salunke                     |
| Date        | Jan 2026                           |
| Status      | Accepted                           |

---

# 2. Context

StarOne Galaxy adopts a Domain-Driven Design (DDD) architecture composed of independently deployable microservices.

Each bounded context represents a distinct business capability with its own lifecycle and business rules.

To preserve domain autonomy, the platform requires clear ownership of business data and persistence responsibilities.

The data architecture must support:

- Independent service evolution
- Strong domain ownership
- Loose coupling
- Future scalability
- Technology flexibility

---

## 2.1 Problem Statement

```text
How should business data be owned and persisted across
bounded contexts while maintaining domain autonomy,
data integrity, and long-term scalability?
```

---

## 2.2 Key Challenges

- Prevent shared database coupling
- Define clear ownership boundaries
- Support independent deployment
- Maintain transactional consistency within domains
- Enable future database technology evolution

---

# 3. Decision

StarOne Galaxy adopts a **Database per Bounded Context** strategy.

Each bounded context shall own its persistence layer and be solely responsible for creating, updating, and maintaining its business data.

Direct database access between bounded contexts is prohibited.

Cross-domain interactions shall occur only through approved APIs or messaging mechanisms defined by ADR-005.

---

## 3.1 Data Ownership Principles

Each bounded context owns:

- Database schema
- Business entities
- Aggregate roots
- Repository implementations
- Database migrations

Other bounded contexts may consume exposed APIs but shall never access another domain's database directly.

---

## 3.2 Database Independence

The architecture does not mandate a single database technology.

Current implementation:

```text
PostgreSQL
```

Future bounded contexts may adopt alternative persistence technologies when justified, without impacting other domains.

---

## 3.3 Development Environment

For development purposes, multiple schemas may reside within a single PostgreSQL instance to simplify local setup.

This implementation convenience does not change the architectural principle of independent data ownership.

---

## 3.4 Cross-Domain Data Access

Permitted:

```text
Service A
    │
REST / Events
    │
Service B
```

Not Permitted:

```text
Service A
    │
Direct SQL
    │
Service B Database
```

---

# 4. Alternatives Considered

---

## 4.1 ❌ Shared Enterprise Database

**Rejected Because**

- Tight coupling
- Difficult schema evolution
- Reduced service autonomy
- Complex deployments

---

## 4.2 ❌ Shared Database with Separate Schemas

**Rejected Because**

- Weak ownership boundaries
- Risk of accidental cross-domain access
- Limited scalability

---

## 4.3 ✅ Database per Bounded Context (Chosen)

**Reasons**

- Strong ownership
- Independent deployments
- Better scalability
- Supports Domain Driven Design
- Easier future migration

---

# 5. Consequences

---

## 5.1 ✅ Positive

- Clear ownership
- Independent evolution
- Better scalability
- Technology flexibility
- Reduced coupling

---

## 5.2 ⚠️ Negative

- Data duplication may occur
- Cross-domain queries require APIs
- Distributed consistency requires additional design

---

# 6. Trade-offs

| Trade-off                                      | Decision                    |
| ---------------------------------------------- | --------------------------- |
| Simplicity vs Domain Independence              | Chose Domain Independence   |
| Shared Data vs Service Autonomy                | Chose Service Autonomy      |
| Centralized Reporting vs Independent Ownership | Chose Independent Ownership |

---

# 7. Impact

---

## Affects

- Database architecture
- Service design
- Integration strategy
- Repository implementation
- Data migration

---

## Enables

- Independent deployments
- Technology evolution
- Service autonomy
- Future polyglot persistence

---

# 8. Rules Enforced

```text
1. Every bounded context owns its data.

2. Direct database access between services is prohibited.

3. Cross-domain communication shall occur only through APIs or events.

4. Database migrations are owned by the respective bounded context.

5. Development environments may share a PostgreSQL instance using separate schemas, but production ownership remains independent.
```

---

# 9. Related Artifacts

- ADR-005 Messaging Strategy
- ADR-007 Architecture Style
- ADR-008 Domain Decomposition Strategy
- ADR-009 API Design Strategy
- HLD
- LLD
- SRS

---

# 10. Decision Summary

```text
StarOne Galaxy adopts a Database per Bounded Context strategy
to ensure clear data ownership, independent service evolution,
reduced coupling, and alignment with Domain-Driven Design principles.
```

---

# 11. Status

```text
ACCEPTED — Independent data ownership is mandatory across all
bounded contexts within the StarOne Galaxy ecosystem.
```

---
