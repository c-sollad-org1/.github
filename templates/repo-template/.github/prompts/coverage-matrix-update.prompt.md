# Prompt: Coverage Matrix Update

## Purpose

Update the governance coverage matrix to document how controls are enforced across the organization. Use this when adding new controls or modifying enforcement mechanisms.

## Context

The coverage matrix is the **source of truth** for governance controls. It documents:
- What control exists
- How it's enforced
- What implements it
- Where it applies
- Who owns it

Located at: `docs/governance/coverage-matrix.md`

## When to Use

- Adding a new security control
- Changing enforcement mechanism
- Documenting existing controls
- Auditing governance coverage
- Responding to compliance requirements

## Prompt Template

```
Update coverage matrix: [CONTROL_NAME]

Action: [ADD | MODIFY | REMOVE]

Control details:
- Name: [Short name of control]
- Description: [What does this control do?]
- Enforcement: [Ruleset | CODEOWNERS | Workflow | Manual]
- Artifact: [What implements this? e.g., "policy-check.yml"]
- Scope: [Where does this apply? e.g., "main branch", "all repos"]
- Owner: [Which team owns this? e.g., "Platform Team"]

Rationale:
[Why is this control needed? What risk does it mitigate?]

Related changes:
- [ ] Ruleset: [NAME] (if applicable)
- [ ] Workflow: [FILE] (if applicable)
- [ ] CODEOWNERS: [PATHS] (if applicable)
- [ ] Documentation: [LOCATION]

Verification:
- [ ] Control is enforced
- [ ] Matrix entry is accurate
- [ ] Related artifacts are updated
```

## Coverage Matrix Format

```markdown
| Control | Enforcement | Artifact | Scope | Owner |
|---------|-------------|----------|-------|-------|
| PR required | Ruleset | Main branch protection | main | Platform |
| Required checks | Ruleset | policy-check, ci | main | Platform |
| CODEOWNERS review | Ruleset | Branch protection | protected paths | Platform |
| No secrets in code | Workflow | policy-check.yml | all branches | Platform |
| Dependency review | Workflow | dependency-review.yml | PRs | Platform |
| Code quality | Workflow | ci.yml (lint, test) | all branches | Repo Owners |
| Security scanning | Workflow | codeql-analysis.yml | main, PRs | Platform |
| Breaking changes | Manual | Semantic versioning | releases | Repo Owners |
| API changes | Manual | Changelog, migration guide | releases | Repo Owners |
```

## Fields Explained

### Control

Short name of the control. What are we protecting or enforcing?

Examples:
- "PR required"
- "CODEOWNERS review"
- "No secrets in code"
- "Security scanning"

### Enforcement

How is this control enforced?

- **Ruleset**: GitHub org/repo ruleset (hard enforcement)
- **CODEOWNERS**: GitHub CODEOWNERS file (review required)
- **Workflow**: GitHub Actions workflow (automated check)
- **Manual**: Human review or process (soft enforcement)
- **Combination**: Multiple mechanisms (list them)

### Artifact

What specific artifact implements this control?

Examples:
- "Main branch protection ruleset"
- "policy-check.yml workflow"
- "CODEOWNERS file"
- "Team review process"
- "Release checklist"

### Scope

Where does this control apply?

Examples:
- "main branch"
- "all protected branches"
- "all repositories"
- "public repositories only"
- "paths: .github/, docs/"

### Owner

Which team is responsible for maintaining this control?

Examples:
- "Platform Team" (org-level controls)
- "Repo Owners" (repo-specific controls)
- "Security Team" (security controls)
- "Specific team name"

## Example Updates

### Adding a New Control

```
Update coverage matrix: Terraform Plan Required

Action: ADD

Control details:
- Name: Terraform plan required
- Description: All infrastructure changes must show plan before apply
- Enforcement: Workflow
- Artifact: terraform-plan.yml
- Scope: PRs to /terraform directory
- Owner: Platform Team

Rationale:
Prevent accidental infrastructure changes. Show impact before applying.

Related changes:
- [x] Workflow: .github/workflows/terraform-plan.yml
- [x] CODEOWNERS: /terraform @org/platform-team
- [ ] Documentation: docs/runbooks/terraform.md

Verification:
- [ ] Workflow runs on PR to /terraform
- [ ] Matrix entry added
- [ ] Runbook updated
```

Matrix entry:

```markdown
| Terraform plan required | Workflow | terraform-plan.yml | /terraform | Platform |
```

### Modifying Existing Control

```
Update coverage matrix: Required checks

Action: MODIFY

Control details:
- Name: Required checks
- Change: Add "security-scan" to required checks list
- Enforcement: Ruleset (unchanged)
- Artifact: Main branch protection (updated)
- Scope: main (unchanged)
- Owner: Platform (unchanged)

Rationale:
All PRs must pass security scanning before merge.

Related changes:
- [x] Ruleset: Updated to include security-scan
- [x] Workflow: security-scan.yml exists in all repos
- [ ] Documentation: Updated org standards

Verification:
- [x] Ruleset updated
- [ ] Matrix entry reflects new check
```

Updated matrix entry:

```markdown
| Required checks | Ruleset | policy-check, ci, security-scan | main | Platform |
```

### Removing a Control

```
Update coverage matrix: Deprecated check

Action: REMOVE

Control details:
- Name: Legacy lint check
- Reason: Replaced by integrated linter in ci.yml

Related changes:
- [x] Workflow: legacy-lint.yml removed
- [x] Ruleset: legacy-lint removed from required checks
- [x] Documentation: Updated to reference ci.yml

Verification:
- [x] Control no longer enforced
- [ ] Matrix entry removed
- [ ] No references to old workflow
```

## Coverage Analysis

Use the matrix to:

1. **Identify gaps**: What's missing?
2. **Audit enforcement**: Are controls actually working?
3. **Review ownership**: Is each control owned?
4. **Assess redundancy**: Multiple controls for same risk?
5. **Compliance mapping**: Map to regulatory requirements

## Integration with Other Artifacts

The coverage matrix should align with:

- **Rulesets**: Documented in policy/rulesets/
- **Workflows**: In .github/workflows/
- **CODEOWNERS**: Document review requirements
- **Governance docs**: docs/governance/

## Best Practices

1. **Keep it current**: Update matrix when controls change
2. **Be specific**: List actual artifact names
3. **One control per row**: Don't combine unrelated controls
4. **Consistent naming**: Use standard terminology
5. **Verify periodically**: Audit matrix vs. actual implementation

## Related

- [Governance Agent](../agents/governance.agent.md)
- [Ruleset Update Prompt](ruleset-update.prompt.md)
- [Coverage Matrix](https://github.com/ORG_NAME/dev-workflow-os/tree/main/docs/governance/coverage-matrix.md)
- [Policy Documentation](https://github.com/ORG_NAME/dev-workflow-os/tree/main/policy)
