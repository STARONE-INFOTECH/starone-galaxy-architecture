# Docker Base Image Strategy

## 1. Purpose

This document defines the enterprise Docker base image strategy for all StarOne Galaxy platform and application repositories.

The objective is to provide secure, lightweight, standardized, and maintainable runtime environments across all services.

---

## 2. Base Image Principles

- Java 21 is the enterprise runtime standard.
- Official Eclipse Temurin images shall be used.
- Images shall be minimal and immutable.
- Multi-stage Docker builds are mandatory.
- Runtime images shall not contain build tools.
- Containers shall execute as non-root users.

---

## 3. Standard Images

### Builder Image

Purpose:

- Compile applications
- Execute Maven builds
- Produce executable artifacts

Standard Image

```text
maven:3.9.11-eclipse-temurin-21
```

---

### Runtime Image

Purpose

Execute Spring Boot services.

Standard Image

```text
eclipse-temurin:21-jre
```

---

## 4. Image Selection Criteria

Selection shall consider:

- Vendor support
- Long Term Support (LTS)
- Security updates
- Image size
- Compatibility
- Community adoption

---

## 5. Versioning

Images shall follow Semantic Versioning.

Example

```text
starone/java21-builder:1.0.0
starone/java21-runtime:1.0.0
```

The `latest` tag shall not be used for production deployments.

---

## 6. Security

- Non-root execution
- Trusted base images only
- Minimal runtime footprint
- No embedded secrets
- Regular security updates

---

## 7. Governance

The Architecture Repository defines the base image strategy.

Infrastructure repositories implement this strategy.

## Linux Distribution Standard

The default runtime operating system shall be Eclipse Temurin's supported Linux runtime image.

Selection criteria:

- Official vendor support
- Long-Term Support (LTS)
- Security update cadence
- Small runtime footprint
- Compatibility with Java 21

Alternative runtime images require Architecture approval.

## Image Maintenance Procedure

Platform Engineering shall maintain all enterprise base images.

Maintenance activities include:

- Monthly security patch review
- Quarterly base image upgrades
- Java LTS update verification
- Vulnerability scanning
- Deprecation review

Applications consume platform images and shall not maintain independent base images.

## Image Governance

Ownership

- Architecture Repository
  - Standards
  - Versioning Policy
  - Security Policy
  - Runtime Selection

- Infrastructure Repository
  - Base Image Implementation
  - Dockerfiles
  - Runtime Templates
  - Builder Images

Any deviation requires an approved Architecture Decision Record (ADR).

## Documentation Standard

Each base image shall include:

- Purpose
- Base image reference
- Supported Java version
- Supported operating system
- Build instructions
- Maintenance owner
- Version history
