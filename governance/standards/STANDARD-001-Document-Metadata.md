# Document Metadata Governance Standard

## Purpose

This standard defines the mandatory metadata model for all governed documentation artifacts within the StarOne Galaxy ecosystem.

The objective is to ensure consistent document identification, ownership, lifecycle visibility, traceability, and governance across all documentation assets.

---

# Scope

This standard applies to:

- ADR
- BRD
- PRD
- FRD
- HLD
- LLD
- SRS
- RTM
- EPIC
- ISSUE
- MILESTONE
- PR
- README_MS
- README_Global

---

# Mandatory Metadata Fields

All governed documents shall contain the following metadata fields.

| Field | Description |
|---------|---------|
| Document ID | Unique identifier for the document |
| Domain | Functional or platform domain |
| Document Type | Artifact classification |
| Version | Document version |
| Author | Document owner |
| Date | Creation or publication date |
| Status | Document lifecycle state |
| Linked Epic | Associated Epic |
| Linked Story | Associated Story |
| Approval Status | Governance approval state |

---

# Document ID Standard

Format:

```text
<DOCUMENT-TYPE>-<DOMAIN>-<SEQUENCE>
```

Examples:

```text
ADR-ARCH-001
HLD-DHS-001
SRS-BOOKSHOW-001
BRD-INFRA-001
```

---

# Domain Values

Approved domains:

```text
INFRA
DHS
BOOKSHOW
GALAXY
GOVERNANCE
```

---

# Document Type Values

Approved document types:

```text
ADR
BRD
PRD
FRD
HLD
LLD
SRS
RTM
EPIC
ISSUE
MILESTONE
PR
README_MS
README_GLOBAL
```

---

# Status Lifecycle

Approved status values:

| Status | Meaning |
|----------|----------|
| Draft | Under authoring |
| Review | Under review |
| Approved | Approved for use |
| Frozen | Baseline locked |
| Deprecated | No longer recommended |
| Archived | Historical reference only |

---

# Approval Status Lifecycle

Approved approval values:

| Approval Status | Meaning |
|-----------------|---------|
| Pending | Awaiting review |
| Approved | Approved by reviewers |
| Rejected | Rejected |
| Superseded | Replaced by newer artifact |

---

# Governance Rules

- Metadata shall appear near the beginning of every governed document.
- Metadata fields shall not be removed.
- Status values must follow the approved lifecycle.
- Document identifiers must remain unique.

---

# References

- EPIC-ARCH-001
- STORY-ARCH-003
- S3-I01
- S3-I02