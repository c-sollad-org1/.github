# Governance

This directory contains governance documentation for the ORG_NAME organization.

## Overview

The ORG_NAME governance model provides:

- **Clarity**: Clear roles, responsibilities, and decision-making processes
- **Consistency**: Standardized policies across all repositories
- **Compliance**: Documented controls and enforcement mechanisms
- **Flexibility**: Balance between standards and autonomy

## Governance Model

### Roles

#### Platform Team
**Responsibilities**:
- Maintain dev-workflow-os (this repo)
- Manage organization-level rulesets and policies
- Support repository owners with governance questions
- Approve governance change requests

**Authority**:
- Organization-wide policies and standards
- Ruleset configuration
- Required workflows and templates

#### Repository Owners
**Responsibilities**:
- Code quality and architecture for their repos
- Repo-specific workflow customization
- Issue triage and prioritization
- Team member permissions

**Authority**:
- Repo-level decisions (within org policies)
- Technology choices
- Development processes

#### Contributors
**Responsibilities**:
- Follow contribution guidelines
- Submit PRs that pass required checks
- Respond to review feedback
- Report issues and bugs

## Decision-Making Process

### Repo-Level Decisions
1. Repository Owner has final say
2. Must align with org-level policies
3. Document significant decisions (ADRs)
4. Communicate to team

### Org-Level Decisions
1. Open "Governance Change" issue in dev-workflow-os
2. Platform Team reviews
3. Impact assessment required
4. Approval before implementation
5. Rollout plan executed
6. Documentation updated

### Governance Changes
Use the [Governance Change issue template](https://github.com/ORG_NAME/.github/blob/main/.github/ISSUE_TEMPLATE/governance-change.yml).

**Required information**:
- Current state
- Proposed change
- Rationale
- Impact assessment
- Affected repositories
- Rollout plan

**Process**:
1. Issue opened
2. Platform Team reviews within 2 business days
3. Discussion period (minimum 3 days)
4. Decision documented in issue
5. Implementation coordinated
6. Documentation updated

## Three-Repository System

### ORG/.github (PUBLIC)
**Purpose**: Organization-wide default community health files

**Inheritance**:
- Files apply to all repos without their own versions
- MUST be public for defaults to work
- Do NOT add workflows here (workflows aren't inherited)

**Contains**:
- CODE_OF_CONDUCT.md
- CONTRIBUTING.md
- SECURITY.md
- SUPPORT.md
- GOVERNANCE.md
- PULL_REQUEST_TEMPLATE.md
- .github/ISSUE_TEMPLATE/*.yml
- workflow-templates/ (shareable, not inherited)

### ORG/repo-template
**Purpose**: Template for new repository creation

**Usage**:
- Click "Use this template" when creating repo
- Copies all structure to new repo
- Customize for specific needs

**Contains**:
- Complete repo structure
- Required workflows (these DO live in each repo)
- Copilot configuration
- Documentation structure

### ORG/dev-workflow-os (This Repo)
**Purpose**: Control plane and source of truth

**Usage**:
- Maintain policies and standards here
- Propagate changes to .github and repo-template
- Reference for all governance questions

**Contains**:
- Governance documentation
- Policy definitions
- Template sources
- Automation scripts
- Coverage matrices

## Key Governance Artifacts

### Rulesets
Organization-level rulesets enforce policies:

- [Ruleset v1 Standards](../../policy/rulesets/ruleset-v1.md)
- Main branch protection
- Required status checks
- CODEOWNERS enforcement

### Required Files
All repositories must have:

- README.md
- LICENSE
- .gitignore
- CODEOWNERS (or .github/CODEOWNERS)
- .github/copilot-instructions.md

See [Required Files](../../policy/required-files/README.md)

### Required Workflows
All repositories must include:

- policy-check.yml - Validates compliance
- add-to-project.yml - Adds issues/PRs to project
- dependency-review.yml - Security scanning
- ci.yml - Build and test (repo-specific)

See [Workflow Standards](../../docs/standards/workflows.md)

### CODEOWNERS
Path-based review requirements:

```
# Default owner for everything
* @org/platform-team

# Path-specific owners
/.github/ @org/platform-team
/docs/ @org/docs-team
/src/ @org/dev-team
```

See [CODEOWNERS Guide](../../docs/standards/codeowners.md)

## Coverage Matrix

The coverage matrix documents how controls are enforced:

- [Coverage Matrix](coverage-matrix.md)
- Maps control → enforcement → artifact → scope → owner
- Single source of truth for governance controls
- Updated with each governance change

## Defense in Depth

Multiple layers of protection:

1. **GitHub Platform**: Organization rulesets (hard enforcement)
2. **CODEOWNERS**: Path-based review requirements
3. **Workflows**: Automated checks (policy-check, CI, security)
4. **Custom Agents**: Copilot validation and assistance
5. **Human Review**: Code review and approval

See [Defense in Depth Diagram](../diagrams/defense-in-depth.mmd)

## GitHub Projects v2

Standard project configuration:

**Status Field** (Single Select):
- Triage - Newly created, needs review
- Todo - Accepted, ready to work
- In Progress - Active development
- In Review - PR open, under review
- Blocked - Waiting on dependencies
- Done - Complete

**Priority Field** (Single Select):
- P0 - Critical (immediate attention)
- P1 - High (this sprint)
- P2 - Medium (next sprint)
- P3 - Low (backlog)

**Area Field** (Single Select):
- governance
- ci
- docs
- devex
- security
- release

See [GitHub Projects Fields](../tables/github-projects-fields.md)

## Custom Agents

Specialized Copilot agents for governance:

- **Governance Agent**: Validate compliance, propose changes
- **Planner Agent**: Break down governance initiatives
- **CI Automation Agent**: Implement policy enforcement in workflows

See [Custom Agent Roster](../standards/custom-agents.md)

## Best Practices

### For Platform Team

1. **Document everything**: All policies in this repo
2. **Communicate early**: Notify before changes
3. **Test first**: Validate on test repos
4. **Rollout gradually**: Phased implementation
5. **Support teams**: Be available for questions

### For Repository Owners

1. **Align with org**: Follow standards unless justified
2. **Document divergence**: Explain repo-specific choices
3. **Keep workflows updated**: Don't remove required workflows
4. **Engage early**: Ask before governance changes
5. **Share learnings**: Contribute back to templates

### For Contributors

1. **Read guidelines**: CONTRIBUTING.md and SECURITY.md
2. **Use templates**: Issue and PR templates
3. **Pass checks**: Ensure policy-check and CI pass
4. **Be responsive**: Address review feedback
5. **Ask questions**: Tag relevant teams

## Compliance Checking

### Automated
- policy-check workflow runs on every PR and push
- Validates required files, prohibited patterns, governance alignment

### Manual Audits
- Quarterly reviews by Platform Team
- Check coverage matrix accuracy
- Review ruleset effectiveness
- Identify governance gaps

### Self-Service
Repository owners can check compliance:

```bash
# Check required files
ls -la README.md LICENSE .gitignore CODEOWNERS

# Validate CODEOWNERS syntax
gh api /repos/ORG_NAME/REPO_NAME/codeowners/errors

# List rulesets
gh api /orgs/ORG_NAME/rulesets
```

## Escalation

If consensus cannot be reached:

1. **Repo-level**: Repository Owner decides
2. **Org-level**: Platform Team decides
3. **Unresolved**: Escalate to organization leadership

## Resources

- [Organization Governance](https://github.com/ORG_NAME/.github/blob/main/GOVERNANCE.md)
- [Coverage Matrix](coverage-matrix.md)
- [Ruleset Standards](../../policy/rulesets/ruleset-v1.md)
- [Required Files](../../policy/required-files/README.md)
- [Governance Stack Diagram](../diagrams/governance-stack.mmd)

## Questions?

For governance questions:
- Open an issue with "governance" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
