# Change: Deploy and Verify DDEV-Coder Template

## Why
To ensure the `coder-ddev-base` image and template work correclty in a real environment, we need a defined deployment and verification process. This ensures that the DockerHub integration and the template configuration are functional.

## What Changes
- Defines the `Verification` capability.
- Establishes a manual verification scenario for deploying to Coder, creating a workspace, and running DDEV.

## Impact
- Affected specs: `verification`
- Affected code: None (Process-only change)
