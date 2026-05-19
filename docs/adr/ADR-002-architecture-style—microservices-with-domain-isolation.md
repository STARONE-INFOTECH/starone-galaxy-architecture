# ADR-002: Architecture Style — Microservices with Domain Isolation

---

## Title Page

| Field | Value |
|---|---|
Document ID | ADR-002 |
Project | StarOne Galaxy |
Decision | Architecture Style Selection |
Author | Sachin Salunke |
Date | Jan 2026 |
Status | Accepted |

---

## 1. Context

StarOne Galaxy is designed as a **multi-domain ecosystem** consisting of independent systems:

- DHS (Enterprise OMS)  
- Bookshow (Consumer Platform)  
- SportStats (Analytics System)  
- VaultIron (Security System)  

The platform must support:

- Independent development and deployment  
- Domain-level isolation  
- Scalability across multiple systems  
- Governance and standardization  

---

### Problem Statement

```text
What architectural style should be adopted to ensure scalability,
flexibility, and strict domain isolation across the ecosystem?
```

---

### Key Considerations

- Multiple independent domains  
- Need for scalability and resilience  
- Avoiding tight coupling between systems  
- Supporting platform-driven infrastructure  
- Enabling long-term evolution  

---

## 2. Decision

StarOne Galaxy will adopt a:

```text
Microservices Architecture combined with Domain-Driven Isolation
```

---

### 2.1 Microservices Architecture

Each domain will be composed of **independent, loosely coupled services** that:

- Encapsulate business capabilities  
- Are independently deployable  
- Communicate via well-defined interfaces (REST / Events)  

---

### 2.2 Domain Isolation

The system will enforce strict domain boundaries:

- No shared database across domains  
- No direct dependency between domains  
- Each domain manages its own services, data, and lifecycle  

---

### 2.3 Platform-Based Architecture

All domains will run on a **shared platform (Control Plane)** that provides:

- Kubernetes orchestration  
- CI/CD pipelines  
- Centralized configuration  

This ensures:

```text
Shared infrastructure + Isolated domain behavior
```

---

### 2.4 Communication Model

- Default: **Synchronous REST communication**  
- Event-driven (Kafka): **only where required (e.g., DHS workflows)**  
- No forced cross-domain communication  

---

## 3. Alternatives Considered

---

### ❌ Option 1: Monolithic Architecture

**Description:**
Single application containing all domains

**Rejected Because:**

- No scalability  
- Tight coupling  
- Difficult to maintain  
- Limits independent evolution  

---

### ❌ Option 2: Distributed Monolith

**Description:**
Multiple services but tightly coupled

**Rejected Because:**

- Hidden dependencies  
- Difficult to scale independently  
- Violates domain isolation principles  

---

### ❌ Option 3: Event-Driven Everywhere

**Description:**
All services communicate via Kafka

**Rejected Because:**

- Over-engineering  
- Increased complexity  
- Not suitable for all domains (e.g., VaultIron)  

---

### ✅ Option 4: Microservices + Domain Isolation (Chosen)

**Description:**
Independent microservices grouped by domain with controlled communication

**Reasons:**

- High scalability  
- Strong isolation  
- Flexible communication patterns  
- Aligns with platform architecture  

---

## 4. Consequences

---

### ✅ Positive

- Independent scalability per domain  
- Clear separation of concerns  
- Improved fault isolation  
- Flexibility in choosing communication patterns  
- Enables parallel development  

---

### ⚠️ Negative

- Increased operational complexity  
- Requires strong governance  
- More infrastructure overhead  

---

## 5. Trade-offs

| Trade-off | Decision |
|---|---|
Simplicity vs Scalability | Chose scalability |
Coupling vs Isolation | Chose isolation |
Uniformity vs Flexibility | Chose flexible communication |

---

## 6. Impact

---

### Affects:

- System architecture (HLD)  
- Service design (LLD)  
- Integration strategy  
- Deployment model  

---

### Enables:

- Domain-driven design  
- Platform engineering model  
- Independent service evolution  

---

## 7. Architecture Principles Enforced

- Domain isolation  
- Database per service  
- API-first design  
- Stateless services  
- Loose coupling  

---

## 8. Related Artifacts

- ADR-001 Repository Strategy  
- SRS-001 StarOne Galaxy  
- HLD-001 Global Architecture  

---

## 9. Decision Summary

```text
StarOne Galaxy adopts a microservices architecture with strict domain isolation,
running on a shared platform to ensure scalability, flexibility, and governance.
```

---

## 10. Status

```text
ACCEPTED — This architecture style is mandatory for all domains
```

---