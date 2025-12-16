# Runbooks

This directory contains operational runbooks for this repository.

## What is a Runbook?

A runbook is a step-by-step guide for operational tasks:
- Deployment procedures
- Incident response
- Troubleshooting guides
- Maintenance tasks
- Recovery procedures

## Runbook Index

<!-- Add links to specific runbooks as you create them -->

### Deployment

- [Deployment Guide](deployment.md) - How to deploy this application
- [Rollback Procedure](rollback.md) - How to rollback a bad deployment

### Operations

- [Health Checks](health-checks.md) - Monitoring and health check procedures
- [Scaling Guide](scaling.md) - When and how to scale resources

### Incident Response

- [Incident Response](incident-response.md) - How to respond to incidents
- [Common Issues](troubleshooting.md) - Known issues and solutions

### Maintenance

- [Dependency Updates](dependency-updates.md) - How to update dependencies
- [Database Migrations](migrations.md) - Running and reverting migrations

## Runbook Template

Each runbook should follow this structure:

```markdown
# Runbook: Task Name

## Purpose

What does this accomplish?

## Prerequisites

- Access needed
- Tools required
- Context/timing

## Procedure

1. Step one with command:
   ```bash
   command here
   ```
   Expected output: ...

2. Step two...

## Verification

How to confirm success?

## Rollback

If something goes wrong...

## Troubleshooting

Common issues and fixes.

## Related

- [Other runbook](...)
- [Architecture doc](...)
```

## Creating a New Runbook

1. Copy the template above
2. Fill in all sections
3. Test the procedure
4. Add to this index
5. Link from related documentation

## Best Practices

1. **Be specific**: Exact commands, not "run the script"
2. **Show expected output**: Help readers confirm they're on track
3. **Include verification**: How to check if it worked
4. **Provide rollback**: How to undo if needed
5. **Keep updated**: Review quarterly or after incidents

## Using Runbooks

### During Incidents

1. Stay calm, follow the procedure
2. Update the incident issue with progress
3. Note any deviations from the runbook
4. After resolution, update the runbook if needed

### For Planned Tasks

1. Read the entire runbook first
2. Ensure prerequisites are met
3. Follow steps in order
4. Verify after completion
5. Report any issues or improvements

## Common Commands

### Repository Operations

```bash
# Check repository status
git --no-pager status

# View recent changes
git --no-pager log --oneline -10

# Create a new branch
git checkout -b feature/my-feature
```

### GitHub CLI

```bash
# View open PRs
gh pr list

# View recent workflow runs
gh run list --limit 10

# Trigger a workflow
gh workflow run ci.yml
```

### Testing

```bash
# Run tests locally
# npm test
# pytest
# go test ./...

# Run linting
# npm run lint
# black --check .
# golangci-lint run
```

## On-Call Information

For on-call responsibilities:
- See [On-Call Guide](on-call.md)
- Escalation path: [team] → [lead] → [manager]
- Incident severity definitions: [Incident Template](https://github.com/ORG_NAME/.github/blob/main/.github/ISSUE_TEMPLATE/incident.yml)

## Related Documentation

- [Architecture](../architecture/README.md)
- [Governance](../governance/README.md)
- [Incident Triage Prompt](../../.github/prompts/incident-triage.prompt.md)

## Questions?

For operational questions:
- Open an issue with the "ops" or "runbook" label
- During incidents: Tag @org/[team-name] in the incident issue
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
