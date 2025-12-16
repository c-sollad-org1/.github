# Governance Instructions

**Apply to**: `**/GOVERNANCE.md`, `**/.github/workflows/*.yml`, `**/policy/**`, `**/CODEOWNERS`

## Context

This repository follows the **ORG_NAME Dev Workflow OS v1** governance model. Changes to governance files require Platform Team review and alignment with organization-wide standards.

## When Making Governance Changes

### 1. Understand the Scope

- **Repo-level changes**: Affect only this repository (e.g., CODEOWNERS, repo-specific workflow)
- **Org-level changes**: Require coordination across repos (e.g., changing required checks, rulesets)

### 2. Check Alignment

Before making changes:

- Review [dev-workflow-os governance docs](https://github.com/ORG_NAME/dev-workflow-os/tree/main/docs/governance)
- Check current org rulesets: `gh api /orgs/ORG_NAME/rulesets`
- Verify required files list in [policy/required-files](https://github.com/ORG_NAME/dev-workflow-os/tree/main/policy/required-files)

### 3. Required Workflows

This repository must include:

- `policy-check.yml`: Validates repo compliance
- `add-to-project.yml`: Adds issues/PRs to project board
- `dependency-review.yml`: Security scanning
- `ci.yml`: Build and test pipeline (customized per repo)

Do not remove or disable these workflows.

### 4. CODEOWNERS Syntax

```
# Default owner
* @org/platform-team

# Path-specific owners (order matters - last match wins)
/docs/ @org/docs-team
/src/api/ @org/backend-team
/.github/ @org/platform-team
```

### 5. Rulesets

Rulesets are configured at the **organization level** and cannot be overridden in individual repos. If you need a ruleset change:

1. Open a "Governance Change" issue in [dev-workflow-os](https://github.com/ORG_NAME/dev-workflow-os)
2. Tag @org/platform-team
3. Provide justification and impact assessment

### 6. Coverage Matrix

When adding new controls (security checks, required reviews, etc.), update the coverage matrix in:

- `docs/governance/coverage-matrix.md`

Format:

| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| PR required | Ruleset | Branch protection | main | Platform |

### 7. Testing Governance Changes

Before merging:

- Test workflow changes in a draft PR
- Verify CODEOWNERS syntax: `gh api /repos/ORG_NAME/REPO/codeowners/errors`
- Run `policy-check` workflow manually

### 8. Communication

For significant governance changes:

- Notify affected teams via PR comment
- Update repo documentation
- If org-wide, coordinate through dev-workflow-os

## Key Principles

1. **Consistency**: Align with org standards unless there's a strong repo-specific reason
2. **Transparency**: Document why governance differs from defaults
3. **Defense in depth**: Layer controls (CODEOWNERS + rulesets + CI)
4. **Automation**: Use workflows to enforce, not just document

## Common Mistakes to Avoid

- ❌ Removing required workflows
- ❌ Making CODEOWNERS changes without team notification
- ❌ Bypassing rulesets instead of requesting exemption
- ❌ Adding conflicting workflow logic
- ❌ Hardcoding secrets in workflows

## Resources

- [Org governance docs](https://github.com/ORG_NAME/dev-workflow-os/tree/main/docs/governance)
- [Ruleset standards](https://github.com/ORG_NAME/dev-workflow-os/tree/main/policy/rulesets)
- [Platform Team](https://github.com/orgs/ORG_NAME/teams/platform-team)
