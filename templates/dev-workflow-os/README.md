# Dev Workflow OS v1

**Control Plane and Source of Truth for ORG_NAME Development Infrastructure**

This repository is the **single source of truth** for development workflow governance, standards, templates, and automation across the ORG_NAME organization.

## What is Dev Workflow OS?

Dev Workflow OS is a comprehensive system for managing development workflows at scale:

- 🏛️ **Governance**: Policies, standards, and compliance controls
- 📋 **Templates**: Reusable templates for repos, workflows, and documentation
- 🤖 **Automation**: Scripts and tools for consistent operations
- 📊 **Visibility**: Coverage matrices and compliance tracking
- 🔒 **Security**: Defense-in-depth approach to repository security

## Repository Structure

```
dev-workflow-os/
├── docs/                   # Documentation
│   ├── standards/          # Coding and process standards
│   ├── governance/         # Governance documentation
│   ├── diagrams/           # Architecture diagrams (Mermaid)
│   ├── tables/             # Reference tables and matrices
│   └── runbooks/           # Operational procedures
├── policy/                 # Policy definitions
│   ├── rulesets/           # Repository ruleset configurations
│   ├── labels/             # Standard label definitions
│   └── required-files/     # Required file templates
├── templates/              # Reusable templates
│   ├── repo-template/      # New repository template
│   └── org-dotgithub/      # Organization defaults template
├── scripts/                # Automation scripts
│   └── gh/                 # GitHub CLI scripts
├── modules/                # Modular components
│   ├── core-defaults/      # Required defaults
│   └── optional-modules/   # Optional enhancements
└── .vscode/                # VS Code workspace settings
```

## Three-Repository System

Dev Workflow OS consists of three interconnected repositories:

### 1. ORG/.github (Org Defaults Repo) - PUBLIC

**Purpose**: Organization-wide default community health files and workflow templates

**Contains**:
- CODE_OF_CONDUCT.md
- CONTRIBUTING.md
- SECURITY.md
- SUPPORT.md
- GOVERNANCE.md
- PULL_REQUEST_TEMPLATE.md
- .github/ISSUE_TEMPLATE/*.yml (issue forms)
- workflow-templates/ (shareable workflow templates)

**Visibility**: MUST be public for defaults to apply org-wide

**Inheritance**: Default files apply to all repos that don't have their own versions

### 2. ORG/repo-template (Template Repo)

**Purpose**: Template for creating new repositories with all required structure

**Contains**:
- Complete repo structure (README, LICENSE, .gitignore, CODEOWNERS)
- .github/workflows/ (policy-check, add-to-project, dependency-review, ci)
- .github/copilot-instructions.md
- .github/instructions/*.instructions.md
- .github/agents/*.agent.md (custom agent profiles)
- .github/prompts/*.prompt.md (reusable prompts)
- .vscode/ configuration
- docs/ structure
- Optional: .devcontainer/

**Usage**: Click "Use this template" when creating a new repository

### 3. ORG/dev-workflow-os (This Repo - Control Plane)

**Purpose**: Source of truth for governance, policies, templates, and automation

**Contains**:
- Governance documentation and standards
- Policy definitions (rulesets, labels, required files)
- Template sources (maintained here, copied to other repos)
- Automation scripts for org management
- Coverage matrices and compliance tracking
- Diagrams and architecture documentation

**Workflow**: Changes here drive updates to .github and repo-template

## Key Features

### Coverage Matrix

Track governance controls across the organization:

| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| PR required | Org ruleset | Branch protection | main | Platform |
| Required checks | Org ruleset | policy-check, ci | main | Platform |
| CODEOWNERS review | Org ruleset | Branch protection | protected paths | Platform |

See [docs/governance/coverage-matrix.md](docs/governance/coverage-matrix.md)

### Ruleset v1 Standards

Organization-wide repository rulesets enforce:

1. **PR Required**: All changes to main via pull request
2. **Required Checks**: policy-check and ci workflows must pass
3. **CODEOWNERS Review**: Required for protected paths
4. **Restrict Bypass**: Only Platform Team + emergency access
5. **Block Force Push**: Prevent history rewriting
6. **Block Deletion**: Prevent branch deletion

See [policy/rulesets/](policy/rulesets/)

### GitHub Projects v2 Configuration

Standard field set for project tracking:

- **Status**: Triage → Todo → In Progress → In Review → Blocked → Done
- **Priority**: P0 (Critical) / P1 (High) / P2 (Medium) / P3 (Low)
- **Area**: governance / ci / docs / devex / security / release
- **Owner Team**: Assigned team
- **Dates**: Target Date, Start Date
- **Effort**: XS / S / M / L / XL

Built-in automations:
- Set Status to Todo when item added
- Set Status to Done when issue closed
- Close issue when Status moved to Done

See [docs/tables/github-projects-fields.md](docs/tables/github-projects-fields.md)

### Custom Agent Roster

Specialized Copilot agents for domain-specific tasks:

- **Planner**: Strategic planning and task breakdown
- **Repo Bootstrap**: Initialize new repositories
- **Governance**: Ensure compliance with org standards
- **CI/Automation**: Build and deployment pipelines
- **Docs/Diagrams**: Documentation and architecture diagrams
- **Security**: Security scanning and hardening
- **Release/Change Mgmt**: Release coordination

See [docs/standards/custom-agents.md](docs/standards/custom-agents.md)

### Swarm Definitions

Coordinate multiple agents for complex tasks:

- **Bootstrap Swarm**: Initialize a new repository
  - Agents: Planner, Governance, CI, Docs
- **Security Hardening Swarm**: Apply security best practices
  - Agents: Security, Governance, CI, Docs
- **Release Swarm**: Coordinate release preparation
  - Agents: Release, CI, Security, Docs

See [docs/standards/swarms.md](docs/standards/swarms.md)

## Getting Started

### For Platform Team

1. Clone this repository
2. Review governance documentation in `docs/governance/`
3. Understand the three-repository system
4. Make changes here, then propagate to .github and repo-template

### For Repository Owners

1. Review [docs/governance/README.md](docs/governance/README.md)
2. Use repo-template when creating new repositories
3. Follow required workflows and governance
4. Open governance change issues for org-wide changes

### For Contributors

1. Read [CONTRIBUTING.md](https://github.com/ORG_NAME/.github/blob/main/CONTRIBUTING.md)
2. Use issue templates in ORG/.github
3. Follow PR requirements (policy-check, CODEOWNERS review)
4. Leverage custom agents for specialized tasks

## Making Changes

### Governance Changes

1. Open a "Governance Change" issue
2. Tag @org/platform-team
3. Provide impact assessment
4. Get approval before implementing

### Template Updates

1. Update templates in this repo
2. Test changes
3. Propagate to .github and repo-template
4. Communicate to affected teams

### Policy Updates

1. Document changes in policy/
2. Update coverage matrix
3. Apply rulesets via GitHub API
4. Notify repository owners

## Architecture

See the architecture diagrams:

- [System Architecture](docs/diagrams/system-architecture.mmd)
- [New Repo Bootstrap Flow](docs/diagrams/repo-bootstrap-flow.mmd)
- [Governance Stack](docs/diagrams/governance-stack.mmd)
- [Defense in Depth](docs/diagrams/defense-in-depth.mmd)

## Documentation

- [Standards](docs/standards/) - Coding and process standards
- [Governance](docs/governance/) - Governance model and policies
- [Diagrams](docs/diagrams/) - Architecture diagrams
- [Tables](docs/tables/) - Reference tables and matrices
- [Runbooks](docs/runbooks/) - Operational procedures

## Automation

Scripts for managing the organization:

- [scripts/gh/](scripts/gh/) - GitHub CLI automation scripts
  - Create repositories
  - Apply rulesets
  - Manage labels
  - Audit compliance

## Support

For questions or issues:

- Open an issue with appropriate label
- Tag @org/platform-team for platform questions
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)

## License

See [LICENSE](LICENSE)

## Related Repositories

- [ORG/.github](https://github.com/ORG_NAME/.github) - Organization defaults
- [ORG/repo-template](https://github.com/ORG_NAME/repo-template) - Repository template
