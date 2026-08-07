# Dockerfile Conventions

## General Rules

- Use multi-stage builds.
- Keep Dockerfiles deterministic.
- One responsibility per image.
- Use official base images where possible.
- Expose only required ports.
- Use ENTRYPOINT for application startup.
- Avoid installing unnecessary packages.

## Runtime Requirements

- Java 21 runtime.
- Non-root execution.
- Read-only filesystem where applicable.
- Health checks should be supported by the application.

## Configuration

Application configuration shall be supplied using environment variables or Spring Cloud Config.
