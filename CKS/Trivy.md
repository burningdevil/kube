# Trivy

Trivy (pronunciation) is a comprehensive and versatile security scanner. Trivy has scanners that look for security issues, and targets where it can find those issues.

Targets (what Trivy can scan):

- Container Image
- Filesystem
- Git Repository (remote)
- Virtual Machine Image
- Kubernetes
- AWS

## General Usage

`trivy <target> [--scanners <scanner1,scanner2>] <subject>`

Examples:

`trivy image/fs/k8s python:3.4-alpine`
