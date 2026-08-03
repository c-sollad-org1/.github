# Governance Coverage Matrix

This document maps governance controls to their enforcement mechanisms, artifacts, scope, ownership, and current implementation status.

## Purpose

The coverage matrix serves as the **single source of truth** for understanding:
- What controls exist
- How they are enforced
- What implements them
- Where they apply
- Who owns them
- **Whether they are actually in place right now**

## Allowed Statuses

Every row carries exactly one status from this list. No other value is permitted.

| Status | Meaning | When to use |
|---|---|---|
| `Implemented` | The control is in place and enforcing today. | Verified against the live system, not against intent. |
| `Blocked By [what]` | The control is intended and not in place because something specific prevents it. The bracket is required and must name the blocker. | Use when the obstacle is identifiable and removable. Example: `Blocked By [gate deployed to 1 of 6 repos]`. |
| `Declined` | A decision was made not to implement this control. | Use when the choice is settled. The row stays in the matrix so the decision is visible rather than reappearing as a gap. |
| `Waiting on Agent or User` | The control is intended, nothing blocks it, and nobody has done it yet. | The default for a designed-but-unbuilt control. |

Rules for status:

1. A status is a claim about the live system. Verify before setting it, do not infer from the presence of a file or a rule name.
2. `Implemented` requires that the named artifact exists AND does what the control says. A workflow whose step is `echo` is not an implementation.
3. `Blocked By` must name the blocker inside the brackets. `Blocked By [pending]` is not a valid status.
4. When a control is removed or turned off, change the status in the same change. A row that silently keeps saying `Implemented` is worse than no row.

## Matrix

| Control | Enforcement | Artifact | Scope | Owner | Status |
|---------|-------------|----------|-------|-------|--------|
| **Access & Authorization** ||||||
| PR required before merge | Org ruleset | RuleSetV1 pull_request rule | main branch | Platform Team | `Implemented` |
| CODEOWNERS review required | Org ruleset | Branch protection + CODEOWNERS | Protected paths | Platform Team | `Waiting on Agent or User` |
| Bypass restrictions | Org ruleset | RuleSetV1 bypass_actors | main branch | Platform Team | `Implemented` |
| Repository permissions | GitHub Teams | Team membership + roles | All repos | Platform Team | `Waiting on Agent or User` |
| **Code Quality** ||||||
| Required status checks | Org ruleset | required-checks aggregator | main branch | Platform Team | `Blocked By [rule removed from RuleSetV1; gate deployed to 1 of 6 repos]` |
| Linting enforced | Workflow | ci.yml lint job | All branches | Repo Owners | `Waiting on Agent or User` |
| Tests required | Workflow | ci.yml test job | All branches | Repo Owners | `Waiting on Agent or User` |
| Code coverage tracking | Workflow | ci.yml coverage report | main, PRs | Repo Owners | `Waiting on Agent or User` |
| **Security** ||||||
| Dependency vulnerability scan | Workflow | dependency-review.yml | PRs | Platform Team | `Waiting on Agent or User` |
| Secret scanning | GitHub native | Secret scanning alerts | All commits | Security Team | `Waiting on Agent or User` |
| Secret push protection | GitHub native | Push protection | All pushes | Security Team | `Waiting on Agent or User` |
| Code scanning (CodeQL) | GitHub native | Default setup or codeql workflow | main, PRs | Security Team | `Declined` |
| Workflow security scanning | Workflow | zizmor job in required-checks | PRs | Platform Team | `Blocked By [gate deployed to 1 of 6 repos]` |
| No hardcoded secrets | Workflow | trufflehog job in required-checks | PRs | Platform Team | `Blocked By [gate deployed to 1 of 6 repos]` |
| **Repository Standards** ||||||
| Required files present | Workflow | policy-check.yml | dev-workflow-os only | Platform Team | `Blocked By [workflow exists in 1 repo, not org-wide]` |
| Copilot instructions exist | Workflow | policy-check.yml | All repos | Platform Team | `Waiting on Agent or User` |
| CODEOWNERS not empty | Workflow | policy-check.yml | All repos | Platform Team | `Waiting on Agent or User` |
| Valid .gitignore | Template | repo-template/.gitignore | All repos | Platform Team | `Waiting on Agent or User` |
| **Branch Protection** ||||||
| Block force push | Org ruleset | RuleSetV1 non_fast_forward | main branch | Platform Team | `Implemented` |
| Block branch deletion | Org ruleset | RuleSetV1 deletion | main branch | Platform Team | `Implemented` |
| Require linear history | Org ruleset | RuleSetV1 required_linear_history | main branch | Platform Team | `Implemented` |
| Dismiss stale reviews | Org ruleset | RuleSetV1 dismiss_stale_reviews_on_push | main branch | Platform Team | `Implemented` |
| Conversation resolution required | Org ruleset | RuleSetV1 required_review_thread_resolution | main branch | Platform Team | `Implemented` |
| **Project Management** ||||||
| Issues added to project | Workflow | add-to-project.yml | All repos | Platform Team | `Waiting on Agent or User` |
| PRs added to project | Workflow | add-to-project.yml | All repos | Platform Team | `Waiting on Agent or User` |
| Status field populated | Project automation | GitHub Projects | Project board | Platform Team | `Waiting on Agent or User` |
| **Documentation** ||||||
| README required | Workflow | policy-check.yml | dev-workflow-os only | Platform Team | `Blocked By [workflow exists in 1 repo, not org-wide]` |
| Architecture docs | Template | repo-template/docs/ | All repos | Repo Owners | `Waiting on Agent or User` |
| Runbooks for ops | Manual | docs/runbooks/ | Service repos | Repo Owners | `Waiting on Agent or User` |
| API documentation | Manual | docs/api/ or inline | API repos | Repo Owners | `Waiting on Agent or User` |
| **Change Management** ||||||
| Breaking changes documented | Manual | CHANGELOG or migration guide | Releases | Repo Owners | `Waiting on Agent or User` |
| Semantic versioning | Manual | Git tags, releases | Releases | Repo Owners | `Waiting on Agent or User` |
| Release notes | Manual | GitHub Releases | Releases | Repo Owners | `Waiting on Agent or User` |
| **Compliance** ||||||
| License file present | Workflow | policy-check.yml | All repos | Platform Team | `Waiting on Agent or User` |
| Code of Conduct | Org default | ORG/.github/CODE_OF_CONDUCT.md | All repos | Platform Team | `Waiting on Agent or User` |
| Contributing guide | Org default | ORG/.github/CONTRIBUTING.md | All repos | Platform Team | `Waiting on Agent or User` |
| Security policy | Org default | ORG/.github/SECURITY.md | All repos | Platform Team | `Waiting on Agent or User` |

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

**Caveat**: a workflow only enforces a control in the repositories where the workflow file exists. A workflow present in one repository is not an org-wide control.

### GitHub Native
Built-in GitHub features (secret scanning, Dependabot, etc.).

**Characteristics**:
- Enabled at org or repo level
- Minimal configuration required
- Managed by GitHub
- Alerts in Security tab

**Caveat**: these are off by default on private repositories. Presence of the feature is not the same as it being enabled.

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

**Caveat**: template instantiation is a one-time copy with no shared ancestry. A template change never reaches repositories created before it.

### Project Automation
GitHub Projects v2 built-in automations.

**Characteristics**:
- Triggers on issue/PR events
- Updates project fields
- No code required
- Configured in project settings

## Coverage Analysis

Counts are derived from the Status column. Update them when a status changes.

| Status | Count |
|---|---|
| `Implemented` | 8 |
| `Blocked By` | 5 |
| `Declined` | 1 |
| `Waiting on Agent or User` | 23 |

The only controls enforcing today are branch protections and the pull request requirement, all of which come from the org ruleset. Every workflow-based and GitHub-native control is either not deployed org-wide or not enabled.

## Gap Mitigation

For areas with lower automated coverage:

1. **Documentation**: clear guidance in runbooks and templates
2. **Training**: onboarding includes governance expectations
3. **Review**: CODEOWNERS ensures expert review
4. **Auditing**: periodic compliance audits by Platform Team
5. **Culture**: promote governance as enabler, not blocker

## Updating This Matrix

When adding or modifying controls:

1. Update this matrix with the new control
2. Update the enforcement mechanism if needed
3. Update the artifact (workflow, ruleset, etc.)
4. Test the control
5. **Set the status from verified evidence, not from intent**
6. Update the Coverage Analysis counts
7. Document in relevant runbooks
8. Communicate to affected teams

## Related Documentation

- [Ruleset Standards](../../policy/rulesets/ruleset-v1.md)
- [Required Files](../../policy/required-files/README.md)
- [Governance Model](README.md)
- [Defense in Depth Diagram](../diagrams/defense-in-depth.mmd)

## Questions?

For questions about coverage or gaps:
- Open an issue with the "governance" label
- Tag the platform team
