# Coder DDEV Base Image

This Docker image is the base image for Coder Drupal DDEV workspaces. It contains:
- Ubuntu LTS
- Docker daemon (for Docker-in-Docker with Sysbox)
- DDEV (latest)
- Node.js LTS
- coder user (UID 1000) with passwordless sudo

## Building

Use the Makefile in the repository root to build this image:

```bash
# From the repository root
make build              # Build with cache
make build-no-cache     # Build without cache
make build-and-push     # Build and push to Docker Hub
```

See the root README.md for complete documentation on version management and deployment.
