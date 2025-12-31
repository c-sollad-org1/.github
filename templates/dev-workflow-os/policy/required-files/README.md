# Required Files

All repositories in ORG_NAME must maintain these required files.

## Core Files

### README.md

**Purpose**: Project overview and getting started guide

**Required sections**:
- One-line description
- Overview
- Getting started (prerequisites, installation, usage)
- Development (building, testing)
- Documentation links
- Contributing link
- License reference
- Support information

**Location**: Repository root

**Validation**: Checked by policy-check.yml workflow

**Template**: See [repo-template/README.md](../../templates/repo-template/README.md)

### LICENSE

**Purpose**: Legal terms for code usage and distribution

**Required**: Yes (choose appropriate license)

**Common options**:
- MIT (most permissive, recommended for open source)
- Apache 2.0 (includes patent grant)
- Proprietary (for private/internal code)

**Location**: Repository root

**Validation**: Checked by policy-check.yml workflow

**Template**: See [repo-template/LICENSE](../../templates/repo-template/LICENSE)

### .gitignore

**Purpose**: Prevent committing build artifacts, dependencies, and secrets

**Required**: Yes

**Must include**:
- OS-specific files (.DS_Store, Thumbs.db)
- IDE files (.vscode/*, .idea/)
- Build artifacts (dist/, build/, target/)
- Dependencies (node_modules/, vendor/, venv/)
- Environment files (.env, .env.local)
- Secrets (*.key, *.pem)

**Location**: Repository root

**Validation**: Checked by policy-check.yml workflow

**Template**: See [repo-template/.gitignore](../../templates/repo-template/.gitignore)

## GitHub Configuration Files

### CODEOWNERS

**Purpose**: Define code ownership for automated review assignment

**Required**: Yes

**Format**:
```
# Default owner for everything
* @org/platform-team

# Path-specific owners
/.github/ @org/platform-team
/docs/ @org/docs-team
/src/ @org/dev-team
```

**Location**: 
- `.github/CODEOWNERS` (preferred)
- `CODEOWNERS` (root, also valid)

**Validation**: 
- Checked by policy-check.yml workflow
- Must not be empty
- Syntax validated via: `gh api /repos/ORG_NAME/REPO/codeowners/errors`

**Template**: See [repo-template/CODEOWNERS](../../templates/repo-template/CODEOWNERS)

**Best practices**:
- Start with default owner (`* @org/team`)
- Add path-specific owners for specialized areas
- Order matters: last match wins
- Use teams, not individuals (for continuity)
- Keep .github/ owned by Platform Team

### .github/copilot-instructions.md

**Purpose**: Provide context and standards for GitHub Copilot

**Required**: Yes

**Must include**:
- Project overview
- Coding standards
- Testing guidelines
- Commit and PR conventions
- Architecture guidelines
- Security considerations
- Integration with org governance

**Location**: `.github/copilot-instructions.md`

**Validation**: Checked by policy-check.yml workflow

**Template**: See [repo-template/.github/copilot-instructions.md](../../templates/repo-template/.github/copilot-instructions.md)

## Workflow Files

### .github/workflows/policy-check.yml

**Purpose**: Validate repository compliance with org policies

**Required**: Yes

**Checks**:
- Required files present
- Prohibited patterns (hardcoded secrets, etc.)
- Governance alignment

**Location**: `.github/workflows/policy-check.yml`

**Template**: See [repo-template/.github/workflows/policy-check.yml](../../templates/repo-template/.github/workflows/policy-check.yml)

**Notes**:
- Must be present and enabled
- Required as status check in branch protection
- Do not disable or remove

### .github/workflows/add-to-project.yml

**Purpose**: Automatically add issues and PRs to project board

**Required**: Yes

**Location**: `.github/workflows/add-to-project.yml`

**Template**: See [repo-template/.github/workflows/add-to-project.yml](../../templates/repo-template/.github/workflows/add-to-project.yml)

**Configuration**:
Requires secrets:
- `ORG_PROJECT_URL`: Project URL
- `ADD_TO_PROJECT_PAT`: PAT with project write access

### .github/workflows/dependency-review.yml

**Purpose**: Scan PRs for vulnerable dependencies

**Required**: Yes

**Location**: `.github/workflows/dependency-review.yml`

**Template**: See [repo-template/.github/workflows/dependency-review.yml](../../templates/repo-template/.github/workflows/dependency-review.yml)

### .github/workflows/ci.yml

**Purpose**: Build and test pipeline

**Required**: Yes (customized per repo)

**Location**: `.github/workflows/ci.yml`

**Must include**:
- Linting
- Testing
- Building

**Template**: See [repo-template/.github/workflows/ci.yml](../../templates/repo-template/.github/workflows/ci.yml)

**Notes**:
- Customize for your tech stack
- Required as status check in branch protection
- Must pass before merge

## Documentation Structure

### docs/architecture/README.md

**Purpose**: Architecture overview and decisions

**Required**: Yes (structure, content evolves)

**Location**: `docs/architecture/README.md`

**Template**: See [repo-template/docs/architecture/README.md](../../templates/repo-template/docs/architecture/README.md)

### docs/governance/README.md

**Purpose**: Repository-specific governance documentation

**Required**: Yes

**Location**: `docs/governance/README.md`

**Template**: See [repo-template/docs/governance/README.md](../../templates/repo-template/docs/governance/README.md)

### docs/runbooks/README.md

**Purpose**: Operational procedures

**Required**: Yes (structure, content varies by repo type)

**Location**: `docs/runbooks/README.md`

**Template**: See [repo-template/docs/runbooks/README.md](../../templates/repo-template/docs/runbooks/README.md)

## Optional but Recommended

### CHANGELOG.md

**Purpose**: Track notable changes between versions

**Recommended for**: Libraries, services with versioned releases

**Format**: [Keep a Changelog](https://keepachangelog.com/)

### SECURITY.md

**Purpose**: Security policy and vulnerability reporting

**Note**: Inherited from ORG/.github by default

**Override if**: Repo has specific security procedures

### CONTRIBUTING.md

**Purpose**: Contribution guidelines

**Note**: Inherited from ORG/.github by default

**Override if**: Repo has specific contribution process

### .devcontainer/devcontainer.json

**Purpose**: Development container configuration

**Recommended for**: Projects with complex dependencies

**Template**: See [repo-template/.devcontainer/devcontainer.json](../../templates/repo-template/.devcontainer/devcontainer.json)

**Note**: Marked as OPTIONAL_MODULE in template

## Enforcement

### Automated Checks

The `policy-check.yml` workflow validates required files on every PR and push to main:

```bash
# Checks for existence
- README.md
- LICENSE
- .gitignore
- CODEOWNERS (in either location)
- .github/copilot-instructions.md

# Validates content
- CODEOWNERS not empty
- No hardcoded secrets (basic check)
```

### Manual Verification

Repository owners should periodically verify:

```bash
# Check all required files exist
ls -la README.md LICENSE .gitignore CODEOWNERS .github/copilot-instructions.md

# Validate CODEOWNERS syntax
gh api /repos/ORG_NAME/REPO_NAME/codeowners/errors

# Check workflows are enabled
gh workflow list

# Verify policy-check passes
gh run list --workflow=policy-check.yml --limit 5
```

### Non-Compliance

If a repository is missing required files:

1. policy-check workflow fails
2. PR cannot be merged (if policy-check is required check)
3. Repository owners notified
4. Platform Team can assist with remediation

## New Repository Setup

When creating a new repository:

1. **Use repo-template**: "Use this template" button
2. **Verify files**: All required files copied
3. **Customize**: Update placeholders with repo-specific details
4. **Validate**: Run policy-check workflow
5. **Confirm**: Ensure all checks pass

See [New Repo Bootstrap Prompt](../../templates/repo-template/.github/prompts/new-repo-bootstrap.prompt.md)

## Updating Required Files

To update the list of required files:

1. Open "Governance Change" issue in dev-workflow-os
2. Justify the addition/removal
3. Get Platform Team approval
4. Update policy-check.yml workflow
5. Update this documentation
6. Update repo-template
7. Communicate to all teams
8. Support existing repos with migration

## Related Documentation

- [Coverage Matrix](../../docs/governance/coverage-matrix.md)
- [Governance Model](../../docs/governance/README.md)
- [Repo Template](../../templates/repo-template/)
- [Policy Check Workflow](../../templates/repo-template/.github/workflows/policy-check.yml)

## Questions?

For questions about required files:
- Open an issue with "governance" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
