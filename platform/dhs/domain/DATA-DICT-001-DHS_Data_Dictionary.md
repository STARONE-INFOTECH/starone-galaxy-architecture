# DATA-DICTIONARY-001: DHS Data Dictionary

## Document Header

| Attribute | Value |
|-----------|--------|
| Document ID | DHS-DATA-DICTIONARY-001 |
| Project | Distributed Hub and Sales (DHS) Platform |
| Repository | starone-dhs-system |
| Version | v1.0 |
| Status | Draft |
| Owner | Solution Architecture Team |
| Architecture Style | Database per Service |
| Date | 2026-06-20 |

---

# 1. Purpose

This document defines the logical data dictionary for all DHS microservices.

Objectives:

- Establish canonical data definitions
- Define service-owned data boundaries
- Standardize naming conventions
- Support API contracts
- Support ERD generation
- Support OpenAPI generation
- Support database design activities

---

# 2. Data Ownership Principles

## Service Ownership

Every microservice exclusively owns:

- Database
- Tables
- Constraints
- Indexes
- Data lifecycle
- Data access policies

---

## Database Rules

- No shared databases
- No shared tables
- No cross-service SQL queries
- No cross-service foreign keys
- Data sharing only through APIs and Events

---

# 3. Common Metadata Fields

All aggregate tables should contain the following metadata fields.

| Field | Type | Nullable | Description |
|-------|------|-----------|-------------|
| id | UUID | No | Primary identifier |
| created_at | TIMESTAMP | No | Creation timestamp |
| created_by | VARCHAR(100) | No | Creator identifier |
| updated_at | TIMESTAMP | Yes | Last update timestamp |
| updated_by | VARCHAR(100) | Yes | Last updater identifier |
| version | BIGINT | No | Optimistic locking version |
| correlation_id | UUID | Yes | Request correlation identifier |

---

# 4. IAM Data Dictionary

## Database
iam-db

---

## users

| Column | Type | Nullable | Description |
|--------|------|-----------|-------------|
| user_id | UUID | No | User identifier |
| username | VARCHAR(100) | No | Login username |
| email | VARCHAR(255) | No | User email |
| password_hash | VARCHAR(500) | No | Encrypted password |
| first_name | VARCHAR(100) | No | First name |
| last_name | VARCHAR(100) | No | Last name |
| phone_number | VARCHAR(30) | Yes | Contact number |
| status | VARCHAR(30) | No | User status |

---

## roles

| Column | Type |
|--------|------|
| role_id | UUID |
| role_code | VARCHAR(100) |
| role_name | VARCHAR(255) |
| status | VARCHAR(30) |

---

## permissions

| Column | Type |
|--------|------|
| permission_id | UUID |
| permission_code | VARCHAR(100) |
| permission_name | VARCHAR(255) |
| description | TEXT |

---

## user_roles

| Column | Type |
|--------|------|
| user_role_id | UUID |
| user_id | UUID |
| role_id | UUID |

---

## role_permissions

| Column | Type |
|--------|------|
| role_permission_id | UUID |
| role_id | UUID |
| permission_id | UUID |

---

## user_sessions

| Column | Type |
|--------|------|
| session_id | UUID |
| user_id | UUID |
| access_token | TEXT |
| refresh_token | TEXT |
| expires_at | TIMESTAMP |

---

# 5. Branch Data Dictionary

## Database
branch-db

---

## branches

| Column | Type |
|--------|------|
| branch_id | UUID |
| branch_code | VARCHAR(50) |
| branch_name | VARCHAR(255) |
| branch_type | VARCHAR(50) |
| region_code | VARCHAR(50) |
| territory_code | VARCHAR(50) |
| status | VARCHAR(30) |

---

## branch_addresses

| Column | Type |
|--------|------|
| address_id | UUID |
| branch_id | UUID |
| address_line1 | VARCHAR(255) |
| city | VARCHAR(100) |
| state | VARCHAR(100) |
| country | VARCHAR(100) |
| postal_code | VARCHAR(20) |

---

## branch_contacts

| Column | Type |
|--------|------|
| contact_id | UUID |
| branch_id | UUID |
| email | VARCHAR(255) |
| phone_number | VARCHAR(30) |

---

# 6. Customer Data Dictionary

## Database
customer-db

---

## customers

| Column | Type |
|--------|------|
| customer_id | UUID |
| customer_code | VARCHAR(50) |
| customer_name | VARCHAR(255) |
| customer_type | VARCHAR(50) |
| branch_id | UUID |
| status | VARCHAR(30) |

---

## customer_addresses

| Column | Type |
|--------|------|
| address_id | UUID |
| customer_id | UUID |
| address_line1 | VARCHAR(255) |
| city | VARCHAR(100) |
| state | VARCHAR(100) |
| country | VARCHAR(100) |
| postal_code | VARCHAR(20) |

---

## customer_contacts

| Column | Type |
|--------|------|
| contact_id | UUID |
| customer_id | UUID |
| email | VARCHAR(255) |
| phone_number | VARCHAR(30) |

---

## customer_credit_profiles

| Column | Type |
|--------|------|
| profile_id | UUID |
| customer_id | UUID |
| credit_limit | DECIMAL(19,2) |
| available_credit | DECIMAL(19,2) |
| credit_status | VARCHAR(50) |

---

# 7. Product Data Dictionary

## Database
product-db

---

## products

| Column | Type |
|--------|------|
| product_id | UUID |
| sku | VARCHAR(100) |
| product_name | VARCHAR(255) |
| category_code | VARCHAR(50) |
| brand_code | VARCHAR(50) |
| product_type | VARCHAR(50) |
| status | VARCHAR(30) |

---

## product_prices

| Column | Type |
|--------|------|
| price_id | UUID |
| product_id | UUID |
| amount | DECIMAL(19,2) |
| currency | VARCHAR(10) |
| effective_from | TIMESTAMP |
| effective_to | TIMESTAMP |

---

## product_attributes

| Column | Type |
|--------|------|
| attribute_id | UUID |
| product_id | UUID |
| attribute_name | VARCHAR(255) |
| attribute_value | TEXT |

---

# 8. Inventory Data Dictionary

## Database
inventory-db

---

## inventories

| Column | Type |
|--------|------|
| inventory_id | UUID |
| product_id | UUID |
| available_quantity | INTEGER |
| reserved_quantity | INTEGER |
| allocated_quantity | INTEGER |
| status | VARCHAR(30) |

---

## inventory_reservations

| Column | Type |
|--------|------|
| reservation_id | UUID |
| order_id | UUID |
| product_id | UUID |
| reserved_quantity | INTEGER |
| reservation_status | VARCHAR(30) |

---

## inventory_allocations

| Column | Type |
|--------|------|
| allocation_id | UUID |
| billing_id | UUID |
| product_id | UUID |
| allocated_quantity | INTEGER |
| allocation_status | VARCHAR(30) |

---

## inventory_movements

| Column | Type |
|--------|------|
| movement_id | UUID |
| product_id | UUID |
| movement_type | VARCHAR(50) |
| quantity | INTEGER |
| remarks | VARCHAR(500) |

---

# 9. Order Data Dictionary

## Database
order-db

---

## orders

| Column | Type |
|--------|------|
| order_id | UUID |
| order_number | VARCHAR(100) |
| customer_id | UUID |
| branch_id | UUID |
| order_status | VARCHAR(30) |
| subtotal_amount | DECIMAL(19,2) |
| tax_amount | DECIMAL(19,2) |
| total_amount | DECIMAL(19,2) |

---

## order_items

| Column | Type |
|--------|------|
| order_item_id | UUID |
| order_id | UUID |
| product_id | UUID |
| quantity | INTEGER |
| unit_price | DECIMAL(19,2) |
| total_price | DECIMAL(19,2) |

---

## order_saga_instances

| Column | Type |
|--------|------|
| saga_id | UUID |
| order_id | UUID |
| saga_status | VARCHAR(50) |
| current_step | VARCHAR(100) |

---

# 10. Billing Data Dictionary

## Database
billing-db

---

## billings

| Column | Type |
|--------|------|
| billing_id | UUID |
| invoice_number | VARCHAR(100) |
| order_id | UUID |
| billing_status | VARCHAR(30) |
| subtotal_amount | DECIMAL(19,2) |
| tax_amount | DECIMAL(19,2) |
| total_amount | DECIMAL(19,2) |

---

## billing_items

| Column | Type |
|--------|------|
| billing_item_id | UUID |
| billing_id | UUID |
| product_id | UUID |
| quantity | INTEGER |
| amount | DECIMAL(19,2) |

---

## backorders

| Column | Type |
|--------|------|
| backorder_id | UUID |
| billing_id | UUID |
| product_id | UUID |
| pending_quantity | INTEGER |
| status | VARCHAR(30) |

---

# 11. Dispatch Data Dictionary

## Database
dispatch-db

---

## dispatches

| Column | Type |
|--------|------|
| dispatch_id | UUID |
| order_id | UUID |
| billing_id | UUID |
| dispatch_status | VARCHAR(30) |
| scheduled_date | TIMESTAMP |
| delivery_date | TIMESTAMP |

---

## dispatch_items

| Column | Type |
|--------|------|
| dispatch_item_id | UUID |
| dispatch_id | UUID |
| product_id | UUID |
| quantity | INTEGER |

---

## delivery_confirmations

| Column | Type |
|--------|------|
| confirmation_id | UUID |
| dispatch_id | UUID |
| confirmation_date | TIMESTAMP |
| confirmed_by | VARCHAR(100) |

---

# 12. Notification Data Dictionary

## Database
notification-db

---

## notifications

| Column | Type |
|--------|------|
| notification_id | UUID |
| channel | VARCHAR(50) |
| recipient | VARCHAR(255) |
| subject | VARCHAR(255) |
| payload | JSONB |
| status | VARCHAR(30) |

---

## notification_templates

| Column | Type |
|--------|------|
| template_id | UUID |
| template_code | VARCHAR(100) |
| template_name | VARCHAR(255) |
| template_body | TEXT |
| template_status | VARCHAR(30) |

---

## notification_preferences

| Column | Type |
|--------|------|
| preference_id | UUID |
| user_id | UUID |
| channel | VARCHAR(50) |
| enabled | BOOLEAN |

---

# 13. Reporting Data Dictionary

## Database
reporting-db

---

## report_definitions

| Column | Type |
|--------|------|
| report_id | UUID |
| report_name | VARCHAR(255) |
| report_type | VARCHAR(100) |
| report_status | VARCHAR(30) |

---

## dashboard_metrics

| Column | Type |
|--------|------|
| metric_id | UUID |
| dashboard_id | UUID |
| metric_name | VARCHAR(255) |
| metric_value | DECIMAL(19,2) |
| metric_timestamp | TIMESTAMP |

---

## reporting_projections

| Column | Type |
|--------|------|
| projection_id | UUID |
| projection_type | VARCHAR(100) |
| projection_data | JSONB |
| projection_timestamp | TIMESTAMP |

---

# 14. Audit Data Dictionary

## Database
audit-db

---

## audit_events

| Column | Type |
|--------|------|
| audit_id | UUID |
| event_name | VARCHAR(255) |
| entity_type | VARCHAR(100) |
| entity_id | UUID |
| source_service | VARCHAR(100) |
| correlation_id | UUID |
| trace_id | UUID |
| event_timestamp | TIMESTAMP |

---

## audit_timelines

| Column | Type |
|--------|------|
| timeline_id | UUID |
| entity_type | VARCHAR(100) |
| entity_id | UUID |
| event_count | INTEGER |

---

## audit_exports

| Column | Type |
|--------|------|
| export_id | UUID |
| export_type | VARCHAR(50) |
| requested_by | VARCHAR(100) |
| generated_at | TIMESTAMP |

---

# 15. Naming Standards

## Table Naming
```text
snake_case
Plural table names

Examples:
users
orders
inventory_reservations
notification_templates
```

## Column Naming
```text
snake_case

Examples:
customer_id
order_status
available_quantity
created_at
```

## Primary Keys
```text
<entity>_id

Examples:
user_id
order_id
product_id
billing_id
```

## Status Fields
```text
<entity>_status

Examples:
order_status
billing_status
dispatch_status
```

---

# 16. Database Governance Rules

1. Every service owns its database exclusively.
2. No cross-service foreign keys are allowed.
3. UUIDs are the standard primary key strategy.
4. All timestamps use UTC.
5. Business tables include audit metadata fields.
6. Eventual consistency is achieved through APIs and Kafka events.
7. Cross-service joins are prohibited.
8. Reporting uses projections and event-driven materialized views.
9. Audit data is immutable.
10. Database schema evolution follows backward-compatible migrations.