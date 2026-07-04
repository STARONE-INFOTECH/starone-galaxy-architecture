# DOCUMENT TEMPLATE STANDARD

**Document ID:** STD-TPL-001

**Version:** v2.0.0

**Status:** Approved

**Owner:** Enterprise Architecture

---

# 1. Purpose

This standard defines the mandatory structure, formatting, metadata, and authoring conventions for all engineering document templates within the STARONE engineering ecosystem.

The objective is to ensure every template is:

- Consistent
- Maintainable
- Reusable
- Traceable
- Machine-readable
- Human-readable

This standard governs **template design only**.

Engineering governance, SDLC ownership, document boundaries, lifecycle, traceability, and repository governance are defined in the **Engineering Governance Handbook**.

---

# 2. Scope

This standard applies to all engineering document templates including:

- Business Need
- BRD
- PRD
- FRD
- SRS
- HLD
- LLD
- ADR
- RTM
- Epic
- Story
- Issue
- Milestone
- Pull Request
- README
- Future engineering document templates

---

# 3. Template Design Principles

Every engineering template shall comply with the following principles.

## TPL-001

Consistency over creativity.

---

## TPL-002

One document, one responsibility.

---

## TPL-003

Minimal duplication.

---

## TPL-004

Progressive elaboration.

---

## TPL-005

Clear ownership.

---

## TPL-006

Reusable structure.

---

## TPL-007

Git repository friendly.

---

## TPL-008

Human readable.

---

## TPL-009

AI processable.

---

# 4. Standard Document Skeleton

Unless explicitly approved otherwise, every engineering document template shall follow the structure below.

```text
Title

1. Title Page

2. Document Metadata

3. Revision History

4. References

5. Sign-Off

6. Scope / Purpose

7. Document-Specific Sections

8. Acceptance / Success Criteria

(Optional)

Glossary

Appendices
```

Individual document templates may extend the document-specific sections while preserving the common structure.

---

# 5. Metadata Standard

Every engineering template shall contain a metadata section.

Mandatory fields:

| Field         | Mandatory |
| ------------- | --------- |
| Document ID   | Yes       |
| Document Name | Yes       |
| Document Type | Yes       |
| Domain        | Yes       |
| Version       | Yes       |
| Status        | Yes       |
| Author        | Yes       |
| Date          | Yes       |

Optional fields:

- Project
- Module
- Repository
- Linked Epic
- Linked Story
- Classification

Templates shall not redefine mandatory metadata.

---

# 6. Heading Standard

Templates shall use GitHub Markdown heading hierarchy.

```text
#

Document Title

##

Major Section

###

Subsection

####

Optional Detail
```

Heading levels shall not be skipped.

Heading styles shall remain consistent throughout the document.

---

# 7. Section Design Rules

Each section shall own one responsibility.

Sections shall not mix unrelated concerns.

Example:

FRD

- Functional Requirements
- Business Rules
- Workflow
- Validation
- Acceptance

Not

- Functional Requirements
- API Design
- Database Design
- Infrastructure

Those belong to downstream artifacts.

---

# 8. Table Standards

Tables shall be used whenever information is structured.

Recommended for:

- Requirements
- Validation Rules
- Business Rules
- Reports
- Roles
- Screens
- Metadata
- Revision History

Narrative content should use paragraphs instead of tables.

---

# 9. List Standards

Bulleted lists shall be used for:

- Features
- Responsibilities
- Constraints
- Assumptions
- Capabilities

Numbered lists shall only be used where sequence is significant.

---

# 10. Requirement Identifier Standard

Requirement identifiers shall remain unique within the owning document.

Examples:

```text
BN-001

BR-001

PR-001

FR-IAM-001

SR-001

HLD-001

LLD-001

ADR-001
```

Identifiers shall never be reused.

---

# 11. Diagram Standards

Preferred notation:

- Mermaid

Recommended diagrams by document:

| Document      | Preferred Diagram |
| ------------- | ----------------- |
| Business Need | Flowchart         |
| BRD           | Business Process  |
| PRD           | User Journey      |
| FRD           | Workflow          |
| SRS           | Sequence          |
| HLD           | Architecture      |
| LLD           | Class Diagram     |
| LLD           | ER Diagram        |
| ADR           | Decision Diagram  |

Avoid embedded images whenever practical.

---

# 12. Markdown Standards

Engineering templates shall use GitHub Flavored Markdown.

Preferred elements:

- Tables
- Mermaid
- Fenced code blocks
- Ordered lists
- Bullet lists

Avoid:

- HTML
- Inline styling
- Images when Mermaid is sufficient

---

# 13. Writing Standards

Engineering documentation shall be:

- Clear
- Concise
- Objective
- Testable
- Consistent
- Unambiguous

Avoid:

- Marketing language
- Personal opinions
- Ambiguous wording
- Implementation assumptions
- Duplicate content

Normative language shall be used.

Preferred:

> The system shall...

Avoid:

> The system will...

> The system can...

unless optional.

---

# 14. Revision History Standard

Every template shall include a revision history section.

Minimum columns:

| Version | Date | Author | Description |

Revision history shall be preserved.

Historical entries shall never be removed.

---

# 15. References Section Standard

Every template shall include a References section.

The References section identifies the approved upstream artifacts required by the document.

References shall not duplicate upstream content.

Forward and backward traceability is maintained by the RTM.

---

# 16. Sign-Off Standard

Approval-based templates shall include a Sign-Off section.

Minimum fields:

| Role | Name | Status |

Projects may extend the approval matrix without modifying the template structure.

---

# 17. Template Inheritance

All engineering templates inherit the common structure.

```text
Title Page

↓

Metadata

↓

Revision History

↓

References

↓

Sign-Off

↓

Scope

↓

Document-Specific Sections

↓

Acceptance Criteria

↓

Glossary

↓

Appendices
```

Only the document-specific sections vary between templates.

---

# 18. Template Customization Rules

Projects may:

- Add document-specific sections.
- Add optional metadata.
- Extend approval roles.

Projects shall not:

- Remove mandatory sections.
- Reorder mandatory sections.
- Modify metadata definitions.
- Change heading hierarchy.
- Alter template ownership.

---

# 19. AI Template Generation Rules

AI-generated engineering templates shall:

- Follow this Document Template Standard.
- Follow the Engineering Governance Handbook.
- Preserve document boundaries.
- Preserve template structure.
- Preserve progressive elaboration.
- Avoid duplication.
- Maintain section ordering.
- Produce valid GitHub Markdown.

---

# 20. Template Validation Checklist

Before approving a template verify:

- Metadata
- Revision History
- References
- Sign-Off
- Heading Hierarchy
- Section Order
- Naming
- Markdown Compliance
- Diagram Standards
- Identifier Standards
- Ownership
- Template Consistency

---

# 21. Relationship to Engineering Governance Handbook

This standard defines **how engineering templates are structured**.

The **Engineering Governance Handbook** defines:

- Engineering Governance
- SDLC Lifecycle
- Repository Governance
- Document Ownership
- SDLC Traceability
- Review Process
- Compliance
- Engineering Responsibilities

Where conflicts exist, the Engineering Governance Handbook takes precedence.

---

# 22. Compliance

All engineering document templates shall comply with:

- Engineering Governance Handbook
- This Document Template Standard
- Approved Enterprise Standards
- Repository Standards
- Markdown Standards

This document is the single source of truth for engineering document template design across the STARONE engineering ecosystem.
