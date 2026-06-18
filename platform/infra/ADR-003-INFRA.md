# ADR-003-INFRA: Git-Backed Spring Cloud Config Server Integration Strategy

## 1. Title Page

**Project Name:** StarOne Galaxy Infrastructure Platform
**Document ID:** ADR-003-INFRA
**Decision Title:** Git-Backed Spring Cloud Config Server Integration Strategy
**Repository Owner:** starone-galaxy-architecture
**Consuming Repository:** starone-galaxy-infra
**Suggested File Path:** `platform/infra/ADR-003-INFRA.md`
**Author:** Sachin Salunke
**Status:** Accepted
**Version:** v1.0.0
**Effective Date:** 2026-06-17

---

## 2. Document Metadata

| Field           | Value                                               |
| --------------- | --------------------------------------------------- |
| Document ID     | ADR-003-INFRA                                       |
| Domain          | Infrastructure Platform                             |
| Document Type   | Architecture Decision Record                        |
| Version         | v1.0.0                                              |
| Author          | Sachin Salunke                                      |
| Status          | Accepted                                            |
| Date            | 2026-06-17                                          |
| Linked Epic     | EPIC-001-INFRA                                      |
| Linked Story    | STORY-005-INFRA – Config Server Platform Foundation |
| Approval Status | Pending                                             |

---

## 3. Revision History

| Version | Date       | Author         | Description                                         |
| ------- | ---------- | -------------- | --------------------------------------------------- |
| v1.0.0  | 2026-06-17 | Sachin Salunke | Initial Config Server integration strategy decision |

---

## 4. References

* BRD-001-INFRA
* PRD-001-INFRA
* HLD-001-INFRA
* EPIC-001-INFRA
* STORY-005-INFRA
* RTM-001-INFRA

---

## 5. Sign-Off Table

| Role           | Name           | Status  |
| -------------- | -------------- | ------- |
| Platform Lead  | Sachin Salunke | Pending |
| Lead Architect | Sachin Salunke | Pending |
| Security Lead  | TBD            | Pending |

---

## 6. Scope

### 6.1 In Scope

* Spring Cloud Config Server deployment
* Git-backed configuration repository integration
* Configuration hierarchy strategy
* Multi-domain configuration management
* Environment-specific configuration resolution
* Configuration versioning and refresh mechanisms

### 6.2 Out Scope

* Configuration asset ownership
* Business service configurations
* Secrets implementation
* Vault integration
* Application-specific configuration values
* Enterprise configuration standards

---

## 7. Requirements

The platform shall:

* Provide centralized configuration management.
* Externalize application configuration from code repositories.
* Support DHS and BookShow domains.
* Support environment-specific configurations.
* Maintain configuration version history.
* Allow configuration updates without rebuilding applications.
* Enable configuration reuse across services.

---

## 8. Assumptions

* Configuration assets are owned by `starone-central-config`.
* Config Server is deployed by `starone-galaxy-infra`.
* Services are Spring Boot Config Clients.
* Configuration repository is available through Git.

---

## 9. Risks

| Risk                                 | Impact                       |
| ------------------------------------ | ---------------------------- |
| Configuration repository unavailable | Application startup failures |
| Invalid configuration commits        | Runtime failures             |
| Configuration drift                  | Environment inconsistencies  |
| Excessive configuration duplication  | Increased maintenance effort |

---

## 10. Dependencies

* Spring Cloud Config Server
* Git repository access
* Docker deployment
* Kubernetes platform
* Networking foundation
* Namespace isolation strategy

---

## 11. Traceability Matrix

| ADR           | BRD           | PRD           | Epic           | Story           |
| ------------- | ------------- | ------------- | -------------- | --------------- |
| ADR-003-INFRA | BRD-001-INFRA | PRD-001-INFRA | EPIC-001-INFRA | STORY-005-INFRA |

---

## 12. Context

### 12.1 Background

StarOne Galaxy consists of multiple independent repositories and services that require centralized, version-controlled, and environment-aware configuration management.

Configuration ownership and infrastructure ownership are intentionally separated.

### 12.2 Problem Statement

Embedding configuration inside application repositories leads to:

* Configuration duplication
* Environment inconsistencies
* Difficult configuration changes
* Poor auditability
* Deployment dependencies on configuration changes

### 12.3 Key Challenges

* Supporting multiple domains
* Maintaining environment isolation
* Preventing configuration duplication
* Enabling centralized configuration management
* Preserving repository boundaries

### 12.4 Constraints

* Configuration assets must remain outside `starone-galaxy-infra`.
* Config Server deployment belongs to `starone-galaxy-infra`.
* Configuration assets belong to `starone-central-config`.
* Services must consume configuration through Spring Cloud Config.

---

## 13. Decision

### 13.1 Selected Approach

Adopt a Git-backed Spring Cloud Config architecture where:

* `starone-galaxy-infra` owns Config Server deployment and runtime infrastructure.
* `starone-central-config` owns all configuration assets and configuration hierarchy.
* Applications consume configuration through Spring Cloud Config Client.

### 13.2 Decision Drivers

* Separation of concerns
* Configuration centralization
* Environment consistency
* Version control
* Maintainability
* Repository boundary compliance

### 13.3 Design Principles

* Externalized Configuration
* Single Source of Truth
* Infrastructure and Configuration Separation
* Git-Based Configuration Management
* Environment-Driven Configuration
* Reusable Configuration Assets

---

## 14. Alternatives Considered

### 14.1 Option A

Store configuration inside each application repository.

### 14.2 Option B

Store configuration directly inside `starone-galaxy-infra`.

### 14.3 Chosen Option

Dedicated Git-backed configuration repository (`starone-central-config`) consumed through Spring Cloud Config Server.

---

## 15. Consequences

### 15.1 Positive Consequences

* Clear repository ownership boundaries
* Centralized configuration management
* Configuration version history
* Independent configuration changes
* Simplified environment management
* Reduced configuration duplication

### 15.2 Negative Consequences

* Additional repository dependency
* Config Server availability becomes critical
* Configuration validation process required

### 15.3 Long-Term Implications

* Supports future domains
* Simplifies service onboarding
* Enables GitOps-style configuration management
* Scales with increasing service count

---

## 16. Trade-Off Analysis

| Option                      | Simplicity | Scalability | Maintainability | Boundary Compliance |
| --------------------------- | ---------- | ----------- | --------------- | ------------------- |
| Config in Application Repos | Medium     | Low         | Low             | Low                 |
| Config in Infra Repository  | High       | Medium      | Medium          | Low                 |
| Dedicated Config Repository | Medium     | High        | High            | High                |

---

## 17. Impact Analysis

### 17.1 Systems Impacted

* starone-galaxy-infra
* starone-central-config
* starone-dhs-system
* bookshow-services

### 17.2 Benefits Enabled

* Externalized configuration
* Environment consistency
* Independent configuration lifecycle
* Centralized configuration management
* Faster operational changes

---

## 18. Implementation Guidance

### Repository Responsibilities

```text
starone-galaxy-infra
└── Owns
    ├── Config Server container
    ├── Config Server deployment
    ├── Config Server networking
    └── Config Server runtime

starone-central-config
└── Owns
    ├── global/
    ├── shared/
    ├── applications/platform/
    ├── applications/dhs/
    └── applications/bookshow/
```

### Configuration Flow

```text
Developer
    ↓
Commit Configuration
    ↓
starone-central-config
    ↓
Spring Cloud Config Server
    ↓
Gateway
    ↓
DHS Services
    ↓
BookShow Services
```

### Configuration Resolution Order

```text
global/application.yml
        ↓
global/application-{profile}.yml
        ↓
applications/{domain}/{service}/{service}.yml
        ↓
applications/{domain}/{service}/{service}-{profile}.yml
        ↓
Environment Variables
```

---

## 19. Decision Summary

StarOne Galaxy adopts a Git-backed Spring Cloud Config architecture where Config Server infrastructure is owned by `starone-galaxy-infra`, configuration assets are owned by `starone-central-config`, and all applications consume externalized configuration through Spring Cloud Config Client while maintaining strict repository responsibility boundaries.
