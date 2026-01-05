## ADDED Requirements
### Requirement: Template Verification
The system SHALL provide a verified path for deploying and testing DDEV based projects.

#### Scenario: Deploy and Test
- **WHEN** the template is deployed to Coder as `coder-ddev-base`
- **AND** a workspace is created with a DDEV project
- **THEN** the template SHALL be available as `coder-ddev-base`
- **AND** the DDEV containers MUST start successfully

