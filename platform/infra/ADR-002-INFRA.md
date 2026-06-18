# ADR-002-INFRA: Namespace Isolation Strategy

## 1. Title Page

**Project Name:** StarOne Galaxy Infrastructure Platform
**Document ID:** ADR-002-INFRA
**Decision Title:** Namespace Isolation Strategy
**Repository Owner:** starone-galaxy-architecture
**Consuming Repository:** starone-galaxy-infra
**Suggested File Path:** `platform/infra/ADR-002-INFRA.md`
**Author:** Sachin Salunke
**Status:** Accepted
**Version:** v1.0.0
**Effective Date:** 2026-06-17

---

## 2. Document Metadata

| Field           | Value                                   |
| --------------- | --------------------------------------- |
| Document ID     | ADR-002-INFRA                           |
| Domain          | Infrastructure Platform                 |
| Document Type   | Architecture Decision Record            |
| Version         | v1.0.0                                  |
| Author          | Sachin Salunke                          |
| Status          | Accepted                                |
| Date            | 2026-06-17                              |
| Linked Epic     | EPIC-001-INFRA                          |
| Linked Story    | STORY-006-INFRA – Networking Foundation |
| Approval Status | Pending                                 |

---

## 3. Revision History

| Version | Date       | Author         | Description                                   |
| ------- | ---------- | -------------- | --------------------------------------------- |
| v1.0.0  | 2026-06-17 | Sachin Salunke | Initial namespace isolation strategy decision |

---

## 4. References

* BRD-001-INFRA
* PRD-001-INFRA
* HLD-001-INFRA
* EPIC-001-INFRA
* STORY-006-INFRA
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

* Kubernetes namespace strategy
* Domain isolation approach
* Shared platform services placement
* Resource boundary definition
* Network segmentation approach
* Environment-level namespace organization
* Future domain scalability

### 6.2 Out Scope

* Kubernetes deployment manifests
* Ingress implementation
* Network policies implementation
* RBAC implementation details
* Service mesh implementation
* Container image strategy
* CI/CD implementation

---

## 7. Requirements

The platform shall:

* Isolate DHS and BookShow workloads.
* Prevent resource conflicts between domains.
* Support independent deployments.
* Support independent scaling.
* Reduce operational blast radius.
* Enable future domain expansion.
* Support shared platform services.

---

## 8. Assumptions

* DHS and BookShow are independent domains.
* Additional domains may be introduced.
* Kubernetes is the primary orchestration platform.
* Shared platform services will be consumed by multiple domains.

---

## 9. Risks

| Risk                          | Impact                           |
| ----------------------------- | -------------------------------- |
| Shared namespace usage        | Resource conflicts               |
| Cross-domain deployments      | Operational coupling             |
| Namespace sprawl              | Increased operational complexity |
| Misconfigured access controls | Security exposure                |

---

## 10. Dependencies

* Kubernetes Platform Foundation
* Networking Foundation
* Observability Foundation
* Config Server Platform Foundation
* Infrastructure Repository Foundation

---

## 11. Traceability Matrix

| ADR           | BRD           | PRD           | Epic           | Story           |
| ------------- | ------------- | ------------- | -------------- | --------------- |
| ADR-002-INFRA | BRD-001-INFRA | PRD-001-INFRA | EPIC-001-INFRA | STORY-006-INFRA |

---

## 12. Context

### 12.1 Background

StarOne Galaxy hosts multiple business domains that must operate independently while sharing common infrastructure capabilities. The platform requires clear operational boundaries to support isolated deployments, scaling, and maintenance activities.

### 12.2 Problem Statement

Running DHS and BookShow workloads in shared namespaces can lead to:

* Resource contention
* Cross-domain operational impact
* Increased security risks
* Complex troubleshooting
* Deployment coupling
* Reduced scalability

### 12.3 Key Challenges

* Maintaining domain independence
* Supporting shared infrastructure services
* Reducing deployment blast radius
* Simplifying operations
* Enabling future platform expansion

### 12.4 Constraints

* Kubernetes is the standard orchestration platform.
* Domains must remain operationally independent.
* Shared services must be reusable.
* Namespace strategy must remain simple and scalable.

---

## 13. Decision

### 13.1 Selected Approach

Adopt a **Domain-Based Namespace Isolation Strategy** where each business domain receives dedicated namespaces and shared infrastructure services are deployed separately.

### 13.2 Decision Drivers

* Isolation
* Security
* Scalability
* Fault containment
* Independent deployments
* Operational simplicity

### 13.3 Design Principles

* Domain First
* Least Privilege
* Fault Isolation
* Independent Scaling
* Shared Services Separation
* Infrastructure Reusability

---

## 14. Alternatives Considered

### 14.1 Option A

Single shared namespace for all workloads.

### 14.2 Option B

Namespace per service.

### 14.3 Chosen Option

Namespace per domain with dedicated shared namespaces.

```text id="56qk6u"
Namespaces
├── dhs
├── bookshow
└── galaxy-admin
```

### Domain Allocation

```text id="1ehcqt"
dhs
├── gateway
├── eureka
├── domain-services

bookshow
├── gateway
├── eureka
├── microservices

galaxy-admin
├── config-server
├── observability
├── shared-platform-services
```

---

## 15. Consequences

### 15.1 Positive Consequences

* Independent domain deployments
* Reduced operational blast radius
* Better resource management
* Easier troubleshooting
* Independent scaling
* Improved security boundaries

### 15.2 Negative Consequences

* Additional namespace management
* Cross-namespace communication complexity
* Additional monitoring configuration

### 15.3 Long-Term Implications

* Supports future domains without redesign
* Enables multi-team ownership
* Simplifies production operations
* Provides scalable platform boundaries

---

## 16. Trade-Off Analysis

| Option                | Simplicity | Isolation | Scalability | Maintainability |
| --------------------- | ---------- | --------- | ----------- | --------------- |
| Shared Namespace      | High       | Low       | Low         | Low             |
| Namespace per Service | Low        | High      | Medium      | Low             |
| Namespace per Domain  | High       | High      | High        | High            |

---

## 17. Impact Analysis

### 17.1 Systems Impacted

* starone-galaxy-infra
* starone-central-config
* starone-dhs-system
* bookshow-services

### 17.2 Benefits Enabled

* Independent release cycles
* Safer deployments
* Domain ownership boundaries
* Simplified operations
* Better scalability
* Future extensibility

---

## 18. Implementation Guidance

1. Create namespaces:

   * `dhs`
   * `bookshow`
   * `galaxy-admin`

2. Deploy shared platform services into `galaxy-admin`.

3. Deploy DHS services into `dhs`.

4. Deploy BookShow services into `bookshow`.

5. Configure namespace-level quotas and limits.

6. Configure cross-namespace communication rules.

7. Configure namespace monitoring and observability.

---

## 19. Decision Summary

StarOne Galaxy adopts a domain-based namespace isolation strategy consisting of dedicated namespaces for DHS, BookShow, and shared platform services. This approach provides strong isolation, independent deployments, simplified operations, and long-term scalability while maintaining reusable shared infrastructure capabilities.
