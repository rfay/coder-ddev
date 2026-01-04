# Project Context

## Purpose
This project provides a vendor-neutral, infrastructure-focused Coder template for seamless DDEV integration. It enables secure, high-performance nested Docker environments using Sysbox, allowing developers to run DDEV-based projects within Coder workspaces with full feature parity and minimal configuration.

## Tech Stack
- **Infrastructure as Code**: Terraform (HCL)
- **Container Runtime**: Docker (with Sysbox runtime for safe nesting)
- **Development Tool**: DDEV (Docker-based PHP/Node/Python development)
- **Platform**: Coder v2+
- **OS**: Linux (Debian/Ubuntu-based images)

## Project Conventions

### Code Style
- **Minimalist**: Avoid bundling non-essential tools (AI agents, custom shell prompts) in the base image.
- **Decoupled**: Strict separation of infrastructure (Terraform/Docker) from application content.
- **Manual-First**: The template does not automate git cloning or project bootstrapping; the user manages their content manually.
- **Standard Paths**: Always use `/home/coder` as the persistent home directory.

### Architecture Patterns
- **Sysbox Isolation**: Uses `sysbox-runc` to provide a "Docker-in-Docker" experience that feels native, without privileged mode security risks.
- **Inner-Docker Cache**: Persists `/var/lib/docker` in a dedicated volume to ensure fast container restarts.
- **Diagnostic Transparency**: All critical startup logs are directed to `/tmp/coder-script-*.log` for easy debugging.
- **SSH Neutrality**: Relies on standard SSH configurations, avoiding opinionated host key injection.

### Git Workflow
- **Monorepo / Infra-Repo**: This repository typically lives in an infrastructure collection.
- **Versioning**: Docker images and Terraform templates should be versioned in lockstep where possible.

## Domain Context
- **DDEV**: A CLI tool for launching local web development environments. It expects access to a Docker daemon.
- **Unified Routing**: Coder handles ingress; DDEV configured to use Coder's port forwarding.

## Important Constraints
- **Sysbox Requirement**: The host Coder node must have `sysbox-runc` installed and configured.
- **Privilege**: Workspaces run unprivileged but with the `sysbox-runc` runtime class.

## External Dependencies
- **Docker Hub**: For base images.
- **DDEV Release Config**: DDEV installs relate to upstream releases.
- **Coder Server**: Requires an active Coder deployment.
