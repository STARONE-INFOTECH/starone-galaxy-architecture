# Requirement ID Standard

**Document ID:** STD-REQID-001

**Version:** v1.0.0

**Status:** Approved

---

# 1. Purpose

This standard defines the enterprise convention for uniquely identifying requirements across the StarOne Galaxy ecosystem.

The objective is to ensure that every requirement is:

- Globally unique
- Human-readable
- Traceable
- Repository-independent
- Consistent across all documentation
- Suitable for implementation, testing, and audit

---

# 2. Scope

This standard applies to all requirement-bearing documents, including:

- BRD
- PRD
- FRD
- SRS
- HLD
- LLD
- ADR (Decision IDs)
- Test Specifications
- User Stories
- Epics

---

# 3. Design Principles

Requirement identifiers shall be:

- Unique
- Immutable
- Sequential
- Meaningful
- Stable throughout the project lifecycle

Requirement IDs shall never be reused, even if a requirement is deleted or deprecated.

---

# 4. Requirement ID Structure

The standard format is:

```text
<SERVICE>-<CATEGORY>-<NUMBER>
```

Example:

```text
ID-SYS-001
```

Where:

| Element  | Description                   |
| -------- | ----------------------------- |
| SERVICE  | Service or platform prefix    |
| CATEGORY | Requirement category          |
| NUMBER   | Three-digit sequential number |

---

# 5. Service Prefixes

## Platform Foundation

```text
PF
```

## Identity Service

```text
ID
```

## Branch Service

```text
BR
```

## Customer Service

```text
CU
```

## Product Service

```text
PR
```

## Inventory Service

```text
IN
```

## Order Service

```text
OR
```

## Billing Service

```text
BI
```

## Dispatch Service

```text
DI
```

## Notification Service

```text
NO
```

## Reporting Service

```text
RE
```

## Audit Service

```text
AU
```

---

# 6. Requirement Categories

| Prefix | Description                |
| ------ | -------------------------- |
| SYS    | Functional Requirement     |
| API    | API Requirement            |
| DB     | Database Requirement       |
| EVT    | Event Requirement          |
| CFG    | Configuration Requirement  |
| SEC    | Security Requirement       |
| COM    | Communication Requirement  |
| NFR    | Non-Functional Requirement |
| VAL    | Validation Requirement     |

---

# 7. Examples

Functional Requirement

```text
ID-SYS-001
```

Security Requirement

```text
ID-SEC-001
```

API Requirement

```text
ID-API-001
```

Database Requirement

```text
ID-DB-001
```

Configuration Requirement

```text
ID-CFG-001
```

Event Requirement

```text
ID-EVT-001
```

Communication Requirement

```text
ID-COM-001
```

Validation Requirement

```text
ID-VAL-001
```

Non-Functional Requirement

```text
ID-NFR-001
```

---

# 8. Numbering Rules

Requirements shall begin with:

```text
001
```

Examples:

```text
ID-SYS-001
ID-SYS-002
ID-SYS-003
```

Numbers shall be:

- Sequential
- Unique within the service and category
- Never reused

Deleted requirements shall remain reserved.

Example:

```text
ID-SYS-007
```

If removed, the next requirement shall be:

```text
ID-SYS-008
```

---

# 9. Document Prefix Mapping

| Document | Prefix Example |
| -------- | -------------- |
| BRD      | BRD-001        |
| PRD      | PRD-001        |
| FRD      | FRD-001        |
| SRS      | SRS-001        |
| HLD      | HLD-001        |
| LLD      | LLD-001        |
| ADR      | ADR-001        |
| RTM      | RTM-001        |
| EPIC     | EPIC-001       |

---

# 10. Requirement Traceability

Every requirement shall be traceable.

Example:

```text
BR-012

↓

PR-008

↓

FR-025

↓

ID-SYS-004

↓

LLD-003

↓

US-021

↓

TASK-102

↓

TC-ID-014
```

---

# 11. Test Case Mapping

Each requirement shall map to at least one test case.

Example:

| Requirement | Test Case |
| ----------- | --------- |
| ID-SYS-001  | TC-ID-001 |
| ID-SYS-002  | TC-ID-002 |
| ID-SEC-001  | TC-ID-010 |
| ID-NFR-001  | TC-ID-050 |

---

# 12. Reserved Prefixes

The following prefixes are reserved for enterprise use.

| Prefix | Usage                        |
| ------ | ---------------------------- |
| ENT    | Enterprise-wide Requirements |
| PF     | Platform Foundation          |
| ID     | Identity Service             |
| BR     | Branch Service               |
| CU     | Customer Service             |
| PR     | Product Service              |
| IN     | Inventory Service            |
| OR     | Order Service                |
| BI     | Billing Service              |
| DI     | Dispatch Service             |
| NO     | Notification Service         |
| RE     | Reporting Service            |
| AU     | Audit Service                |

Additional prefixes shall be approved through the architecture governance process.

---

# 13. Compliance Rules

Every requirement shall:

- Follow this naming convention.
- Be unique.
- Have a documented source.
- Be verifiable.
- Be traceable.
- Be testable.

Requirement IDs shall never change after publication.

---

# 14. Related Standards

- documentation-compliance.md
- documentation-metadata.md
- traceability.md
- naming-conventions.md
- architecture-standards.md

---

# 15. Revision History

| Version | Date       | Description                                        |
| ------- | ---------- | -------------------------------------------------- |
| v1.0.0  | 2026-06-27 | Initial enterprise requirement identifier standard |
