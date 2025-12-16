# Dev Workflow OS v1 - Implementation Guide

This document provides complete folder trees and file contents for the three-repository system.

## System Overview

The Dev Workflow OS v1 consists of three interconnected repositories:

1. **ORG/.github** - Organization defaults (PUBLIC)
2. **ORG/repo-template** - Repository template  
3. **ORG/dev-workflow-os** - Control plane / source of truth

## Repository 1: ORG/.github (Organization Defaults)

**Visibility**: MUST be PUBLIC for defaults to apply organization-wide

**Purpose**: Organization-wide default community health files and workflow templates

### Folder Tree

```
ORG/.github/
├── .github/
│   └── ISSUE_TEMPLATE/
│       ├── config.yml
│       ├── bug_report.yml
│       ├── feature_request.yml
│       ├── task.yml
│       ├── governance-change.yml
│       ├── new-repo-request.yml
│       ├── swarm-run.yml
│       └── incident.yml
├── workflow-templates/
│   ├── policy-check.yml
│   ├── policy-check.properties.json
│   ├── add-to-project.yml
│   └── add-to-project.properties.json
├── profile/
│   └── README.md (optional org profile)
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── GOVERNANCE.md
├── PULL_REQUEST_TEMPLATE.md
├── SECURITY.md
├── SUPPORT.md
└── LICENSE
```

### Key Files

All files are already created in the current repository structure. See the actual files for complete content.

**Community Health Files**:
- CODE_OF_CONDUCT.md - Behavioral standards
- CONTRIBUTING.md - Contribution guidelines
- GOVERNANCE.md - Decision-making process
- SECURITY.md - Vulnerability reporting
- SUPPORT.md - How to get help
- PULL_REQUEST_TEMPLATE.md - PR description template

**Issue Templates** (.github/ISSUE_TEMPLATE/):
- config.yml - Issue template configuration
- bug_report.yml - Bug reporting form
- feature_request.yml - Feature request form
- task.yml - Task tracking form
- governance-change.yml - Governance change proposal
- new-repo-request.yml - New repository request
- swarm-run.yml - Multi-agent swarm coordination
- incident.yml - Production incident reporting

**Workflow Templates** (workflow-templates/):
- policy-check.yml - Repository compliance validation
- policy-check.properties.json - Metadata
- add-to-project.yml - Auto-add issues/PRs to project
- add-to-project.properties.json - Metadata

## Repository 2: ORG/repo-template

**Purpose**: Template repository for creating new repos with complete structure

### Folder Tree

```
ORG/repo-template/
├── .github/
│   ├── agents/
│   │   ├── planner.agent.md
│   │   ├── governance.agent.md
│   │   ├── ci-automation.agent.md
│   │   └── docs-diagrams.agent.md
│   ├── instructions/
│   │   ├── governance.instructions.md
│   │   └── docs.instructions.md
│   ├── prompts/
│   │   ├── new-repo-bootstrap.prompt.md
│   │   ├── ruleset-update.prompt.md
│   │   ├── coverage-matrix-update.prompt.md
│   │   └── incident-triage.prompt.md
│   ├── workflows/
│   │   ├── policy-check.yml
│   │   ├── add-to-project.yml
│   │   ├── dependency-review.yml
│   │   └── ci.yml
│   └── copilot-instructions.md
├── .vscode/
│   ├── settings.json
│   ├── extensions.json
│   └── tasks.json
├── .devcontainer/
│   └── devcontainer.json (OPTIONAL_MODULE)
├── docs/
│   ├── architecture/
│   │   └── README.md
│   ├── governance/
│   │   └── README.md
│   └── runbooks/
│       └── README.md
├── README.md
├── LICENSE
├── .gitignore
└── CODEOWNERS
```

All template files are located in `/home/runner/work/.github/.github/templates/repo-template/`

### Key Components

**Custom Agents** (.github/agents/):
- planner.agent.md - Strategic planning and task breakdown
- governance.agent.md - Compliance and policy enforcement
- ci-automation.agent.md - Build, test, deployment automation
- docs-diagrams.agent.md - Documentation and architecture diagrams

**Instructions** (.github/instructions/):
- governance.instructions.md - Governance change guidance
- docs.instructions.md - Documentation standards

**Prompts** (.github/prompts/):
- new-repo-bootstrap.prompt.md - Repository initialization
- ruleset-update.prompt.md - Update repository rulesets
- coverage-matrix-update.prompt.md - Update coverage matrix
- incident-triage.prompt.md - Incident response procedures

**Workflows** (.github/workflows/):
- policy-check.yml - Validate repo compliance
- add-to-project.yml - Auto-add to project board
- dependency-review.yml - Security dependency scanning
- ci.yml - Continuous integration (customize per repo)

**Documentation** (docs/):
- architecture/README.md - Architecture overview
- governance/README.md - Repo governance docs
- runbooks/README.md - Operational procedures

## Repository 3: ORG/dev-workflow-os (Control Plane)

**Purpose**: Source of truth for governance, policies, templates, automation

### Folder Tree

```
ORG/dev-workflow-os/
├── docs/
│   ├── standards/
│   │   ├── custom-agents.md
│   │   ├── swarms.md
│   │   ├── workflows.md
│   │   └── codeowners.md
│   ├── governance/
│   │   ├── README.md
│   │   └── coverage-matrix.md
│   ├── diagrams/
│   │   ├── system-architecture.mmd
│   │   ├── repo-bootstrap-flow.mmd
│   │   ├── governance-stack.mmd
│   │   ├── defense-in-depth.mmd
│   │   ├── issue-lifecycle.mmd
│   │   ├── access-model.mmd
│   │   └── automation-map.mmd
│   ├── tables/
│   │   └── github-projects-fields.md
│   └── runbooks/
│       ├── README.md
│       ├── new-repo-setup.md
│       ├── ruleset-management.md
│       └── compliance-audit.md
├── policy/
│   ├── rulesets/
│   │   ├── ruleset-v1.md
│   │   ├── main-branch-protection.json
│   │   └── release-branch-protection.json
│   ├── labels/
│   │   ├── standard-labels.md
│   │   └── labels.json
│   └── required-files/
│       ├── README.md
│       └── checklist.md
├── templates/
│   ├── repo-template/
│   │   └── (copy of ORG/repo-template structure)
│   └── org-dotgithub/
│       └── (copy of ORG/.github structure)
├── scripts/
│   └── gh/
│       ├── create-repo.sh
│       ├── apply-rulesets.sh
│       ├── sync-labels.sh
│       ├── audit-compliance.sh
│       └── README.md
├── modules/
│   ├── core-defaults/
│   │   ├── README.md
│   │   └── required-workflows.md
│   └── optional-modules/
│       ├── README.md
│       ├── devcontainer.md
│       ├── security-scanning.md
│       └── code-coverage.md
├── .vscode/
│   ├── settings.json
│   └── extensions.json
├── README.md
└── LICENSE
```

All dev-workflow-os files are located in `/home/runner/work/.github/.github/templates/dev-workflow-os/`

### Key Documents

**Governance** (docs/governance/):
- README.md - Complete governance model
- coverage-matrix.md - Control → Enforcement → Artifact → Scope → Owner

**Standards** (docs/standards/):
- custom-agents.md - Agent roster and usage
- swarms.md - Multi-agent swarm definitions
- workflows.md - Workflow standards
- codeowners.md - CODEOWNERS best practices

**Diagrams** (docs/diagrams/) - All Mermaid format:
- system-architecture.mmd - Three-repo system overview
- repo-bootstrap-flow.mmd - New repository creation flow
- governance-stack.mmd - Layered governance approach
- defense-in-depth.mmd - Security layers
- issue-lifecycle.mmd - Issue state machine
- access-model.mmd - Permission model
- automation-map.mmd - Automation workflows

**Tables** (docs/tables/):
- github-projects-fields.md - Project field definitions
  - Status: Triage → Todo → In Progress → In Review → Blocked → Done
  - Priority: P0 / P1 / P2 / P3
  - Area: governance / ci / docs / devex / security / release
  - Owner Team, Target Date, Start Date, Effort (XS/S/M/L/XL)

**Policy** (policy/):
- rulesets/ruleset-v1.md - Ruleset standards
  - PR required
  - Required checks (policy-check, ci)
  - CODEOWNERS review
  - Restrict bypass
  - Block force-push
  - Block deletion
- required-files/README.md - Required file definitions

**Scripts** (scripts/gh/):
- Bash scripts for GitHub CLI automation
- Repository creation, ruleset application, label syncing, compliance auditing

## System Features

### Coverage Matrix

Documented in `dev-workflow-os/docs/governance/coverage-matrix.md`

Format:
| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| PR required | Org ruleset | Branch protection | main | Platform |
| Required checks | Org ruleset | policy-check, ci | main | Platform |
| CODEOWNERS review | Org ruleset | Branch protection | paths | Platform |

### Ruleset v1 Standards

Documented in `dev-workflow-os/policy/rulesets/ruleset-v1.md`

1. **PR Required**: All changes to main via pull request
2. **Required Checks**: policy-check and ci must pass
3. **CODEOWNERS Review**: Required for protected paths
4. **Restrict Bypass**: Only Platform Team + emergency
5. **Block Force-Push**: Prevent history rewriting
6. **Block Deletion**: Prevent branch deletion

### Folder Restrictions (Defense in Depth)

Layered approach:
1. **CODEOWNERS**: Review requirements by path
2. **Rulesets**: Enforce PR + required checks
3. **Workflows**: Automated validation (policy-check)
4. **Custom Agents**: Copilot guidance

### GitHub Projects v2 Fields

Documented in `dev-workflow-os/docs/tables/github-projects-fields.md`

**Status** (Single Select):
- Triage, Todo, In Progress, In Review, Blocked, Done

**Priority** (Single Select):
- P0 (Critical), P1 (High), P2 (Medium), P3 (Low)

**Area** (Single Select):
- governance, ci, docs, devex, security, release

**Additional Fields**:
- Owner Team (Text)
- Target Date, Start Date (Date)
- Effort (XS/S/M/L/XL)

**Built-in Automations**:
- Set Status to Todo when item added
- Set Status to Done when issue closed
- Close issue when Status moved to Done
- Set Start Date when moved to In Progress

### Custom Agent Roster

Documented in `dev-workflow-os/docs/standards/custom-agents.md`

**Agents**:
1. **Planner** - Strategic planning and task breakdown
2. **Repo Bootstrap** - Initialize new repositories
3. **Governance** - Ensure compliance with org standards
4. **CI/Automation** - Build and deployment pipelines
5. **Docs/Diagrams** - Documentation and architecture diagrams
6. **Security** - Security scanning and hardening
7. **Release/Change Mgmt** - Release coordination

### Swarm Definitions

Documented in `dev-workflow-os/docs/standards/swarms.md`

**Swarms**:
1. **Bootstrap Swarm** - Initialize new repository
   - Agents: Planner, Governance, CI, Docs
   
2. **Security Hardening Swarm** - Apply security best practices
   - Agents: Security, Governance, CI, Docs
   
3. **Release Swarm** - Coordinate release preparation
   - Agents: Release, CI, Security, Docs

## Placeholders

Throughout all files, use these placeholders:

- `ORG_NAME` - Organization name
- `ORG_PROJECT_URL` - GitHub Projects v2 URL
- `ADD_TO_PROJECT_PAT` - Personal Access Token for project automation
- `@org/platform-team` - Platform team GitHub handle
- `@org/[team-name]` - Team-specific handles
- `<CONTACT_EMAIL>` - Support email address
- `<SECURITY_EMAIL>` - Security contact email
- `[REPO_NAME]` - Repository-specific name

## Implementation Steps

### 1. Set Up ORG/.github

1. Ensure repository is PUBLIC
2. Add/update community health files
3. Create issue templates
4. Add workflow templates
5. Verify defaults apply org-wide

### 2. Create ORG/repo-template

1. Create repository from template in this repo
2. Mark as "Template repository" in settings
3. Customize README and placeholders
4. Test creating a new repo from template
5. Verify all required files copy correctly

### 3. Create ORG/dev-workflow-os

1. Create repository
2. Copy structure from template in this repo
3. Customize for your organization
4. Link to .github and repo-template
5. Document workflows and processes

### 4. Configure Organization Rulesets

1. Review policy/rulesets/ruleset-v1.md
2. Create rulesets via GitHub UI or API
3. Test on pilot repositories
4. Roll out organization-wide
5. Document and communicate

### 5. Set Up GitHub Projects

1. Create organization project
2. Configure fields per docs/tables/github-projects-fields.md
3. Set up built-in automations
4. Configure workflow secrets (ORG_PROJECT_URL, PAT)
5. Test automation

### 6. Train Teams

1. Share documentation
2. Demonstrate workflows
3. Explain governance model
4. Show custom agent usage
5. Support adoption

## Related Files

All implementation files are located in:
- `/home/runner/work/.github/.github/` - ORG/.github files (current repo)
- `/home/runner/work/.github/.github/templates/repo-template/` - Template files
- `/home/runner/work/.github/.github/templates/dev-workflow-os/` - Control plane files

## Questions?

For questions about implementation:
- Open an issue in this repository
- Tag @org/platform-team
- See SUPPORT.md for additional help
