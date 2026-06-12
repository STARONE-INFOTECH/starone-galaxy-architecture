# ADR-004: Configuration Management Strategy — Centralized Config with Domain Isolation

---

## Title Page

| Field       | Value                             |
| ----------- | --------------------------------- |
| Document ID | ADR-004                           |
| Project     | StarOne Galaxy                    |
| Decision    | Configuration Management Strategy |
| Author      | Sachin Salunke                    |
| Date        | Jan 2026                          |
| Status      | Accepted                          |

---

## 1. Context

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

### Problem Statement

```text
How should configuration be managed across multiple domains
while ensuring security, scalability, and strict domain isolation?
```

---

### Key Challenges

- Avoiding configuration duplication
- Managing environment-specific configs (dev, staging, prod)
- Securing sensitive data (passwords, keys)
- Preventing config leakage across domains
- Ensuring dynamic configuration updates

---

## 2. Decision

StarOne Galaxy will adopt a:

```text
Centralized Configuration Management using Spring Cloud Config
with strict domain-level isolation and encryption
```

---

### 2.1 Centralized Config Store

- All configurations will be stored in:

```text
starone-galaxy-config repository
```

- Managed via **Spring Cloud Config Server**

---

### 2.2 Domain-Level Isolation

- Configurations are separated per domain:

```text
dhs-service.yml
bookshow-service.yml
sportstats-service.yml
vaultiron-service.yml
```

- No domain can access another domain’s configuration

---

### 2.3 Environment Separation

Configurations are maintained per environment:

```text
application-dev.yml
application-staging.yml
application-prod.yml
```

---

### 2.4 Secure Configuration (Encryption)

- Sensitive data must be encrypted using:

```text
JCE Encryption (Spring Cloud Config)
```

Examples:

- Database passwords
- API keys
- Tokens

---

### 2.5 Runtime Configuration Injection

- Services fetch configuration at runtime from Config Server
- No hardcoded configuration inside services

---

### 2.6 Configuration Access Rules

```text
✔ Services can only access their own config
✔ Config access is read-only
✔ No direct modification at runtime
```

---

## 3. Alternatives Considered

---

### ❌ Option 1: Local Configuration per Service

**Description:**
Each service maintains its own config files

**Rejected Because:**

- Configuration duplication
- Hard to manage across environments
- No central governance

---

### ❌ Option 2: Environment Variables Only

**Description:**
All configs managed via environment variables

**Rejected Because:**

- Difficult to manage at scale
- No version control
- Poor visibility

---

### ❌ Option 3: Shared Configuration Across Domains

**Description:**
Common config shared across all domains

**Rejected Because:**

- Violates domain isolation
- Risk of unintended dependency
- Security concerns

---

### ✅ Option 4: Centralized Config with Isolation (Chosen)

**Description:**
Central config repository with domain-specific separation and encryption

**Reasons:**

- Central governance
- Strong security
- Domain isolation maintained
- Easy environment management

---

## 4. Consequences

---

### ✅ Positive

- Centralized control of configuration
- Improved security via encryption
- Simplified environment management
- Reduced duplication
- Better traceability (Git-based)

---

### ⚠️ Negative

- Dependency on Config Server availability
- Initial setup complexity
- Requires secure key management

---

## 5. Trade-offs

| Trade-off                   | Decision                  |
| --------------------------- | ------------------------- |
| Decentralization vs Control | Chose centralized control |
| Flexibility vs Governance   | Balanced with isolation   |
| Simplicity vs Security      | Chose security            |

---

## 6. Impact

---

### Affects:

- Infrastructure setup (Config Server)
- Service startup configuration
- Security model
- Deployment pipelines

---

### Enables:

- Dynamic configuration updates
- Secure secret management
- Standardized configuration model

---

## 7. Rules Enforced

```text
1. All configuration must reside in central config repository
2. Sensitive data must be encrypted
3. No hardcoded configuration in services
4. Config must be isolated per domain
5. Environment-specific configs must be maintained
```

---

## 8. Related Artifacts

- ADR-001 Repository Strategy
- ADR-002 Architecture Style
- ADR-003 Domain Isolation
- SRS-001 StarOne Galaxy
- HLD-001 Global Architecture

---

## 9. Decision Summary

```text
StarOne Galaxy adopts a centralized configuration management strategy
using Spring Cloud Config with strict domain isolation and encrypted
secrets to ensure secure, scalable, and manageable configuration handling.
```

---

## 10. Status

```text
ACCEPTED — This configuration model is mandatory across all services
```

---
