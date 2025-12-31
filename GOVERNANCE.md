---
title: "Governance"
created: 2025-12-16
status: active
author: Platform Team
---

## Governance Model

This document outlines how decisions are made across **ORG_NAME** repositories.

### Roles

- **Platform Team** (@org/platform-team): Owns governance, tooling, and the "Dev Workflow OS" control plane.
- **Repository Owners**: Teams or individuals with admin rights to a specific repo. Responsible for code quality, issue triage, and enforcing repo-specific policies.
- **Contributors**: Anyone submitting PRs, issues, or participating in discussions.

### Decision-making

- **Repo-level decisions**: Repository Owners have final say on technical direction, architecture, and merges.
- **Organization-level decisions** (rulesets, org defaults, shared tooling): Platform Team leads, with input from Repository Owners.
- **Governance changes**: Use the "Governance Change" issue template. Platform Team reviews and approves.

### Change process

1. Open an issue using the appropriate template.
2. Discuss in the issue thread.
3. For governance changes, Platform Team approves before implementation.
4. For repo-level changes, Repository Owners approve.

### Consensus

- Aim for consensus through discussion.
- If consensus cannot be reached, Platform Team (for org-level) or Repository Owners (for repo-level) make the final call.

### Escalation

If you disagree with a decision:

1. Open a discussion in the relevant issue or PR.
2. Tag @org/platform-team for org-level disputes.
3. For unresolved conflicts, escalate to the organization leadership.

### Transparency

- All decisions are made in public issues or PRs (unless security-sensitive).
- Governance changes are tracked in the **dev-workflow-os** repository.

### Contact

For questions about governance:

- Open an issue in the **dev-workflow-os** repository
- Tag @org/platform-team
