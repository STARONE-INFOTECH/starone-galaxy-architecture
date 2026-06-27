# DOMAIN-001: DHS Domain Model

## Document Header

| Attribute          | Value                                                 |
| ------------------ | ----------------------------------------------------- |
| Document ID        | DHS-DOMAIN-001                                        |
| Project            | Distributed Hub and Sales (DHS) Platform              |
| Repository         | starone-dhs-system                                    |
| Version            | v1.0                                                  |
| Status             | Draft                                                 |
| Owner              | Solution Architecture Team                            |
| Architecture Style | Cloud-Native, Multi-Module Microservices Architecture |
| Pattern            | Domain-Driven Design (DDD)                            |
| Date               | 2026-06-20                                            |

---

# 1. Purpose

This document defines the bounded contexts, domain ownership, aggregate boundaries, domain entities, value objects, and domain relationships of the DHS Platform.

The objective of this document is to establish a clear business domain model that supports:

- Service autonomy
- Database per Service
- Independent deployment
- Event-driven integration
- Saga-based distributed transactions
- Future scalability and independent evolution

---

# 2. Domain Principles

## Domain Ownership

Each business capability owns:

- Domain Model
- Database
- APIs
- Domain Events
- Business Rules
- Data Lifecycle

No service may:

- Access another service database
- Share tables
- Share repositories
- Perform cross-service SQL queries

Interactions occur only through:

- REST APIs
- OpenFeign Clients
- Kafka Domain Events

---

# 3. Bounded Context Map

```text
Platform Context
├── Gateway Context
└── Discovery Context

Core Business Contexts
├── Identity Context
├── Branch Context
├── Customer Context
├── Product Context
├── Inventory Context
├── Order Context
├── Billing Context
├── Dispatch Context
├── Notification Context
├── Audit Context
├── Reporting Context
├── Supplier Context
├── Procurement Context
└── Return Context
```

---

# 4. Context Relationships

```text
IAM
 ├── Branch
 ├── Customer
 ├── Product
 ├── Inventory
 ├── Order
 ├── Billing
 ├── Dispatch
 ├── Notification
 ├── Audit
 ├── Reporting
 ├── Supplier
 ├── Procurement
 └── Return

Branch
 └── Customer

Product
 └── Inventory

Customer
 └── Order

Inventory
 └── Order

Order
 ├── Billing
 ├── Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Billing
 ├── Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Notification
 └── Audit

Reporting
 └── Audit
```

---

# 5. Platform Domain

## Bounded Context

Platform

## Services

- gateway-service
- discovery-service

## Responsibilities

- API Routing
- Authentication Enforcement
- Authorization Enforcement
- Service Registration
- Service Discovery
- Cross-Cutting Concerns

## Aggregate Roots

None

## Domain Type

Supporting Subdomain

---

# 6. Identity Domain

## Bounded Context

Identity Management

## Service

iam-service

## Aggregate Root

### User

Represents a platform user identity.

### Role

Represents authorization grouping.

### Permission

Represents executable privileges.

### Session

Represents authenticated sessions.

---

## Entities

### User

- userId
- username
- email
- password
- status
- createdAt

### Role

- roleId
- roleCode
- roleName

### Permission

- permissionId
- permissionCode
- permissionName

### Session

- sessionId
- token
- expiry

---

## Value Objects

### UserProfile

- firstName
- lastName
- phoneNumber

### Credential

- passwordHash
- passwordExpiry

---

## Domain Events

- UserCreated
- UserUpdated
- UserActivated
- UserDeactivated
- UserLoggedIn
- UserLoggedOut
- RoleAssigned

---

# 7. Branch Domain

## Bounded Context

Branch Management

## Service

branch-service

## Aggregate Root

### Branch

Represents a business branch.

---

## Entities

### Branch

- branchId
- branchCode
- branchName
- branchType
- status

### Region

- regionId
- regionCode
- regionName

### Territory

- territoryId
- territoryCode
- territoryName

---

## Value Objects

### Address

- addressLine1
- city
- state
- country
- postalCode

### ContactInformation

- email
- phoneNumber

---

## Domain Events

- BranchCreated
- BranchUpdated
- BranchActivated
- BranchDeactivated
- TerritoryAssigned

---

# 8. Customer Domain

## Bounded Context

Customer Management

## Service

customer-service

## Aggregate Root

### Customer

Represents a customer identity.

---

## Entities

### Customer

- customerId
- customerCode
- customerName
- customerType
- status

### CustomerCreditProfile

- creditLimit
- creditStatus

### CustomerCategory

- categoryCode
- categoryName

---

## Value Objects

### CustomerAddress

- addressLine1
- city
- state
- postalCode

### ContactInformation

- email
- phoneNumber

---

## Domain Events

- CustomerCreated
- CustomerUpdated
- CustomerActivated
- CustomerDeactivated
- CustomerCreditUpdated

---

# 9. Product Domain

## Bounded Context

Product Catalog Management

## Service

product-service

## Aggregate Root

### Product

Represents a sellable business product.

---

## Entities

### Product

- productId
- sku
- productName
- productType
- status

### ProductCategory

- categoryCode
- categoryName

### ProductBrand

- brandCode
- brandName

### ProductPrice

- amount
- currency

---

## Value Objects

### ProductSpecification

- model
- description
- attributes

---

## Domain Events

- ProductCreated
- ProductUpdated
- ProductActivated
- ProductDeactivated
- ProductPriceUpdated

---

# 10. Inventory Domain

## Bounded Context

Inventory Management

## Service

inventory-service

## Aggregate Root

### Inventory

Represents stock ownership and availability.

---

## Entities

### Inventory

- inventoryId
- productId
- availableQuantity
- reservedQuantity
- allocatedQuantity

### Reservation

- reservationId
- orderId
- quantity

### Allocation

- allocationId
- billingId
- quantity

### InventoryMovement

- movementId
- movementType
- quantity

---

## Value Objects

### StockQuantity

- available
- reserved
- allocated

---

## Domain Events

- InventoryCreated
- InventoryReserved
- InventoryReleased
- InventoryAllocated
- InventoryAdjusted
- InventoryAvailabilityChanged

---

# 11. Order Domain

## Bounded Context

Order Management

## Service

order-service

## Aggregate Root

### Order

Represents a customer purchase transaction.

---

## Entities

### Order

- orderId
- orderNumber
- customerId
- branchId
- status

### OrderItem

- orderItemId
- productId
- quantity
- unitPrice

### OrderSaga

- sagaId
- status

---

## Value Objects

### OrderAmount

- subtotal
- tax
- total

---

## Domain Events

- OrderCreated
- OrderValidated
- OrderConfirmed
- OrderCancelled
- OrderFailed
- OrderCompleted

---

# 12. Billing Domain

## Bounded Context

Billing Management

## Service

billing-service

## Aggregate Root

### Billing

Represents invoice generation and financial calculations.

---

## Entities

### Billing

- billingId
- invoiceNumber
- orderId
- billingStatus

### BillingItem

- billingItemId
- productId
- quantity
- amount

### Backorder

- backorderId
- pendingQuantity

---

## Value Objects

### TaxAmount

- taxType
- taxAmount

### MonetaryAmount

- subtotal
- discount
- total

---

## Domain Events

- BillingCreated
- BillingCompleted
- BillingPartiallyCompleted
- BillingCancelled
- BillingFailed
- BackorderCreated

---

# 13. Dispatch Domain

## Bounded Context

Dispatch Management

## Service

dispatch-service

## Aggregate Root

### Dispatch

Represents shipment execution.

---

## Entities

### Dispatch

- dispatchId
- orderId
- dispatchStatus

### Shipment

- shipmentId
- scheduleDate
- deliveryDate

### DeliveryConfirmation

- confirmationId
- confirmationDate

---

## Value Objects

### DeliveryAddress

- addressLine1
- city
- state
- postalCode

---

## Domain Events

- DispatchCreated
- DispatchScheduled
- DispatchStarted
- DispatchDelivered
- DispatchCancelled
- DispatchFailed

---

# 14. Notification Domain

## Bounded Context

Notification Management

## Service

notification-service

## Aggregate Root

### Notification

Represents business communication delivery.

---

## Entities

### Notification

- notificationId
- channel
- message
- status

### NotificationTemplate

- templateId
- templateCode
- templateName

### NotificationPreference

- preferenceId
- channel
- enabled

---

## Value Objects

### DeliveryInformation

- recipient
- subject
- payload

---

## Domain Events

- NotificationCreated
- NotificationDelivered
- NotificationFailed
- NotificationRetried

---

# 15. Reporting Domain

## Bounded Context

Reporting & Analytics

## Service

reporting-service

## Aggregate Root

### Report

Represents analytical information.

---

## Entities

### Report

- reportId
- reportType
- status

### Dashboard

- dashboardId
- dashboardName

### Projection

- projectionId
- projectionType

---

## Value Objects

### KPI

- name
- value
- timestamp

---

## Domain Events

- ReportGenerated
- DashboardGenerated
- ReportExported

---

# 16. Audit Domain

## Bounded Context

Audit & Compliance

## Service

audit-service

## Aggregate Root

### AuditEvent

Represents immutable business and security events.

---

## Entities

### AuditEvent

- auditId
- eventType
- entityType
- entityId
- timestamp

### Correlation

- correlationId
- traceId

### Timeline

- timelineId
- entityId
- events

---

## Value Objects

### AuditMetadata

- sourceService
- eventName
- actor
- ipAddress

---

## Domain Events

- AuditEventPersisted
- ComplianceReportGenerated
- AuditExportGenerated

---

# 17. Domain Dependency Matrix

```text
IAM
 ├── Branch
 ├── Customer
 ├── Product
 ├── Inventory
 ├── Order
 ├── Billing
 ├── Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Branch
 └── Customer

Product
 └── Inventory

Customer
 └── Order

Inventory
 └── Order

Order
 ├── Billing
 ├── Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Billing
 ├── Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Dispatch
 ├── Notification
 ├── Reporting
 └── Audit

Notification
 └── Audit

Reporting
 └── Audit
```

---

# 18. Domain Model Principles

1. One Bounded Context per Microservice
2. One Database per Service
3. Aggregate Boundaries are Service Boundaries
4. Cross-Service Communication via APIs and Events Only
5. Domain Events are Immutable
6. Services are Independently Deployable
7. Business Data Ownership Never Crosses Service Boundaries
8. Saga Pattern Coordinates Distributed Transactions
9. Reporting Uses Event-Driven Projections
10. Audit Uses Immutable Event Storage
