# Governance

This directory contains governance documentation specific to this repository.

## Contents

- **Coverage Matrix**: Control enforcement mapping
- **Rulesets**: Repository-specific rulesets (if any)
- **Policies**: Repository-specific policies

## Organization-Level Governance

This repository follows the **ORG_NAME Dev Workflow OS v1** governance model.

For organization-wide governance:
- See [ORG_NAME/.github](https://github.com/ORG_NAME/.github)
- See [dev-workflow-os](https://github.com/ORG_NAME/dev-workflow-os)

## Repository-Specific Governance

### CODEOWNERS

This repository uses CODEOWNERS for review requirements:

```
* @org/[team-name]
/.github/ @org/platform-team
```

See [CODEOWNERS](../../CODEOWNERS) or [.github/CODEOWNERS](../../.github/CODEOWNERS) for full details.

### Required Workflows

This repository includes these required workflows:

1. **policy-check**: Validates repository compliance
2. **add-to-project**: Adds issues/PRs to project board
3. **dependency-review**: Security scanning for dependencies
4. **ci**: Build and test pipeline

### Branch Protection

The `main` branch is protected by organization-level rulesets:

- ✅ Pull request required before merge
- ✅ Required status checks must pass
- ✅ CODEOWNERS review required
- ✅ Force push blocked
- ✅ Branch deletion blocked

### Coverage Matrix

The coverage matrix documents how governance controls are enforced.

| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| PR required | Org ruleset | Branch protection | main | Platform |
| Required checks | Org ruleset | policy-check, ci | main | Platform |
| CODEOWNERS review | Org ruleset | Branch protection | protected paths | Platform |
| Dependency review | Workflow | dependency-review.yml | PRs | Platform |
| Code quality | Workflow | ci.yml (lint, test) | all branches | Repo Owners |

## Making Governance Changes

### Repo-Level Changes

For changes that only affect this repository:

1. Open an issue with the "governance" label
2. Propose the change with rationale
3. Get approval from repository owners
4. Update documentation
5. Implement via PR

### Org-Level Changes

For changes that affect the organization:

1. Open a "Governance Change" issue in [dev-workflow-os](https://github.com/ORG_NAME/dev-workflow-os)
2. Tag @org/platform-team
3. Provide impact assessment
4. Follow the governance change process

## Compliance

### Required Files

This repository must maintain:

- ✅ README.md
- ✅ LICENSE
- ✅ .gitignore
- ✅ CODEOWNERS
- ✅ .github/copilot-instructions.md

### Required Workflows

All workflows in `.github/workflows/` must be maintained. Do not remove or disable required workflows.

### Auditing

The `policy-check` workflow runs on every PR and push to `main` to verify compliance.

To run locally:
```bash
# Check required files
ls -la README.md LICENSE .gitignore CODEOWNERS

# Validate CODEOWNERS syntax
gh api /repos/ORG_NAME/REPO_NAME/codeowners/errors
```

## Resources

- [Org Governance](https://github.com/ORG_NAME/.github/blob/main/GOVERNANCE.md)
- [Dev Workflow OS](https://github.com/ORG_NAME/dev-workflow-os)
- [Governance Agent](.github/agents/governance.agent.md)
- [Governance Instructions](.github/instructions/governance.instructions.md)

## Questions?

For governance questions:
- Open an issue with the "governance" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
