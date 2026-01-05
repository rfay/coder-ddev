## 1. Deployment phase
- [x] 1.1 Publish template to Coder <!-- id: 1.1 -->
  - Command: `coder templates push --directory . --name coder-ddev-base --yes`
- [x] 1.2 Create a Workspace <!-- id: 1.2 -->
  - Command: `coder create --template coder-ddev-base test-ddev-1`

## 2. Verification Phase
- [x] 1.3 Update template display name to "Coder DDEV Base" <!-- id: 1.3 -->
- [x] 2.0 Fix startup script permission error <!-- id: 2.0 -->
- [x] 2.1 SSH into Workspace and Verify DDEV <!-- id: 2.1 -->
  - Command: `coder ssh test-ddev-1`
  - Inside: `cd ~/projects/d11simple && ddev start`
  - Inside: `docker ps`
