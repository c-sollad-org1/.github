# GitHub Projects v2 Field Configuration

This document defines the standard field set for GitHub Projects v2 across the ORG_NAME organization.

## Overview

All organization projects should use this consistent field set for:
- Standardized tracking across teams
- Consistent reporting and metrics
- Simplified automation
- Cross-team visibility

## Field Definitions

### Status (Single Select) - REQUIRED

Tracks the current state of work.

**Values**:
- **Triage** - Newly created, needs review and prioritization
- **Todo** - Accepted and prioritized, ready to be worked on
- **In Progress** - Active development underway
- **In Review** - Pull request opened, under review
- **Blocked** - Work paused due to dependencies or issues
- **Done** - Complete and merged/closed

**Color Scheme**:
- Triage: Gray
- Todo: Yellow
- In Progress: Blue
- In Review: Purple
- Blocked: Red
- Done: Green

**Transitions**:
```
Triage → Todo (after prioritization)
Triage → Done (if rejected/duplicate)
Todo → In Progress (work starts)
In Progress → In Review (PR opened)
In Progress → Blocked (dependency/issue)
Blocked → In Progress (unblocked)
In Review → In Progress (changes requested)
In Review → Done (PR merged)
```

### Priority (Single Select) - REQUIRED

Indicates urgency and importance.

**Values**:
- **P0** - Critical: Immediate attention required (outages, security, blocking)
- **P1** - High: Should be completed this sprint/cycle
- **P2** - Medium: Should be completed next sprint/cycle
- **P3** - Low: Backlog, no immediate timeline

**Guidelines**:
- P0: Drop everything, all hands if needed
- P1: Top of current sprint
- P2: Plan for next sprint
- P3: Nice to have, prioritize when capacity allows

### Area (Single Select) - REQUIRED

Categorizes work by domain or functional area.

**Values**:
- **governance** - Policies, standards, compliance
- **ci** - Build, test, deployment automation
- **docs** - Documentation and diagrams
- **devex** - Developer experience and tooling
- **security** - Security, vulnerability management
- **release** - Release management and coordination

**Usage**: Tag issues/PRs with the most relevant area. If multiple areas apply, choose the primary one.

### Owner Team (Text) - RECOMMENDED

Identifies which team is responsible.

**Format**: `@org/team-name`

**Examples**:
- @org/platform-team
- @org/backend-team
- @org/frontend-team
- @org/security-team

**Guidelines**:
- Assign to team, not individual (teams own work)
- Use GitHub team mentions for consistency
- One owner team per item

### Target Date (Date) - OPTIONAL

When this should be completed.

**Usage**:
- Set for P0/P1 items
- Optional for P2/P3
- Can be adjusted as needed
- Used for planning and timeline tracking

### Start Date (Date) - OPTIONAL

When work actually started.

**Usage**:
- Set automatically when Status → In Progress
- Or manually set when work begins
- Helps track cycle time

### Effort (Single Select) - OPTIONAL

Estimated size/complexity of work.

**Values**:
- **XS** - Extra Small: < 2 hours (quick fix, minor tweak)
- **S** - Small: 2-4 hours (single file change, small feature)
- **M** - Medium: 1-2 days (moderate feature, several files)
- **L** - Large: 3-5 days (significant feature, architecture change)
- **XL** - Extra Large: 1+ weeks (major initiative, should be broken down)

**Guidelines**:
- Estimate conservatively
- XL items should be broken into smaller tasks
- Re-estimate if scope changes significantly

## Built-in Automations

GitHub Projects v2 includes built-in automations that should be configured:

### 1. Set Status to Todo when added
**Trigger**: Item added to project
**Action**: Set Status = Todo

**Configuration**:
```
When: Item added to project
Then: Set Status to "Todo"
```

### 2. Set Status to Done when closed
**Trigger**: Issue or PR closed
**Action**: Set Status = Done

**Configuration**:
```
When: Item closed
Then: Set Status to "Done"
```

### 3. Close item when moved to Done
**Trigger**: Status changed to Done
**Action**: Close issue or PR

**Configuration**:
```
When: Status changed to "Done"
Then: Close item
```

### 4. Set Start Date when In Progress
**Trigger**: Status changed to In Progress
**Action**: Set Start Date = today

**Configuration**:
```
When: Status changed to "In Progress"
Then: Set Start Date to "current date"
```

## Views

### Default Board View

**Columns**: Group by Status
- Triage
- Todo
- In Progress
- In Review
- Blocked
- Done

**Sort**: Priority (P0 first), then Target Date

**Filters**: None (show all)

### Priority View

**Columns**: Group by Priority
- P0
- P1
- P2
- P3

**Sort**: Status (In Progress first), then Target Date

**Filters**: Status != Done (hide completed items)

### Team View

**Columns**: Group by Owner Team

**Sort**: Priority, then Status

**Filters**: Status != Done

### Area View

**Columns**: Group by Area

**Sort**: Priority, then Status

**Filters**: Status != Done

### Sprint View

**Table Layout**: Show all fields

**Filters**: 
- Status = Todo, In Progress, In Review, or Blocked
- Priority = P0 or P1

**Sort**: Priority, then Target Date

## Creating a New Project

### Setup Steps

1. **Create project**:
   ```bash
   gh project create --owner ORG_NAME --title "Project Name"
   ```

2. **Add fields** (via UI):
   - Status (single select): Add values as listed above
   - Priority (single select): P0, P1, P2, P3
   - Area (single select): governance, ci, docs, devex, security, release
   - Owner Team (text)
   - Target Date (date)
   - Start Date (date)
   - Effort (single select): XS, S, M, L, XL

3. **Configure automations** (via UI):
   - Set up the 4 built-in automations listed above

4. **Create views**:
   - Default Board (group by Status)
   - Priority View (group by Priority)
   - Team View (group by Owner Team)
   - Area View (group by Area)
   - Sprint View (table, filtered)

5. **Set permissions**:
   - Admin: Platform Team
   - Write: All teams
   - Read: Organization members

### Automation via Workflows

The `add-to-project.yml` workflow automatically adds new issues and PRs to the project:

```yaml
- name: Add to project
  uses: actions/add-to-project@v0.5.0
  with:
    project-url: ${{ secrets.ORG_PROJECT_URL }}
    github-token: ${{ secrets.ADD_TO_PROJECT_PAT }}
```

**Required secrets**:
- `ORG_PROJECT_URL`: Full URL to the project
- `ADD_TO_PROJECT_PAT`: Personal Access Token with project write access

## Reporting and Metrics

### Velocity Metrics

Track team velocity using:
- **Throughput**: Items completed per week/sprint
- **Cycle time**: Start Date → Done
- **Lead time**: Created → Done

### Priority Distribution

Monitor P0/P1 ratio:
- Target: < 20% P0/P1
- Too many P0s: Indicates poor planning or constant firefighting
- Too few P0s: May indicate under-urgency

### Blocked Items

Monitor blocked items:
- Review weekly
- Unblock or re-prioritize
- Document blockers and resolutions

### Area Distribution

Track work by area:
- Ensure balance across areas
- Identify neglected areas
- Plan capacity accordingly

## Best Practices

### For Platform Team

1. **Consistency**: Use the same field set across projects
2. **Automation**: Enable all built-in automations
3. **Training**: Onboard teams on field definitions
4. **Monitoring**: Review project health weekly

### For Team Members

1. **Keep updated**: Move items through Status as work progresses
2. **Prioritize ruthlessly**: Not everything can be P0 or P1
3. **Unblock**: Actively work to unblock Blocked items
4. **Break down**: Split XL items into smaller tasks
5. **Close when done**: Don't leave items in Done forever

### Common Mistakes

- ❌ Everything marked P0/P1
- ❌ Items stuck in In Progress for weeks
- ❌ No Target Date on P0/P1 items
- ❌ Blocked items with no context in comments
- ❌ Status not updated when PR opened

## Related Documentation

- [Issue Lifecycle Diagram](../diagrams/issue-lifecycle.mmd)
- [Automation Map](../diagrams/automation-map.mmd)
- [add-to-project workflow](../../templates/repo-template/.github/workflows/add-to-project.yml)

## Questions?

For questions about project configuration:
- Open an issue with "devex" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
