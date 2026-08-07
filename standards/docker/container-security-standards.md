# Container Security Standards

## Security Principles

- Run containers as non-root users.
- Do not store secrets in images.
- Use trusted base images.
- Keep runtime images minimal.
- Remove build-time dependencies from runtime images.
- Apply the principle of least privilege.
- Scan images for known vulnerabilities before release.

## Secrets

Secrets shall be provided through:

- Environment variables
- Kubernetes Secrets
- External secret management solutions
