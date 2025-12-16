# Governance Coverage Matrix

This document maps governance controls to their enforcement mechanisms, artifacts, scope, and ownership.

## Purpose

The coverage matrix serves as the **single source of truth** for understanding:
- What controls exist
- How they're enforced
- What implements them
- Where they apply
- Who owns them

## Matrix

| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| **Access & Authorization** ||||
| PR required before merge | Org ruleset | Main branch protection | main branch | Platform Team |
| CODEOWNERS review required | Org ruleset | Branch protection + CODEOWNERS | Protected paths | Platform Team |
| Bypass restrictions | Org ruleset | Ruleset bypass config | main branch | Platform Team |
| Repository permissions | GitHub Teams | Team membership + roles | All repos | Platform Team |
| **Code Quality** ||||
| Required status checks | Org ruleset | policy-check, ci workflows | main branch | Platform Team |
| Linting enforced | Workflow | ci.yml (lint job) | All branches | Repo Owners |
| Tests required | Workflow | ci.yml (test job) | All branches | Repo Owners |
| Code coverage tracking | Workflow | ci.yml (coverage report) | main, PRs | Repo Owners |
| **Security** ||||
| Dependency vulnerability scan | Workflow | dependency-review.yml | PRs | Platform Team |
| Secret scanning | GitHub native | Secret scanning alerts | All commits | Security Team |
| Code scanning (CodeQL) | Workflow | codeql-analysis.yml | main, PRs | Security Team |
| No hardcoded secrets | Workflow | policy-check.yml | All branches | Platform Team |
| **Repository Standards** ||||
| Required files present | Workflow | policy-check.yml | All repos | Platform Team |
| Copilot instructions exist | Workflow | policy-check.yml | All repos | Platform Team |
| CODEOWNERS not empty | Workflow | policy-check.yml | All repos | Platform Team |
| Valid .gitignore | Template | repo-template/.gitignore | All repos | Platform Team |
| **Branch Protection** ||||
| Block force push | Org ruleset | Branch protection | main branch | Platform Team |
| Block branch deletion | Org ruleset | Branch protection | main branch | Platform Team |
| Require linear history | Org ruleset | Branch protection | main branch | Platform Team |
| Dismiss stale reviews | Org ruleset | Branch protection | main branch | Platform Team |
| **Project Management** ||||
| Issues added to project | Workflow | add-to-project.yml | All repos | Platform Team |
| PRs added to project | Workflow | add-to-project.yml | All repos | Platform Team |
| Status field populated | Project automation | GitHub Projects | Project board | Platform Team |
| **Documentation** ||||
| README required | Workflow | policy-check.yml | All repos | Platform Team |
| Architecture docs | Template | repo-template/docs/ | All repos | Repo Owners |
| Runbooks for ops | Manual | docs/runbooks/ | Service repos | Repo Owners |
| API documentation | Manual | docs/api/ or inline | API repos | Repo Owners |
| **Change Management** ||||
| Breaking changes documented | Manual | CHANGELOG or migration guide | Releases | Repo Owners |
| Semantic versioning | Manual | Git tags, releases | Releases | Repo Owners |
| Release notes | Manual | GitHub Releases | Releases | Repo Owners |
| **Compliance** ||||
| License file present | Workflow | policy-check.yml | All repos | Platform Team |
| Code of Conduct | Org default | ORG/.github/CODE_OF_CONDUCT.md | All repos | Platform Team |
| Contributing guide | Org default | ORG/.github/CONTRIBUTING.md | All repos | Platform Team |
| Security policy | Org default | ORG/.github/SECURITY.md | All repos | Platform Team |

## Enforcement Mechanisms

### Org Ruleset
Hard enforcement at the GitHub organization level. Cannot be bypassed without explicit permission.

**Characteristics**:
- Applies to all repositories (or targeted subset)
- Enforced before commit/push/merge
- Requires Platform Team to modify
- Audit trail in GitHub audit log

### Workflow
Automated checks via GitHub Actions.

**Characteristics**:
- Runs on PR or push
- Can be required via branch protection
- Configurable per repository
- Visible in PR checks

### GitHub Native
Built-in GitHub features (secret scanning, Dependabot, etc.).

**Characteristics**:
- Enabled at org or repo level
- Minimal configuration required
- Managed by GitHub
- Alerts in Security tab

### Manual
Human review or process.

**Characteristics**:
- Relies on human judgment
- Documented in runbooks/guides
- No automated enforcement
- Verified in code review

### Template
Enforced by repo-template structure.

**Characteristics**:
- Applied when repo created
- Not actively enforced afterward
- Relies on policy-check for validation

### Project Automation
GitHub Projects v2 built-in automations.

**Characteristics**:
- Triggers on issue/PR events
- Updates project fields
- No code required
- Configured in project settings

## Coverage Analysis

### High Coverage Areas ✅
- Access control (rulesets + CODEOWNERS)
- Security scanning (workflows + GitHub native)
- Repository standards (policy-check workflow)
- Branch protection (rulesets)

### Medium Coverage Areas ⚠️
- Code quality (workflow-based, can be skipped locally)
- Project management (automation-based, not enforced)
- Documentation (template + manual)

### Low Coverage Areas ❌
- Change management (entirely manual)
- Breaking changes (no automated detection)
- Release quality (manual process)

## Gap Mitigation

For areas with lower automated coverage:

1. **Documentation**: Clear guidance in runbooks and templates
2. **Training**: Onboarding includes governance expectations
3. **Review**: CODEOWNERS ensures expert review
4. **Auditing**: Periodic compliance audits by Platform Team
5. **Culture**: Promote governance as enabler, not blocker

## Updating This Matrix

When adding or modifying controls:

1. Update this matrix with the new control
2. Update the enforcement mechanism if needed
3. Update the artifact (workflow, ruleset, etc.)
4. Test the control
5. Document in relevant runbooks
6. Communicate to affected teams

See [Coverage Matrix Update Prompt](../../templates/repo-template/.github/prompts/coverage-matrix-update.prompt.md) for detailed guidance.

## Related Documentation

- [Ruleset Standards](../../policy/rulesets/ruleset-v1.md)
- [Required Files](../../policy/required-files/README.md)
- [Governance Model](README.md)
- [Defense in Depth Diagram](../diagrams/defense-in-depth.mmd)

## Questions?

For questions about coverage or gaps:
- Open an issue with the "governance" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
