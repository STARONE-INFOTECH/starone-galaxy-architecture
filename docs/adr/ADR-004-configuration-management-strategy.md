# ADR-004: Configuration Management Strategy — Centralized Config with Domain Isolation

---

# 1. Title Page

| Field       | Value                             |
| ----------- | --------------------------------- |
| Document ID | ADR-004                           |
| Project     | StarOne Galaxy                    |
| Decision    | Configuration Management Strategy |
| Author      | Sachin Salunke                    |
| Date        | Jan 2026                          |
| Status      | Accepted                          |

---

# 2. Context

StarOne Galaxy is a **multi-domain distributed system** with multiple independent services across domains:

- DHS
- Bookshow
- SportStats
- VaultIron

Each service requires:

- Environment-specific configuration
- Secure secret management
- Consistent configuration governance
- Flexibility without cross-domain interference

---

## 2.1 Problem Statement

```text
How should configuration be managed across multiple domains
while ensuring security, scalability, and strict domain isolation?
```

---

## 2.2 Key Challenges

- Avoiding configuration duplication
- Managing environment-specific configs (dev, staging, prod)
- Securing sensitive data (passwords, keys)
- Preventing config leakage across domains
- Ensuring dynamic configuration updates

---

# 3. Decision

StarOne Galaxy shall implement a centralized configuration management platform that provides:

• Centralized configuration storage
• Environment isolation
• Domain isolation
• Secure secret management
• Version-controlled configuration
• Dynamic configuration distribution

The initial implementation shall use:

Spring Cloud Config Server

with

starone-galaxy-central-config

as the Git-backed configuration repository.

---

## 3.1 Centralized Config Store

- All configurations will be stored in:

```text
starone-galaxy-central-config repository
```

- Managed through the enterprise configuration platform.

- The current implementation uses Spring Cloud Config Server.
- Future implementations may use another centralized configuration technology without changing this architectural decision.

---

## 3.2 Domain-Level Isolation

Configuration assets shall be logically isolated by business domain. The implementation mechanism is defined within the Infrastructure Repository.

Examples are defined in:

docs/configuration-management/CONFIGURATION_CONVENTIONS.md

---

## 3.3 Environment Separation

Configuration shall support environment-specific overrides.

Implementation is defined by the Infrastructure Repository.


---

## 3.4 Secure Configuration (Encryption)

Sensitive configuration values shall be encrypted using the enterprise-approved encryption mechanism.

The initial implementation uses Spring Cloud Config encryption.

Examples:

- Database passwords
- API keys
- Tokens

---

## 3.5 Runtime Configuration Injection

- Services shall obtain configuration from the enterprise configuration platform during startup and refresh events.
- The current implementation uses Spring Cloud Config Server.
- No hardcoded configuration inside services

---

## 3.6 Configuration Access Rules

```text
✔ Services can only access their own config
✔ Config access is read-only
✔ No direct modification at runtime
```

---

# 4. Traceability

## 4.1 Parent Traceability (Backward)

| Source | Reference |
|--------|-----------|
| Enterprise Vision | StarOne Galaxy Ecosystem Charter (SGE) |
| Related ADR | ADR-001 Repository Strategy |
| Related ADR | ADR-002 Architecture Style |
| Related ADR | ADR-003 Domain Isolation |

### Parent Relationship

```text
StarOne Galaxy Ecosystem Charter
            │
            ▼
ADR-001 Repository Strategy
            │
            ▼
ADR-003 Domain Isolation
            │
            ▼
ADR-004 Configuration Management Strategy
```

---

## 4.2 Child Traceability (Forward)

| Target | Reference |
|---------|-----------|
| Infrastructure HLD | HLD-INFRA-001 Platform Configuration Architecture |
| Infrastructure LLD | LLD-INFRA-001 Spring Cloud Configuration Implementation |
| Infrastructure Repository | starone-galaxy-infra |
| Configuration Repository | starone-galaxy-central-config |
| Platform Component | Spring Cloud Config Server |
| Platform Component | Configuration Management Framework |
| Consumer | All StarOne Services |

### Forward Relationship

```text
ADR-004
    │
    ├── HLD-INFRA-001
    │       │
    │       ▼
    │   LLD-INFRA-001
    │       │
    │       ▼
    │   starone-galaxy-infra
    │       │
    │       ▼
    │   Spring Cloud Config Server
    │
    └──────────────► starone-galaxy-central-config
                        │
                        ▼
                 Configuration Assets
                        │
                        ▼
              All Platform & Business Services
```

---

## 4.3 RTM Relationship

| Parent Artifact | Current Artifact | Child Artifact |
|-----------------|------------------|----------------|
| StarOne Galaxy Ecosystem Charter | ADR-004 | HLD-INFRA-001 |
| ADR-003 Domain Isolation | ADR-004 | LLD-INFRA-001 |
| ADR-001 Repository Strategy | ADR-004 | starone-galaxy-infra |
| ADR-002 Architecture Style | ADR-004 | starone-galaxy-central-config |

---

# 5. Repository Responsibilities

| Repository     | Responsibility                                 |
| -------------- | ---------------------------------------------- |
| Architecture   | Defines configuration governance and standards |
| Infrastructure | Implements configuration platform              |
| Central Config | Stores configuration assets                    |
| Applications   | Consume centralized configuration              |

---

# 6. Alternatives Considered

---

## 6.1 ❌ Option 1: Local Configuration per Service

**Description:**
Each service maintains its own config files

**Rejected Because:**

- Configuration duplication
- Hard to manage across environments
- No central governance

---

## 6.2 ❌ Option 2: Environment Variables Only

**Description:**
All configs managed via environment variables

**Rejected Because:**

- Difficult to manage at scale
- No version control
- Poor visibility

---

## 6.3 ❌ Option 3: Shared Configuration Across Domains

**Description:**
Common config shared across all domains

**Rejected Because:**

- Violates domain isolation
- Risk of unintended dependency
- Security concerns

---

## 6.4 ✅ Option 4: Centralized Config with Isolation (Chosen)

**Description:**
Central config repository with domain-specific separation and encryption

**Reasons:**

- Central governance
- Strong security
- Domain isolation maintained
- Easy environment management

---

# 7. Consequences

---

## 7.1 ✅ Positive

- Centralized control of configuration
- Improved security via encryption
- Simplified environment management
- Reduced duplication
- Better traceability (Git-based)

---

## 7.2 ⚠️ Negative

- Dependency on Config Server availability
- Initial setup complexity
- Requires secure key management

---

# 8. Trade-offs

| Trade-off                   | Decision                  |
| --------------------------- | ------------------------- |
| Decentralization vs Control | Chose centralized control |
| Flexibility vs Governance   | Balanced with isolation   |
| Simplicity vs Security      | Chose security            |

---

# 9. Impact

---

## 9.1 Affected Repositories

- starone-galaxy-infra
- starone-galaxy-central-config
- starone-dhs-platform
- starone-bookshow-platform
- future platform services

---

## 9.2 Enables:

- Dynamic configuration updates
- Secure secret management
- Standardized configuration model

---

# 10. Rules Enforced

```text
1. All configuration must reside in central config repository
2. Sensitive data must be encrypted
3. No hardcoded configuration in services
4. Config must be isolated per domain
5. Environment-specific configs must be maintained
```

---


# 11. Decision Summary

```text
StarOne Galaxy adopts a centralized configuration management strategy
using Spring Cloud Config with strict domain isolation and encrypted
secrets to ensure secure, scalable, and manageable configuration handling.
```

---

# 12. Status

```text
ACCEPTED — This configuration model is mandatory across all services
```

---
