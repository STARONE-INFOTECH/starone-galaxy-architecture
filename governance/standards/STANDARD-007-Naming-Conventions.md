# STANDARD-007 — Enterprise Naming Conventions

# Document Metadata

| Field | Description |
|---------|---------|
| Document ID | STANDARD-007 |
| Document Title | Enterprise Naming Conventions |
| Domain | Governance Standards |
| Document Type | Governance Standard |
| Repository | starone-galaxy-architecture |
| Version | 1.1 |
| Author | Sachin Salunke |
| Date | Jan 2026 |
| Status | Approved Draft |
| Linked Epic | EPIC-ARCH-001 Ecosystem Design & Governance Baseline |
| Linked Story | STORY-ARCH-001 Repository Scaffolding |
| Linked Issue | S1-I04 Publish Naming Standards and Template Baseline |
| Approval Status | Platform Architect Approved |
| Classification | Governance Controlled Document |

---

# Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0 | Jan 2026 | Sachin Salunke | Initial naming governance baseline |
| 1.1 | Jan 2026 | Sachin Salunke | Added Documentation Template Baseline governance and S1-FR-007 traceability |

---

# Sign-Off Table

| Role | Status |
|---|---|
| Platform Architect | Approved |
| Security Review | Pending |
| DevOps Governance | Pending |

---

# Purpose

This standard defines mandatory naming conventions for all repositories, architecture artifacts, services, workflows, branches, packages, event contracts, and documentation templates across the StarOne Galaxy ecosystem.

---

# Business Objective

Establish a governed naming taxonomy that:

- Reduces architectural drift
- Improves discoverability
- Enables governance automation
- Supports CI/CD validation
- Creates a reusable enterprise taxonomy
- Standardizes documentation template usage

---

# Scope

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
- Documentation templates

Applies to:

- starone-galaxy-architecture
- starone-galaxy-infra
- starone-galaxy-config
- starone-dhs-system
- starone-bookshow-system

---

# Repository Naming Standard

**Pattern**

```text
starone-{domain}-{type}
```

**Examples**

```text
starone-galaxy-infra
starone-galaxy-config
starone-galaxy-architecture
starone-dhs-system
starone-bookshow-system
```

**Rules**

- lowercase only
- kebab-case only
- no spaces
- no underscores
- no abbreviations unless approved
- domain before type

---

# Documentation Artifact Naming

**Pattern**

```text
{TYPE}-{NUMBER}-{Title}.md
```

**Examples**

```text
ADR-001-Repository-Taxonomy.md
HLD-001-Global-Ecosystem-Architecture.md
SRS-001-Documentation-Standards-Engine.md
RTM-001-Governance-Traceability.md
STANDARD-007-Naming-Conventions.md
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

## Branch Naming Standard

**Pattern**

```text
feature/<name>
hotfix/<name>
release/<version>
```

**Examples**

```text
feature/s1-i04-naming-standards
feature/c4-container-diagram
hotfix/fix-rttm-linkage
release/v1.0.0
```

**Rules**

- lowercase only
- kebab-case only
- issue/story ID prefix preferred
- no spaces
- no camelCase

---

## GitHub Workflow Naming Standard

**Pattern**

```text
domain-purpose.yml
```

**Examples**

```text
doc-validation.yml
security-compliance.yml
architecture-review.yml
lint-standards.yml
governance-validation.yml
```

**Rules**

- purpose-driven names
- no generic names such as build.yml
- lowercase only
- kebab-case only

---

## Service Naming Standard

**Pattern**

```text
<domain>-<capability>-service
```

**Examples**

```text
dhs-order-service
dhs-inventory-service
bookshow-booking-service
```

---

## Java Package Naming Standard

**Pattern**

```text
com.starone.<domain>.<service>
```

**Examples**

```text
com.starone.dhs.billing
com.starone.bookshow.booking
```

---

## Kafka Topic Naming Standard

**Pattern**

```text
<domain>.<entity>.<event>
```

**Examples**

```text
dhs.order.created
dhs.inventory.updated
bookshow.booking.confirmed
```

---

## Configuration Key Naming Standard

**Pattern**

```text
domain.service.property
```

**Example**

```text
dhs.billing.retry.maxAttempts
```

---

## Naming Rules Matrix

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

## Reserved Prefixes

### Approved Repository Prefixes

```text
starone-
dhs-
bookshow-
```

### Reserved Document Prefixes

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

No ad-hoc prefixes permitted.

---

## Governance Rules

Mandatory requirements:

- All repositories must follow naming taxonomy
- All architecture artifacts must follow approved patterns
- New services require governance-compliant naming
- Workflow files must follow standard patterns
- Branches must align with Git governance rules

Deviation from standards requires Platform Architect approval.

---

## Documentation Template Baseline

### Template Purpose

The StarOne Galaxy ecosystem maintains a standardized documentation template baseline to ensure consistency, traceability, governance compliance, and document quality.

All documentation artifacts shall be created using approved templates.

---

### Template Repository Location

```text
docs/templates/
```

---

### Approved Templates

```text
ADR_Template.md
BRD_Template.md
FRD_Template.md
HLD_Template.md
LLD_Template.md
PRD_Template.md
RTM_Template.md
SRS_Template.md
README_Global_Template.md
README_MS_Template.md
```

---

### Template Governance Rules

- All new documents must originate from approved templates.
- Template modifications require Platform Architect approval.
- Revision History is mandatory.
- Sign-Off Tables are mandatory.
- Traceability sections are mandatory where applicable.
- Mermaid diagrams remain the standard diagramming format.

---

### Template Ownership Matrix

| Template Type | Governance Owner |
|---|---|
| Architecture Templates | Platform Architect |
| Requirements Templates | Platform Architect |
| Governance Templates | Governance Board |
| README Templates | Platform Architect |

---

## Validation Requirements

The following validations may be automated in future CI/CD pipelines:

- Repository naming validation
- Branch naming validation
- Workflow filename validation
- Artifact prefix validation
- Kafka topic naming validation
- Template compliance validation

---

## Compliance Examples

### Valid

```text
ADR-001-Repository-Taxonomy.md
feature/s1-i04-naming-standards
dhs-order-service
dhs.order.created
```

### Invalid

```text
repo_final
build.yml
MyBranch
orderservice
```

---

## Future Governance Automation

Future controls may include:

- GitHub Actions naming validation
- Branch policy enforcement
- Artifact naming linting
- Kafka topic governance validation
- Repository provisioning templates
- Template compliance validation

---

## Related Standards

| Standard | Purpose |
|---|---|
| STANDARD-006 | CODEOWNERS Governance |
| STANDARD-008 | Contribution Governance |
| CONTRIBUTING.md | Contribution Governance |
| ADR-001 | Repository Taxonomy Decision |
| HLD-001 | Platform Architecture Baseline |

---

## Requirement Traceability Matrix (RTM)

| Requirement ID | Requirement Description | Coverage Section |
|---|---|---|
| S1-FR-004 | Define repository naming conventions | Repository Naming through Governance Rules |
| S1-FR-007 | Establish documentation template repository baseline | Documentation Template Baseline |

Coverage Status: Complete

---

## Traceability

| Epic | Story | Issue | Requirement |
|---|---|---|---|
| EPIC-ARCH-001 | STORY-ARCH-001 | S1-I04 | S1-FR-004 |
| EPIC-ARCH-001 | STORY-ARCH-001 | S1-I04 | S1-FR-007 |

Coverage: 100%

---

## Approval

| Role | Status |
|---|---|
| Platform Architect | Approved |
| Security Review | Pending |
| DevOps Governance | Pending |

---

**Enterprise Naming Governance — Enabling Consistent Platform Engineering Across the StarOne Galaxy Ecosystem**