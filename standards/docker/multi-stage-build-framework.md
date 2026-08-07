# Multi-Stage Docker Build Framework

## 1. Purpose

This document defines the enterprise multi-stage Docker build framework for all StarOne Galaxy platform and application repositories.

The objective is to standardize container builds that are secure, reproducible, lightweight, and maintainable.

---

## 2. Build Architecture

Every Docker image shall use a minimum of two stages:

1. Builder Stage
2. Runtime Stage

Additional stages (test, scan, publish) may be introduced when required.

---

## 3. Builder Stage Standard

Purpose

- Resolve dependencies
- Compile source code
- Execute tests
- Package application artifacts

Standard Builder Image

```text
starone/java21-builder:1.0.0
```

Builder images shall never be deployed to runtime environments.

---

## 4. Runtime Stage Standard

Purpose

Run packaged applications with the minimum required runtime dependencies.

Standard Runtime Image

```text
starone/java21-runtime:1.0.0
```

Runtime images shall not contain:

- Maven
- Gradle
- Source code
- Build cache
- Package managers

---

## 5. Artifact Packaging

Only deployable artifacts shall be copied from the builder stage.

Example

```text
target/*.jar
```

No source code or temporary build files shall exist in runtime images.

---

## 6. Build Optimization

The framework shall:

- Cache dependency downloads
- Minimize Docker layers
- Reduce image size
- Produce deterministic builds
- Support reproducible artifacts

---

## 7. Security

- Non-root execution
- Immutable runtime images
- Trusted base images only
- Secrets externalized
- Runtime image minimized

---

## 8. Governance

The Architecture Repository owns the multi-stage build standard.

Infrastructure repositories implement reusable templates based on this framework.

## 9. Artifact Packaging Standards

Only production-ready artifacts shall be copied into the runtime image.

### Packaging Rules

- Copy only executable JAR files.
- Exclude source code.
- Exclude Maven repository.
- Exclude test classes.
- Exclude build cache.
- Exclude temporary files.

Example

```text
COPY --from=builder /workspace/target/*.jar app.jar
```

## 10. Documentation Standards

Every reusable Docker template shall include:

- Purpose
- Supported application type
- Required base images
- Build instructions
- Runtime requirements
- Exposed ports
- Version compatibility
- Maintainer
