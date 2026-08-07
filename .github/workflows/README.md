# GitHub Workflow Governance

This directory contains GitHub Actions workflows that implement Governance-as-Code for the StarOne Galaxy ecosystem. The workflows are designed for both self-consumption within this repository and reusable consumption by other StarOne Galaxy repositories.

## Workflow Baseline

| Workflow           | Purpose                                    |
| ------------------ | ------------------------------------------ |
| validation.yml     | Central validation orchestration workflow  |
| architecture.yml   | Architecture governance validation         |
| documentation.yml  | Documentation governance validation        |
| governance.yml     | Governance structure and policy validation |
| security.yml       | Security validation and compliance checks  |
| pr-validation.yml  | Pull request governance enforcement        |
| lint-standards.yml | Repository standards linting               |
| maven-build.yml    | Reusable Java 21 Maven build verification  |

## Validation Composition

### validation.yml

The validation workflow orchestrates the following reusable workflows:

- Architecture Review
- Documentation Validation
- Governance Validation
- Security Validation

### Documentation Validation

Documentation validation includes:

- Markdown Validation
- Mermaid Diagram Validation

### Governance Validation

Governance validation includes:

- Governance Artifact Validation
- PR Template Validation
- Commit Validation
- Issue Template Validation

### Security Validation

Security validation includes:

- Dependency Security
- Secret Scan
- Workflow Security
- Security Reporting

---

## Engineering Build Capabilities

### Maven Build

The `maven-build.yml` workflow provides the `ENG-BUILD-MAVEN` reusable
engineering capability for Java 21 Maven repositories.

The workflow:

- provisions Java 21 using the Temurin distribution;
- enables Maven dependency caching;
- reports the Maven Wrapper runtime;
- executes `./mvnw --batch-mode --no-transfer-progress clean verify`.

Consumer repositories retain ownership of dependency versions, Maven plugins,
module structure, and project-specific build configuration.

### Maven Consumer Prerequisites

Consumer repositories must:

- include the Maven Wrapper (`mvnw`, `mvnw.cmd`, and `.mvn/wrapper/`);
- use Maven 3.9 or later;
- support Java 21;
- provide a valid Maven project;
- ensure `./mvnw clean verify` succeeds from the repository root.

---

## Reusable Workflow Consumption

Consumer repositories can use the centralized validation workflow:

```yaml
jobs:
  validation:
    uses: STARONE-INFOTECH/starone-galaxy-architecture/.github/workflows/validation.yml@v1
```
---

Java 21 Maven repositories can consume the reusable Maven build capability:

```yaml
jobs:
  maven-build:
```
```markdown
    uses: STARONE-INFOTECH/starone-galaxy-architecture/.github/workflows/maven-build.yml@v1
```

---

## Future Expansion

Planned enhancements include:

- Dependency governance enhancements
- SBOM generation and validation
- Container image scanning
- Kubernetes manifest validation
- OpenAPI governance validation
- Organization-wide reusable workflow adoption

---

Governance Automation Baseline — Enabling CI/CD Governance-as-Code across the StarOne Galaxy ecosystem.
