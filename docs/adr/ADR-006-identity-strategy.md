# ADR-006: Identity Strategy — Domain-Isolated Authentication Model

---

## Title Page

| Field | Value |
|---|---|
Document ID | ADR-006 |
Project | StarOne Galaxy |
Decision | Identity & Authentication Strategy |
Author | Sachin Salunke |
Date | Jan 2026 |
Status | Accepted |

---

## 1. Context

StarOne Galaxy consists of multiple **independent domains**:

- DHS (Enterprise OMS)  
- Bookshow (Consumer Platform)  
- SportStats (Analytics System)  
- VaultIron (Security System)  

Each domain serves **different user types**, use cases, and security requirements.

---

### Problem Statement

```text
Should identity and authentication be centralized across all domains
or managed independently within each domain?
```

---

### Key Challenges

- Maintaining domain isolation  
- Supporting different user types per domain  
- Ensuring secure authentication and authorization  
- Avoiding unnecessary coupling between domains  
- Supporting future scalability  

---

## 2. Decision

StarOne Galaxy will adopt a:

```text
Domain-Isolated Identity Strategy (Decentralized Authentication)
```

---

## 2.1 Identity Model

Each domain will:

- Manage its own users  
- Implement its own authentication system  
- Maintain its own user database  

---

## 2.2 Authentication Mechanism

- JWT-based authentication per domain  
- Tokens are **domain-scoped**  
- No shared authentication token across domains  

---

## 2.3 Authorization Model

- Role-Based Access Control (RBAC) per domain  
- Roles are domain-specific  

Example:

```text
DHS → Sales, Admin, Finance
Bookshow → Customer
VaultIron → Secure User
```

---

## 2.4 No Central Identity Provider (Initial Phase)

- No centralized SSO (Single Sign-On)  
- No shared identity service across domains  

---

## 2.5 API Gateway Security

- Each domain gateway validates its own JWT  
- No cross-domain token validation  

---

## 2.6 Future Extensibility

The architecture allows future evolution to:

```text
Central Identity Provider (SSO)
```

But only if:

- Business requires unified identity  
- Cross-domain user experience is needed  

---

## 3. Alternatives Considered

---

### ❌ Option 1: Centralized Identity (SSO)

**Description:**
Single identity provider for all domains

**Rejected Because:**

- Violates domain isolation  
- Creates single point of failure  
- Increases system complexity  
- Unnecessary for independent applications  

---

### ❌ Option 2: Shared User Database

**Description:**
All domains share a common user database

**Rejected Because:**

- Breaks domain boundaries  
- Security risks  
- Tight coupling  

---

### ❌ Option 3: Token Sharing Across Domains

**Description:**
Single JWT used across all domains

**Rejected Because:**

- Security risks  
- Lack of domain-level control  
- Violates isolation  

---

### ✅ Option 4: Domain-Isolated Identity (Chosen)

**Description:**
Each domain manages its own identity and authentication

**Reasons:**

- Strong domain isolation  
- Better security control  
- Independent evolution  
- Simpler implementation  

---

## 4. Consequences

---

### ✅ Positive

- Strong security boundaries  
- Independent user management  
- Reduced system complexity  
- No cross-domain dependency  
- Easier maintenance  

---

### ⚠️ Negative

- No unified login experience  
- Duplicate users across domains  
- Future migration to SSO may require effort  

---

## 5. Trade-offs

| Trade-off | Decision |
|---|---|
Convenience vs Isolation | Chose isolation |
Centralization vs Independence | Chose independence |
User Experience vs Security | Balanced toward security |

---

## 6. Impact

---

### Affects:

- Security architecture  
- API Gateway design  
- User management systems  
- Authentication flows  

---

### Enables:

- Independent domain security  
- Flexible identity evolution  
- Simplified initial implementation  

---

## 7. Rules Enforced

```text
1. Each domain must manage its own identity system
2. No shared authentication across domains
3. JWT tokens must be domain-scoped
4. RBAC must be implemented per domain
5. No cross-domain token validation
```

---

## 8. Related Artifacts

- ADR-002 Architecture Style  
- ADR-003 Domain Isolation  
- ADR-004 Config Strategy  
- ADR-005 Messaging Strategy  
- SRS-001 StarOne Galaxy  
- HLD-001 Global Architecture  

---

## 9. Decision Summary

```text
StarOne Galaxy adopts a domain-isolated identity strategy where each domain
manages its own authentication and authorization, ensuring strong security,
independence, and scalability.
```

---

## 10. Status

```text
ACCEPTED — This identity model is mandatory for all domains
```

---