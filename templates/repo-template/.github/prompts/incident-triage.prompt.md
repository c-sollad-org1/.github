# Prompt: Incident Triage

## Purpose

Guide initial triage and response for production incidents. Use this when an incident is reported to quickly assess and respond.

## Context

Incidents require immediate attention and coordination. This prompt helps:
- Assess severity
- Gather initial information
- Coordinate response
- Track resolution

## When to Use

- Production outage or degradation
- Security incident
- Data loss or corruption
- Critical bug in production
- Service disruption

## Prompt Template

```
Incident: [SHORT_DESCRIPTION]

Initial report:
- Reporter: [WHO]
- Detected at: [TIMESTAMP UTC]
- Incident started: [TIMESTAMP UTC or "unknown"]
- Severity: [SEV1/SEV2/SEV3/SEV4 - see below]

Symptoms:
- [What users are experiencing]
- [Error messages or metrics]
- [Affected services/components]

Impact:
- Users affected: [% or count or "unknown"]
- Services affected: [LIST]
- Geographic scope: [global/regional/specific region]
- Business impact: [revenue loss/SLA breach/reputation/other]

Triage steps:
1. [ ] Confirm severity level
2. [ ] Identify incident commander
3. [ ] Create war room / coordination channel
4. [ ] Notify stakeholders
5. [ ] Gather logs and metrics
6. [ ] Form initial hypothesis
7. [ ] Identify mitigation options
8. [ ] Execute mitigation
9. [ ] Verify mitigation
10. [ ] Monitor for resolution

Status updates:
- [TIMESTAMP]: [Status update]
- [TIMESTAMP]: [Status update]

Resolution:
- Resolved at: [TIMESTAMP UTC]
- Root cause: [Brief description]
- Mitigation: [What was done]
- Follow-up: [Post-incident review, preventive measures]
```

## Severity Levels

### SEV1 - Critical

- **Definition**: Full outage, data loss, security breach
- **Impact**: Majority of users affected, critical functionality unavailable
- **Response time**: Immediate (< 15 minutes)
- **Escalation**: All hands, incident commander, exec notification
- **Examples**:
  - Service completely down
  - Database corruption
  - Security breach with data exposure
  - Payment processing failure

### SEV2 - High

- **Definition**: Major feature unavailable, significant degradation
- **Impact**: Substantial user impact, workaround may exist
- **Response time**: < 1 hour
- **Escalation**: On-call team, incident commander, stakeholder notification
- **Examples**:
  - API returning 50% errors
  - Login failures affecting some users
  - Critical background job failing

### SEV3 - Medium

- **Definition**: Minor feature issue, performance degradation
- **Impact**: Limited user impact, workaround available
- **Response time**: < 4 hours during business hours
- **Escalation**: On-call team
- **Examples**:
  - Non-critical feature broken
  - Slow response times
  - Intermittent errors

### SEV4 - Low

- **Definition**: Minor issue, minimal impact
- **Impact**: Few users affected, easy workaround
- **Response time**: Next business day
- **Escalation**: Regular issue tracking
- **Examples**:
  - UI glitch
  - Non-critical metric missing
  - Minor documentation error

## Triage Checklist

### Immediate (0-15 minutes)

- [ ] Confirm incident is real (not false alarm)
- [ ] Assess severity using criteria above
- [ ] Identify incident commander (IC)
- [ ] Create coordination channel (#incident-YYYY-MM-DD)
- [ ] Page on-call team
- [ ] Update status page (if applicable)

### Short-term (15-60 minutes)

- [ ] Gather diagnostic information:
  - Logs from affected services
  - Metrics and dashboards
  - Recent changes (deployments, config changes)
  - Error rates and patterns
- [ ] Form initial hypotheses
- [ ] Identify mitigation options:
  - Rollback deployment
  - Disable feature flag
  - Scale resources
  - Failover to backup
- [ ] Execute mitigation
- [ ] Post updates to incident channel

### Resolution

- [ ] Verify mitigation worked
- [ ] Monitor for stability
- [ ] Communicate resolution to stakeholders
- [ ] Update status page
- [ ] Thank responders
- [ ] Schedule post-incident review

### Follow-up

- [ ] Conduct post-incident review (within 1 week)
- [ ] Document timeline and root cause
- [ ] Identify preventive measures
- [ ] Create issues for follow-up work
- [ ] Update runbooks
- [ ] Share learnings with team

## Investigation Questions

### What changed?

- Deployments in last 24 hours?
- Configuration changes?
- Infrastructure changes?
- Dependency updates?
- Traffic patterns?

### What do the logs say?

- Error messages?
- Stack traces?
- Correlation IDs?
- Timing patterns?

### What do the metrics show?

- Error rates?
- Latency (p50, p95, p99)?
- Resource utilization (CPU, memory, disk)?
- Request volume?
- Database performance?

### What's the blast radius?

- All users or subset?
- All regions or specific ones?
- All features or specific ones?
- Internal systems affected?

## Mitigation Options

### Rollback

Revert to previous known-good version.

**When**: Recent deployment likely caused issue
**How**: Deploy previous version tag
**Pros**: Quick, low risk
**Cons**: Loses new features, may have data migrations

### Disable Feature

Turn off problematic feature via feature flag.

**When**: New feature causing issues
**How**: Set feature flag to false
**Pros**: Very quick, preserves rest of service
**Cons**: Feature unavailable to users

### Scale Resources

Increase capacity to handle load.

**When**: Resource exhaustion (CPU, memory, connections)
**How**: Increase instance count or size
**Pros**: Addresses capacity issues
**Cons**: Higher cost, may not fix root cause

### Failover

Switch to backup system or region.

**When**: Primary system is down
**How**: DNS/load balancer change
**Pros**: Restores service quickly
**Cons**: Backup may be stale, complex

### Hot Fix

Deploy targeted fix for the issue.

**When**: Root cause known and fix is simple
**How**: Deploy minimal patch
**Pros**: Fixes root cause
**Cons**: Risky during incident, requires testing

## Communication Templates

### Initial Notification

```
🚨 Incident Alert - SEV[N]: [Brief description]

Impact: [Who/what is affected]
Started: [Time]
Status: Investigating

We are working on this with priority. Updates every [15/30] minutes.
```

### Status Update

```
📊 Incident Update - SEV[N]: [Description]

Current status: [Investigating/Mitigating/Monitoring/Resolved]

What we know:
- [Finding 1]
- [Finding 2]

Next steps:
- [Action 1]
- [Action 2]

Next update: [Time]
```

### Resolution

```
✅ Incident Resolved - SEV[N]: [Description]

Resolved at: [Time]
Duration: [Total time]

Root cause: [Brief explanation]

Mitigation: [What we did]

Follow-up:
- Post-incident review scheduled for [Date]
- Preventive work tracked in issue #[NUM]

Thank you to the response team!
```

## Related

- [Incident runbook](../../docs/runbooks/incident-response.md)
- [On-call guide](../../docs/runbooks/on-call.md)
- [Monitoring dashboards](link-to-dashboards)
- [Status page](link-to-status-page)
