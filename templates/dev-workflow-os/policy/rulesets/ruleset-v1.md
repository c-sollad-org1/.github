# Ruleset v1 Standards

This document defines the baseline organization-level rulesets for ORG_NAME repositories.

## Overview

**Rulesets** are GitHub's mechanism for enforcing policies at the organization or repository level. Rulesets provide:
- Hard enforcement (cannot be bypassed without permission)
- Centralized management (org-level rulesets apply to all repos)
- Audit trail (all bypass attempts are logged)
- Granular control (target specific branches, tags, or repos)

## Ruleset Philosophy

1. **Protect main**: Main branch is the source of truth, must be stable
2. **Require review**: All changes go through pull requests
3. **Automate checks**: Required workflows validate before merge
4. **Defense in depth**: Layer multiple controls
5. **Escape hatch**: Platform Team can bypass in emergencies (logged)

## Baseline Ruleset (Main Branch Protection)

This ruleset applies to the `main` branch across all repositories.

### Configuration

**Name**: `Main Branch Protection`

**Target**: 
- Branch pattern: `refs/heads/main`
- Repository scope: All repositories (or targeted list)

**Enforcement**: `Active` (blocking)

### Rules

#### 1. Require Pull Request

**Rule**: `pull_request`

**Settings**:
- Required: Yes
- Dismiss stale reviews: Yes (when new commits pushed)
- Require review from Code Owners: Yes
- Required approving review count: 1

**Rationale**: 
- All changes go through PR review
- Prevents direct pushes to main
- Ensures code review happens

#### 2. Require Status Checks

**Rule**: `required_status_checks`

**Settings**:
- Required checks:
  - `policy-check` (from policy-check.yml workflow)
  - `ci` (from ci.yml workflow, may vary by repo)
- Require branches to be up to date: No (allows parallel work)

**Rationale**:
- Automated validation before merge
- policy-check ensures governance compliance
- ci ensures tests pass

**Note**: Individual repos may add additional required checks (e.g., `security-scan`, `integration-tests`). This is encouraged via branch protection at repo level.

#### 3. Block Force Pushes

**Rule**: `non_fast_forward`

**Settings**:
- Block force pushes: Yes

**Rationale**:
- Prevents history rewriting
- Protects against accidental overwrites
- Maintains audit trail

#### 4. Block Deletions

**Rule**: `deletion`

**Settings**:
- Block branch deletion: Yes

**Rationale**:
- Prevents accidental main branch deletion
- Protects critical branches

#### 5. Require Linear History

**Rule**: `required_linear_history`

**Settings**:
- Require linear history: Yes

**Rationale**:
- Cleaner git history
- Easier to trace changes
- Encourages squash or rebase merges

**Note**: This can be relaxed for repos that prefer merge commits. Override at repo level if needed.

#### 6. Require Signed Commits (Optional)

**Rule**: `required_signatures`

**Settings**:
- Require signed commits: No (optional, enable per repo)

**Rationale**:
- Enhanced security and identity verification
- Optional because not all teams have GPG keys set up

**Recommendation**: Enable for repos handling sensitive data or requiring high assurance.

### Bypass Permissions

**Who can bypass**:
- Platform Team: Yes (for emergency fixes, infrastructure changes)
- Repository Admins: No (must follow process)
- Bots/Apps: Specific apps only (e.g., Dependabot for automated updates)

**Bypass process**:
1. Must be documented (reason, who, when)
2. Logged in GitHub audit log
3. Reviewed in quarterly audits
4. Alternative: Use emergency branch, then PR to main

**Legitimate bypass reasons**:
- Critical security fix needed immediately
- Infrastructure/platform changes affecting workflows
- Fixing broken CI that blocks all PRs

**Not legitimate**:
- "I'm in a hurry"
- "It's just a small change"
- "I'll fix it later"

## Additional Rulesets

### Development Branch Protection

**Name**: `Development Branch Protection`

**Target**: `refs/heads/dev`, `refs/heads/develop`, `refs/heads/staging`

**Rules** (lighter than main):
- Require pull request: Yes
- Required reviews: 0 (PRs required but auto-merge allowed)
- Block force push: No (allow rebase/squash)
- Block deletion: No

**Rationale**: Balance between protection and flexibility for dev branches.

### Release Branch Protection

**Name**: `Release Branch Protection`

**Target**: `refs/heads/release/*`

**Rules**:
- Require pull request: Yes
- Required reviews: 2 (higher bar for releases)
- Require status checks: Yes (all checks must pass)
- Block force push: Yes
- Block deletion: Yes

**Rationale**: Release branches are sensitive, require extra scrutiny.

### Tag Protection

**Name**: `Tag Protection`

**Target**: `refs/tags/*`

**Rules**:
- Creation: Allowed (tags can be created)
- Update: Blocked (tags are immutable once created)
- Deletion: Blocked (tags are permanent)

**Rationale**: Tags mark releases, should never change or disappear.

## Repository-Specific Overrides

Individual repositories can add **additional** protections but cannot weaken org-level rulesets.

**Allowed**:
- Add more required status checks
- Increase required review count
- Add additional protected branches
- Enable commit signing

**Not Allowed**:
- Remove required checks
- Bypass PR requirement
- Allow force push on main
- Disable CODEOWNERS review

To request an exception to org-level rulesets:
1. Open "Governance Change" issue
2. Provide strong justification
3. Get Platform Team approval
4. Document in repo's governance docs

## Implementing Rulesets

### Via GitHub UI

1. Go to Organization Settings → Rulesets
2. Click "New ruleset"
3. Configure as documented above
4. Set enforcement to "Active"
5. Save

### Via GitHub API

```bash
# Create ruleset (using JSON for complex nested structures is recommended)
cat > ruleset.json << 'EOF'
{
  "name": "Main Branch Protection",
  "target": "branch",
  "enforcement": "active",
  "conditions": {
    "ref_name": {
      "include": ["refs/heads/main"],
      "exclude": []
    }
  },
  "rules": [
    {
      "type": "pull_request",
      "parameters": {
        "dismiss_stale_reviews_on_push": true,
        "require_code_owner_review": true,
        "required_approving_review_count": 1
      }
    },
    {
      "type": "required_status_checks",
      "parameters": {
        "required_status_checks": [
          {"context": "policy-check"},
          {"context": "ci"}
        ]
      }
    },
    {"type": "non_fast_forward"},
    {"type": "deletion"},
    {"type": "required_linear_history"}
  ]
}
EOF

gh api /orgs/ORG_NAME/rulesets \
  --method POST \
  --input ruleset.json
```

### Via Terraform (Infrastructure as Code)

```hcl
resource "github_organization_ruleset" "main_protection" {
  name        = "Main Branch Protection"
  target      = "branch"
  enforcement = "active"

  conditions {
    ref_name {
      include = ["refs/heads/main"]
      exclude = []
    }
  }

  rules {
    pull_request {
      dismiss_stale_reviews_on_push     = true
      require_code_owner_review         = true
      required_approving_review_count   = 1
    }

    required_status_checks {
      required_check {
        context = "policy-check"
      }
      required_check {
        context = "ci"
      }
    }

    non_fast_forward = true
    deletion        = true
    required_linear_history = true
  }

  bypass_actors {
    actor_id    = data.github_team.platform.id
    actor_type  = "Team"
    bypass_mode = "always"
  }
}
```

## Monitoring and Auditing

### Check Ruleset Status

```bash
# List all rulesets
gh api /orgs/ORG_NAME/rulesets

# Get specific ruleset
gh api /orgs/ORG_NAME/rulesets/[RULESET_ID]

# Check which rulesets apply to a repo
gh api /repos/ORG_NAME/REPO_NAME/rulesets
```

### Audit Bypass Events

Ruleset bypasses are logged in the GitHub audit log:

```bash
# Via GitHub UI: Settings → Audit log → Filter by action
# Search for: action:branch_protection.bypass

# Via API
gh api /orgs/ORG_NAME/audit-log \
  --jq '.[] | select(.action == "branch_protection.bypass")'
```

Review bypass events quarterly:
- Was bypass justified?
- Could it have been avoided?
- Do we need to adjust process?

### Compliance Checks

Repository compliance with rulesets:

```bash
# Check if repo has expected protection
gh api /repos/ORG_NAME/REPO_NAME/branches/main/protection

# List repos missing required checks
# (custom script in scripts/gh/audit-rulesets.sh)
```

## Troubleshooting

### PR Blocked by Ruleset

**Symptom**: Cannot merge PR, "Required status checks have not passed"

**Resolution**:
1. Check which check is failing (GitHub UI shows details)
2. Fix the issue in the PR
3. Re-run failed checks if transient failure
4. If check is incorrect, update workflow (separate PR)

### Cannot Push to Branch

**Symptom**: `error: failed to push some refs`, `refusing to allow a user to push`

**Resolution**:
1. Are you trying to push to main directly? Open a PR instead
2. Is force push blocked? Use regular push or open new PR
3. Contact Platform Team if legitimate need to bypass

### Check Not Running

**Symptom**: Required check not starting, PR cannot merge

**Resolution**:
1. Check if workflow file exists (`.github/workflows/policy-check.yml`)
2. Check workflow syntax (YAML errors)
3. Check workflow triggers (should include `pull_request`)
4. Re-run workflow manually if stuck

### Need to Bypass Ruleset

**Symptom**: Emergency fix needed, cannot wait for PR process

**Process**:
1. Document reason (open incident issue)
2. Contact Platform Team for approval
3. Platform Team member bypasses ruleset
4. Make the fix
5. Follow up with proper PR afterward
6. Document in incident post-mortem

## Migration from Branch Protection

If migrating from legacy branch protection rules:

1. **Audit existing rules**: Document current branch protection settings
2. **Create equivalent rulesets**: Map settings to ruleset rules
3. **Test on pilot repos**: Validate rulesets work as expected
4. **Communicate**: Notify teams of upcoming change
5. **Enable rulesets**: Activate org-level rulesets
6. **Remove old rules**: Delete legacy branch protection (optional)
7. **Monitor**: Watch for issues in first week

## Related Documentation

- [Coverage Matrix](../../docs/governance/coverage-matrix.md)
- [Defense in Depth Diagram](../../docs/diagrams/defense-in-depth.mmd)
- [Governance Model](../../docs/governance/README.md)
- [Ruleset Update Prompt](../../templates/repo-template/.github/prompts/ruleset-update.prompt.md)

## Questions?

For questions about rulesets:
- Open an issue with "governance" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
