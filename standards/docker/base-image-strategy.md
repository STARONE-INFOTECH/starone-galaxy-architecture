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
