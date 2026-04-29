# 🤝 Contribution & Governance Guide
**Project:** StarOne Galaxy  
**Domain:** Cross-Domain Governance  
**Author:** Sachin Salunke  
**Status:** Approved (Baseline)

## 1. Overview
This guide defines the standards for contributing to the **StarOne Galaxy Architecture** repository. Following these rules ensures 100% traceability and ISO-compliant documentation across all five ecosystem repositories.

---

## 2. Branching Model (AC-06)
We follow a **Trunk-Based Development** model with short-lived feature branches to ensure the "Architectural Source of Truth" is always up to date.

| Branch Type | Naming Convention | Purpose |
| :--- | :--- | :--- |
| **Main** | `main` | Production-ready, approved architectural baseline. |
| **Feature** | `feat/STORY-ID-description` | New architectural artifacts (HLD, SRS, Epics). |
| **Fix** | `fix/STORY-ID-description` | Corrections to existing documentation. |
| **Hotfix** | `hotfix/issue-description` | Critical governance or security updates. |

### Workflow:
1. Create a branch from `main`.
2. Commit changes using **Semantic Commit Messages** (see Section 3).
3. Open a Pull Request (PR) and link the corresponding **GitHub Issue**.
4. Merge to `main` only after **Architecture Review Board (ARB)** sign-off.

---

## 3. Naming & Commit Standards (AC-05)

### File & Folder Naming
- **Format:** `kebab-case` (all lowercase, hyphens instead of spaces).
- **Versioning:** Use suffix `_v1.0` only for major baselines; otherwise, rely on Git history.
- **Example:** `docs/adr/adr-001-repository-strategy.md`

### Semantic Commit Messages
All commits must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:
- `feat:` (New architecture or documentation)
- `fix:` (Correction to existing docs)
- `docs:` (Documentation-only changes)
- `refactor:` (Restructuring folders/taxonomy)
- `chore:` (Updating GitHub Actions or internal tools)

**Example:** `feat: initialize repository scaffolding and taxonomy (ref SGA-ARCH#1)`

---

## 4. Documentation Standards (SDLC)
To maintain **ISO/IEC/IEEE 29148** compliance, every document must:
1. Use the approved **Master Template**.
2. Include a **Revision History** table.
3. Include **Mermaid.js** diagrams for any logic flow or structure.
4. Maintain **Traceability** back to the Product Vision.

---

## 5. Governance Ownership (AC-03)
As defined in `.github/CODEOWNERS`, all changes to the `governance/` and `architecture/` directories require approval from the **Platform Architect (Sachin Salunke)**.

---

## 6. Definition of Done (DoD)
A contribution is considered "Done" when:
- [ ] Markdown linter passes (CI/CD check).
- [ ] Mermaid diagrams render correctly.
- [ ] No broken internal links.
- [ ] Linked Issue is moved to "Done" on the Master Project Board.