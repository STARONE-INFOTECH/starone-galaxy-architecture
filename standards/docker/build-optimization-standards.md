# Build Optimization Standards

## Build Practices

- Use multi-stage builds.
- Cache dependency downloads where possible.
- Minimize image layers.
- Exclude unnecessary files using `.dockerignore`.
- Produce reproducible builds.

## Runtime Images

- Contain only the application runtime.
- Exclude source code.
- Exclude build tools.
- Exclude package managers where possible.

## Goal

Produce secure, lightweight, and reproducible container images suitable for enterprise deployment.