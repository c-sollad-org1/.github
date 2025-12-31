# Prompt: Ruleset Update

## Purpose

Update or create repository rulesets to enforce governance policies. Use this when adding new protection rules or modifying existing ones.

## Context

Rulesets are configured at the **organization level** and apply to repos based on target rules. Individual repos cannot override org rulesets, so changes require Platform Team approval.

## When to Use

- Adding new required status checks
- Modifying branch protection rules
- Enforcing CODEOWNERS review
- Restricting branch operations (force push, deletion)
- Configuring bypass permissions

## Prerequisites

- Governance Change issue opened in dev-workflow-os
- Platform Team approval
- Impact assessment completed

## Prompt Template

```
Update ruleset: [RULESET_NAME]

Change type: [CREATE_NEW | MODIFY_EXISTING | DELETE]

Current state:
- Ruleset: [NAME] (if existing)
- Target: [BRANCH_PATTERN or TAG_PATTERN]
- Current rules: [LIST_CURRENT_RULES]

Proposed changes:
- [ ] Add required status check: [CHECK_NAME]
- [ ] Require pull request before merge
- [ ] Require CODEOWNERS review
- [ ] Require linear history
- [ ] Block force pushes
- [ ] Restrict deletions
- [ ] Restrict creations
- [ ] Configure bypass list: [USERS/TEAMS/APPS]

Rationale:
[Why is this change needed?]

Impact assessment:
- Affected repositories: [LIST or "all repos"]
- Breaking change: [YES/NO]
- Affects existing PRs: [YES/NO]
- Team notifications needed: [YES/NO - which teams?]

Rollout plan:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Success criteria:
- [ ] Ruleset created/updated in GitHub
- [ ] Policy documented in dev-workflow-os
- [ ] Coverage matrix updated
- [ ] Teams notified
- [ ] Verified on test repository
```

## Ruleset v1 Standards

Organization-wide baseline:

1. **PR Required**: All changes to `main` via pull request
2. **Required Checks**: 
   - `policy-check` workflow must pass
   - `ci` workflow must pass (repo-specific tests)
3. **CODEOWNERS Review**: Required for paths with CODEOWNERS
4. **Restrict Bypass**: Only Platform Team + emergency access
5. **Block Force Push**: Prevent history rewriting
6. **Block Deletion**: Prevent branch deletion

## GitHub CLI Commands

### List Rulesets

```bash
gh api /orgs/ORG_NAME/rulesets
```

### Get Ruleset Details

```bash
gh api /orgs/ORG_NAME/rulesets/[RULESET_ID]
```

### Create Ruleset

```bash
gh api /orgs/ORG_NAME/rulesets \
  --method POST \
  --field name="[RULESET_NAME]" \
  --field enforcement="active" \
  --field target="branch" \
  --field 'conditions[ref_name][include][]="refs/heads/main"'
```

### Update Ruleset

```bash
gh api /orgs/ORG_NAME/rulesets/[RULESET_ID] \
  --method PUT \
  --field name="[RULESET_NAME]" \
  ...
```

## Common Scenarios

### Add Required Status Check

```
Update ruleset: Main Branch Protection

Change type: MODIFY_EXISTING

Proposed changes:
- [x] Add required status check: security-scan

Rationale:
All PRs must pass security scanning before merge

Impact assessment:
- Affected repositories: all repos
- Breaking change: YES - PRs without security-scan will be blocked
- Affects existing PRs: YES
- Team notifications needed: YES - all teams

Rollout plan:
1. Add security-scan workflow to all repos (via repo-template update)
2. Wait 1 week for teams to adopt
3. Update ruleset to require security-scan
4. Monitor for issues, provide support

Success criteria:
- [x] All repos have security-scan workflow
- [ ] Ruleset updated
- [ ] No blocked PRs (or resolved quickly)
```

### Enforce CODEOWNERS Review

```
Update ruleset: CODEOWNERS Enforcement

Change type: MODIFY_EXISTING

Proposed changes:
- [x] Require CODEOWNERS review for protected files
- [x] Dismiss stale reviews on new commits

Rationale:
Ensure domain experts review changes to critical paths

Impact assessment:
- Affected repositories: all repos with CODEOWNERS
- Breaking change: YES - PRs may need additional reviews
- Affects existing PRs: YES
- Team notifications needed: YES

Rollout plan:
1. Audit all CODEOWNERS files for accuracy
2. Communicate change to teams
3. Enable ruleset
4. Monitor first week for issues

Success criteria:
- [ ] CODEOWNERS files reviewed
- [ ] Ruleset enabled
- [ ] Teams understand new process
```

## Defense in Depth

Rulesets are one layer. Use multiple controls:

1. **Rulesets**: Hard enforcement at GitHub level
2. **CODEOWNERS**: Review requirements by path
3. **Workflows**: Automated checks (policy-check, CI)
4. **Branch Protection**: Legacy settings (if not migrated to rulesets)

## Coverage Matrix Update

After ruleset changes, update coverage matrix:

| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| PR required | Org ruleset | Main branch protection | main | Platform |
| Required checks | Org ruleset | policy-check, ci | main | Platform |
| CODEOWNERS review | Org ruleset | Branch protection | protected paths | Platform |

## Validation

Before merging:

1. Test on a non-production repo
2. Verify expected behavior
3. Check bypass permissions work
4. Confirm no unintended blocks

## Rollback

If issues arise:

1. Set ruleset enforcement to `evaluate` (report only)
2. Investigate and fix issues
3. Re-enable `active` enforcement

## Related

- [Governance Agent](../agents/governance.agent.md)
- [Coverage Matrix](https://github.com/ORG_NAME/dev-workflow-os/tree/main/docs/governance/coverage-matrix.md)
- [Ruleset Standards](https://github.com/ORG_NAME/dev-workflow-os/tree/main/policy/rulesets)
