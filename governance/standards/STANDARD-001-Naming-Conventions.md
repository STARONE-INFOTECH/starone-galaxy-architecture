# STANDARD-001 — Enterprise Naming Conventions

> **Standard ID:** STANDARD-001  
> **Title:** Enterprise Naming Conventions  
> **Repository:** starone-galaxy-architecture  
> **Domain:** Governance Standards  
> **Author:** Sachin Salunke  
> **Version:** 1.0  
> **Date:** Jan 2026  
> **Status:** Approved Draft  

---

# Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0 | Jan 2026 | Sachin Salunke | Initial naming governance baseline |

---

# 1. Purpose

This standard defines mandatory naming conventions for all repositories, architecture artifacts, services, workflows, branches, packages, and event contracts across the StarOne Galaxy ecosystem.

The purpose of this standard is to:

- Establish architectural consistency
- Reduce taxonomy drift
- Improve discoverability
- Support governance automation
- Enable CI/CD validation rules
- Standardize cross-domain engineering practices

---

# 2. Scope

This standard applies to:

- Repositories
- Documentation artifacts
- Services/modules
- Branches
- GitHub workflows
- Java packages
- Kafka topics
- Configuration keys
- Runtime domains

Applies to:

- starone-galaxy-infra
- starone-galaxy-config
- starone-galaxy-architecture
- starone-dhs-system
- bookshow-system

---

# 3. Repository Naming Standard

## Repository Naming Pattern

```text
starone-{domain}-{type}
```

## Repository Examples

```text
starone-galaxy-infra
starone-galaxy-config
starone-galaxy-architecture
starone-dhs-system
starone-bookshow-system
```

## Repository Naming Rules

- lowercase only
- kebab-case only
- no spaces
- no underscores
- no abbreviations unless approved
- domain before type

---

# 4. Documentation Artifact Naming

## Artifact Naming Pattern

```text
{TYPE}-{NUMBER}-{Title}.md
```

## Artifact Examples

```text
ADR-001-Repository-Taxonomy.md
HLD-001-Global-Ecosystem-Architecture.md
SRS-001-Documentation-Standards-Engine.md
RTM-001-Governance-Traceability.md
STANDARD-001-Naming-Conventions.md
```

## Approved Prefixes

| Prefix | Meaning |
|---|---|
| ADR | Architecture Decision Record |
| HLD | High Level Design |
| LLD | Low Level Design |
| SRS | Software Requirements Specification |
| BRD | Business Requirements Document |
| PRD | Product Requirements Document |
| RTM | Requirement Traceability Matrix |
| STANDARD | Governance Standard |
| EPIC | Agile Epic |
| STORY | Agile Story |
| ISSUE | Agile Issue |
| C4 | C4 Architecture Models |

---

# 5. Branch Naming Standard

## Branch Naming Pattern

```text
feature/<name>
hotfix/<name>
release/<version>
```

## Branch Examples

```text
feature/s1-i04-naming-standards
feature/c4-container-diagram
hotfix/fix-rttm-linkage
release/v1.0.0
```

##  Branch Naming Rules

- lowercase only
- kebab-case only
- issue/story ID prefix preferred
- no spaces
- no camelCase

---

# 6. GitHub Workflow Naming Standard

## GitHub Workflow Naming Pattern

```text
domain-purpose.yml
```

## GitHub Workflow Examples

```text
doc-validation.yml
security-compliance.yml
architecture-review.yml
lint-standards.yml
```

## GitHub Workflow Naming Rules

- purpose-driven names
- no generic names like build.yml
- lowercase only
- kebab-case only

---

# 7. Service Naming Standard

## Service Naming Pattern

```text
<domain>-<capability>-service
```

## Service Examples

```text
dhs-order-service
dhs-inventory-service
bookshow-booking-service
```

## Service Naming Rules

- domain prefix mandatory
- service suffix mandatory
- bounded-context aligned

---

# 8. Java Package Naming Standard

## Java Package Naming Pattern

```text
com.starone.<domain>.<service>
```

## Java Package Examples

```text
com.starone.dhs.billing
com.starone.bookshow.booking
```

---

# 9. Kafka Topic Naming Standard

## Kafka Topic Naming Pattern

```text
<domain>.<entity>.<event>
```

## Kafka Topic Examples

```text
dhs.order.created
dhs.inventory.updated
bookshow.booking.confirmed
```

## Kafka Topic Naming Rules

- lowercase only
- dot notation only
- event suffix mandatory
- no environment names in topics

---

# 10. Configuration Key Naming Standard

## Configuration Key Naming Pattern

```text
domain.service.property
```

## Configuration Key Example

```text
dhs.billing.retry.maxAttempts
```

---

# 11. Naming Rules Matrix

| Asset | Convention |
|---|---|
| Repositories | kebab-case |
| Artifacts | Prefix-ID-Title |
| Branches | type/name |
| Services | domain-capability-service |
| Packages | dot notation |
| Topics | domain.entity.event |
| Config Keys | domain.service.property |

---

# 12. Reserved Prefixes

## Approved Repository Prefixes

```text
starone-
dhs-
bookshow-
```

## Reserved Document Prefixes

```text
ADR
HLD
LLD
SRS
BRD
PRD
RTM
STANDARD
C4
EPIC
STORY
ISSUE
```

No ad hoc prefixes permitted.

---

# 13. Governance Rules

Mandatory requirements:

- All repositories must follow naming taxonomy
- All architecture artifacts must follow approved patterns
- New services require governance-compliant naming
- Workflow files must follow standard patterns
- Branches must align with Git governance rules

Deviation from standards requires architecture approval.

---

# 14. Validation Requirements

The following validations will later be automated via CI/CD:

- Repository naming validation
- Branch naming validation
- Workflow filename validation
- Artifact prefix validation
- Kafka topic naming validation

---

# 15. Compliance Examples

## Valid Examples

```text
ADR-001-Repository-Taxonomy.md
feature/s1-i04-naming-standards
dhs-order-service
dhs.order.created
```

## Invalid Examples

```text
repo_final
build.yml
MyBranch
orderservice
```

---

# 16. Future Governance Automation

Future automation controls will include:

- GitHub Actions naming validation
- Branch policy enforcement
- Artifact naming linting
- Kafka topic governance validation
- Repository provisioning templates

---

# 17. Related Standards

| Standard | Purpose |
|---|---|
| CONTRIBUTING.md | Contribution governance |
| CODEOWNERS | Ownership governance |
| ADR-001 | Repository taxonomy decisions |
| HLD-001 | Platform architecture baseline |

---

# 18. Approval

| Role | Status |
|---|---|
| Platform Architect | Approved |
| Security Review | Pending |
| DevOps Governance | Pending |

---

# 19. Traceability

| Epic | Story | Issue | Requirement |
|---|---|---|---|
| EPIC-ARCH-001 | STORY-ARCH-001 | S1-I04 | S1-FR-004 |

Coverage: 100%

---

Enterprise Naming Governance — Enabling Consistent Platform Engineering.