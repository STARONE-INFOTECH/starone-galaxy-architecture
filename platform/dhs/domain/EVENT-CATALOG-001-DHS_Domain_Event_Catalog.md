# EVENT-CATALOG-001: DHS Domain Event Catalog

## Document Header

| Attribute          | Value                                    |
| ------------------ | ---------------------------------------- |
| Document ID        | DHS-EVENT-CATALOG-001                    |
| Project            | Distributed Hub and Sales (DHS) Platform |
| Repository         | starone-dhs-system                       |
| Version            | v1.0                                     |
| Status             | Draft                                    |
| Owner              | Solution Architecture Team               |
| Architecture Style | Event-Driven Microservices Architecture  |
| Messaging Platform | Apache Kafka                             |
| Date               | 2026-06-20                               |

---

# 1. Purpose

This document defines the domain events exchanged between independently deployable DHS microservices.

The objective of this catalog is to:

* Establish event contracts
* Define event ownership
* Enable service autonomy
* Support Saga-based distributed transactions
* Prevent direct database coupling
* Provide event traceability
* Standardize event naming conventions

---

# 2. Event Principles

## Ownership

Every event has exactly one publisher.

## Immutability

Published events cannot be modified.

## Autonomy

Services react to events independently.

## Eventual Consistency

Cross-service workflows achieve consistency asynchronously.

## Correlation

Every event carries correlation metadata.

---

# 3. Standard Event Envelope

```json
{
  "eventId": "uuid",
  "eventName": "OrderCreated",
  "eventVersion": "v1",
  "eventTimestamp": "2026-06-20T10:15:30Z",
  "sourceService": "order-service",
  "correlationId": "uuid",
  "traceId": "uuid",
  "payload": {}
}
```

---

# 4. Event Naming Convention

```text
<Entity><Action>

Examples:
UserCreated
BranchActivated
OrderCreated
BillingCompleted
DispatchDelivered
NotificationDelivered
```

---

# 5. Identity Domain Events

## Publisher

iam-service

---

## UserCreated

### Purpose

Published when a new user is created.

### Consumers

* notification-service
* audit-service

### Payload

```json
{
  "userId": "uuid",
  "username": "string",
  "email": "string",
  "status": "ACTIVE"
}
```

---

## UserUpdated

### Consumers

* audit-service

---

## UserActivated

### Consumers

* branch-service
* audit-service

---

## UserDeactivated

### Consumers

* branch-service
* audit-service

---

## UserLoggedIn

### Consumers

* audit-service

---

## UserLoggedOut

### Consumers

* audit-service

---

## RoleAssigned

### Consumers

* audit-service

---

# 6. Branch Domain Events

## Publisher

branch-service

---

## BranchCreated

### Consumers

* customer-service
* reporting-service
* audit-service

### Payload

```json
{
  "branchId": "uuid",
  "branchCode": "string",
  "branchName": "string",
  "status": "ACTIVE"
}
```

---

## BranchUpdated

### Consumers

* reporting-service
* audit-service

---

## BranchActivated

### Consumers

* product-service
* reporting-service
* audit-service

---

## BranchDeactivated

### Consumers

* customer-service
* reporting-service
* audit-service

---

## TerritoryAssigned

### Consumers

* reporting-service
* audit-service

---

# 7. Customer Domain Events

## Publisher

customer-service

---

## CustomerCreated

### Consumers

* order-service
* reporting-service
* audit-service

---

## CustomerUpdated

### Consumers

* order-service
* reporting-service
* audit-service

---

## CustomerActivated

### Consumers

* reporting-service
* audit-service

---

## CustomerDeactivated

### Consumers

* reporting-service
* audit-service

---

## CustomerCreditUpdated

### Consumers

* billing-service
* reporting-service
* audit-service

---

# 8. Product Domain Events

## Publisher

product-service

---

## ProductCreated

### Consumers

* inventory-service
* reporting-service
* audit-service

---

## ProductUpdated

### Consumers

* reporting-service
* audit-service

---

## ProductActivated

### Consumers

* inventory-service
* order-service
* reporting-service
* audit-service

---

## ProductDeactivated

### Consumers

* inventory-service
* reporting-service
* audit-service

---

## ProductPriceUpdated

### Consumers

* billing-service
* reporting-service
* audit-service

---

# 9. Inventory Domain Events

## Publisher

inventory-service

---

## InventoryCreated

### Consumers

* reporting-service
* audit-service

---

## InventoryReserved

### Consumers

* order-service
* reporting-service
* audit-service

---

## InventoryReleased

### Consumers

* order-service
* reporting-service
* audit-service

---

## InventoryAllocated

### Consumers

* order-service
* billing-service
* reporting-service
* audit-service

---

## InventoryAdjusted

### Consumers

* reporting-service
* audit-service

---

## InventoryAvailabilityChanged

### Consumers

* billing-service
* reporting-service
* audit-service

---

# 10. Order Domain Events

## Publisher

order-service

---

## OrderCreated

### Consumers

* inventory-service
* billing-service
* notification-service
* reporting-service
* audit-service

---

## OrderValidated

### Consumers

* reporting-service
* audit-service

---

## OrderConfirmed

### Consumers

* billing-service
* dispatch-service
* reporting-service
* audit-service

---

## OrderCancelled

### Consumers

* inventory-service
* dispatch-service
* reporting-service
* audit-service

---

## OrderFailed

### Consumers

* reporting-service
* audit-service

---

## OrderCompleted

### Consumers

* reporting-service
* audit-service

---

# 11. Billing Domain Events

## Publisher

billing-service

---

## BillingCreated

### Consumers

* reporting-service
* audit-service

---

## BillingPartiallyCompleted

### Consumers

* dispatch-service
* notification-service
* reporting-service
* audit-service

---

## BillingCompleted

### Consumers

* inventory-service
* dispatch-service
* notification-service
* reporting-service
* audit-service

---

## BillingCancelled

### Consumers

* reporting-service
* audit-service

---

## BillingFailed

### Consumers

* order-service
* reporting-service
* audit-service

---

## BackorderCreated

### Consumers

* notification-service
* reporting-service
* audit-service

---

# 12. Dispatch Domain Events

## Publisher

dispatch-service

---

## DispatchCreated

### Consumers

* reporting-service
* audit-service

---

## DispatchScheduled

### Consumers

* notification-service
* reporting-service
* audit-service

---

## DispatchStarted

### Consumers

* reporting-service
* audit-service

---

## DispatchDelivered

### Consumers

* notification-service
* reporting-service
* audit-service

---

## DispatchCancelled

### Consumers

* reporting-service
* audit-service

---

## DispatchFailed

### Consumers

* reporting-service
* audit-service

---

## DeliveryConfirmed

### Consumers

* reporting-service
* audit-service

---

# 13. Notification Domain Events

## Publisher

notification-service

---

## NotificationCreated

### Consumers

* audit-service

---

## NotificationDelivered

### Consumers

* iam-service
* audit-service

---

## NotificationFailed

### Consumers

* audit-service

---

## NotificationRetried

### Consumers

* audit-service

---

# 14. Reporting Domain Events

## Publisher

reporting-service

---

## ReportGenerated

### Consumers

* audit-service

---

## DashboardGenerated

### Consumers

* audit-service

---

## ReportExported

### Consumers

* audit-service

---

# 15. Audit Domain Events

## Publisher

audit-service

---

## AuditEventPersisted

### Consumers

None

---

## ComplianceReportGenerated

### Consumers

None

---

## AuditExportGenerated

### Consumers

None

---

# 16. Saga Event Flows

## Order Fulfillment Saga

```text
OrderCreated
        ↓
InventoryReserved
        ↓
BillingCompleted
        ↓
DispatchScheduled
        ↓
DispatchDelivered
        ↓
OrderCompleted
```

---

## Compensation Flow

```text
OrderCreated
        ↓
InventoryReserved
        ↓
BillingFailed
        ↓
InventoryReleased
        ↓
OrderFailed
```

---

# 17. Kafka Topic Naming Convention

```text
dhs.<domain>.<event>

Examples:

dhs.iam.user-created
dhs.branch.branch-created
dhs.customer.customer-created
dhs.product.product-created
dhs.inventory.inventory-reserved
dhs.order.order-created
dhs.billing.billing-completed
dhs.dispatch.dispatch-delivered
dhs.notification.notification-delivered
dhs.reporting.report-generated
dhs.audit.audit-event-persisted
```

---

# 18. Event Versioning Strategy

```text
v1
 └── Initial Contract

v2
 └── Additive Changes Only

Breaking Changes
 └── New Event Version
```

---

# 19. Event Governance Rules

1. Events are immutable.
2. Events must contain correlation identifiers.
3. Events must be idempotent.
4. Consumers must tolerate duplicate delivery.
5. Services never depend on consumer acknowledgements.
6. Events may evolve only through versioning.
7. Events never expose internal database schemas.
8. All business workflows use asynchronous events for eventual consistency.
