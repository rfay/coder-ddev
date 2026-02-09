# DDEV Coder Template

Coder workspace template for DDEV-based development with Docker-in-Docker support, Node.js, and Git.

## Features

- **Custom Base Image**: Ubuntu 24.04 LTS with essential development tools
- **Docker-in-Docker**: Full Docker support for DDEV (using Sysbox runtime)
- **Node.js/npm**: LTS version (configurable)
- **DDEV v1.24.10**: Pre-installed and ready to use
- **VS Code for Web**: Browser-based IDE with full extension support
- **PHP/Python/Node Projects**: Support for 20+ project types via DDEV

## Configuration

**Container:**
- User: `coder` (UID 1000)
- Runtime: `sysbox-runc` (for secure Docker-in-Docker)
- Docker daemon: Runs inside the container

**Installed Tools:**
- Docker CLI and daemon (latest stable)
- ddev (latest)
- Node.js LTS (configurable via `node_version` variable)
- Git, vim, build tools

## Docker Image and Template Management

### Building and Deploying

The base Docker image is built from the `image/Dockerfile` and the Coder template is in `template/`. Use the provided Makefile to manage everything:

```bash
# Full deployment (build, push image, push template)
make deploy

# Full deployment without cache
make deploy-no-cache

# Image operations
make build              # Build the image with cache
make build-no-cache     # Build without cache (useful for clean builds)
make push               # Push to Docker Hub
make build-and-push     # Build and push in one command

# Template operations
make push-template      # Push template to Coder

# Utility commands
make test               # Test the built image
make info               # Show version and configuration
make help               # See all available commands
```

### Version Management

The Docker image and template versions are managed via two files:

1. **`VERSION` file** (root directory): Used by the Makefile when building/tagging Docker images
2. **`template/template.tf`**: The `image_version` variable default value

**To release a new version:**
1. Update the `VERSION` file (e.g., `v0.5`)
2. Update the `image_version` default in `template/template.tf` to match
3. Run `make deploy` to build image, push image, and push template

**Quick deployment:**
```bash
# After updating both VERSION and template.tf:
make deploy              # Build with cache and deploy
# or
make deploy-no-cache     # Clean build and deploy
```

**Note:** Keep the VERSION file and template.tf `image_version` in sync manually when releasing new versions.

## Supported Project Types

DDEV supports 20+ project types out of the box. All work identically in Coder workspaces.

**Static Sites:**
- HTML, Jekyll, Hugo, any static site generator

**Generic:**
- Custom PHP, Go, Rust, or any web application

See [DDEV Documentation](https://ddev.readthedocs.io/) for full list and configuration.

## Documentation

**New to Coder?**
- 📘 [Getting Started Guide](./docs/user/getting-started.md) - Create your first workspace
- 📗 [Using Workspaces](./docs/user/using-workspaces.md) - Daily workflows and tips

**Administrators:**
- 📕 [Operations Guide](./docs/admin/operations-guide.md) - Deploy and manage template
- 📙 [User Management](./docs/admin/user-management.md) - Users, roles, permissions
- 📔 [Troubleshooting](./docs/admin/troubleshooting.md) - Debug common issues

**DDEV Experts:**
- 🔍 [Comparison to Local DDEV](./docs/architecture/comparison-to-local.md) - Architecture, tradeoffs, migration

**Developers/Contributors:**
- 🤖 [CLAUDE.md](./CLAUDE.md) - AI-assisted development guide

📚 **[Full Documentation Index](./docs/README.md)**

## Template Structure

```
coder-ddev/
├── docs/                # Documentation
│   ├── admin/           # Administrator guides
│   ├── user/            # User guides
│   ├── architecture/    # Architecture and comparisons
│   └── README.md        # Documentation index
├── ddev-user/           # Coder template
│   ├── template.tf      # Terraform template definition
│   └── scripts/         # Startup and shutdown scripts
├── image/               # Docker image
│   ├── Dockerfile       # Image build instructions
│   └── scripts/         # Files copied to image
├── Makefile             # Build and deploy automation
├── VERSION              # Current image version
└── README.md            # This file
```

## Quick Start

### For Users (Developers using DDEV)

Create and use DDEV workspaces:

```bash
# Create workspace
coder create --template ddev-user my-workspace --yes

# SSH into workspace
coder ssh my-workspace

# Create DDEV project (examples - choose your project type)
mkdir ~/projects/my-site && cd ~/projects/my-site

# WordPress
ddev config --project-type=wordpress --docroot=web
ddev composer create drupal/recommended-project

# Laravel
ddev config --project-type=laravel --docroot=public
ddev composer create laravel/laravel

# Generic PHP
ddev config --project-type=php --docroot=web
mkdir web && echo "<?php phpinfo();" > web/index.php

# Start DDEV
ddev start
```

**Access your project:**
- Open Coder dashboard
- Find your workspace
- Click on port **80** or **443** under "Apps"

**📖 [Full Getting Started Guide](./docs/user/getting-started.md)**

### For Administrators

Deploy template and manage infrastructure:

```bash
# Build and push Docker image
cd image
docker build -t randyfay/coder-ddev:v0.1 .
docker push randyfay/coder-ddev:v0.1

# Deploy template to Coder
coder templates push --directory ddev-user ddev-user --yes

# Or use Makefile
make deploy  # Build + push image + push template
```

**📖 [Full Operations Guide](./docs/admin/operations-guide.md)**
