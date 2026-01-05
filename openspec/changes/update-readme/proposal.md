# Change: Update README with Deployment Commands

## Why
The current `README.md` lacks specific instructions on how to deploy the `coder-ddev-base` template and create workspaces using the new naming convention.

## What Changes
- Updates `template/README.md` (or project root README) to include:
  - `coder templates push` command.
  - `coder create` command.
  - Prerequisite checks (Vault, DockerHub).

## Impact
- Affected specs: `documentation`
- Affected code: `template/README.md`
