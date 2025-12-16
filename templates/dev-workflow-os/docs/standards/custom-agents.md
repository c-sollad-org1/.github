# Custom Agent Roster

This document defines the custom Copilot agents available across ORG_NAME repositories.

## Overview

Custom agents are specialized Copilot profiles with domain expertise. They provide:
- **Domain knowledge**: Expert in specific areas (governance, CI, security, etc.)
- **Consistent guidance**: Standardized recommendations aligned with org standards
- **Automation assistance**: Help implement complex tasks
- **Context-aware**: Understand org-specific patterns and practices

## Agent Roster

### 1. Planner Agent

**Profile**: Strategic planning and task breakdown specialist

**Location**: `.github/agents/planner.agent.md`

**Expertise**:
- Breaking down complex problems into actionable tasks
- Creating project plans and roadmaps
- Identifying dependencies and critical path
- Estimating effort and timeline
- Risk assessment

**When to Use**:
- Planning a new feature or initiative
- Breaking down a complex issue
- Creating a release plan
- Organizing major refactoring

**Example Prompt**:
```
@planner I need to add OAuth2 authentication to our API.
Constraints: 2 sprints, cannot break existing clients, requires security review.
Success criteria: OAuth2 implemented, migration path for clients, docs updated.
```

**Output**: Task breakdown, dependencies, timeline, risks

### 2. Repo Bootstrap Agent

**Profile**: Repository initialization and setup expert

**Location**: Organization-level (ORG/.github-private if exists)

**Expertise**:
- Repository creation from template
- Initial configuration and setup
- Workflow configuration
- Documentation structure
- Team permissions

**When to Use**:
- Creating a new repository
- Migrating existing repo to org standards
- Setting up CI/CD for new project

**Example Prompt**:
```
@repo-bootstrap Initialize ORG_NAME/payment-service
Language: TypeScript, Owner: @org/payments-team
Optional modules: DevContainer, Security scanning, Code coverage
```

**Output**: Configured repository ready for development

### 3. Governance Agent

**Profile**: Organization governance and compliance expert

**Location**: `.github/agents/governance.agent.md`

**Expertise**:
- Organization policies and standards
- Repository rulesets and branch protection
- CODEOWNERS management
- Required file compliance
- Coverage matrix maintenance
- Policy check workflow interpretation

**When to Use**:
- Reviewing governance-related PRs
- Validating repository setup
- Updating CODEOWNERS or rulesets
- Proposing governance changes
- Investigating policy check failures

**Example Prompt**:
```
@governance I need to add a required check to the CI workflow.
Current: runs unit tests. Desired: also require integration tests.
Must align with org standards and not break existing PRs.
```

**Output**: Compliance assessment, required changes, implementation steps

### 4. CI Automation Agent

**Profile**: Build, test, and deployment automation expert

**Location**: `.github/agents/ci-automation.agent.md`

**Expertise**:
- GitHub Actions workflows
- Build and test automation
- Dependency management
- Security scanning (CodeQL, dependency review)
- Deployment pipelines
- Caching and optimization
- Matrix builds

**When to Use**:
- Creating or updating CI workflows
- Debugging workflow failures
- Optimizing build times
- Adding security scanning
- Setting up deployment automation

**Example Prompt**:
```
@ci-automation Our CI workflow is slow (15 min). 
Tech stack: Node.js 20, TypeScript, Jest tests.
Goal: Reduce to under 5 minutes.
```

**Output**: Workflow optimization strategy, caching setup, parallelization options

### 5. Docs & Diagrams Agent

**Profile**: Technical documentation and architecture diagram expert

**Location**: `.github/agents/docs-diagrams.agent.md`

**Expertise**:
- Technical writing
- Architecture documentation
- Mermaid diagrams
- API documentation
- Runbooks and procedures
- ADRs (Architecture Decision Records)

**When to Use**:
- Creating or updating documentation
- Drawing architecture diagrams
- Writing runbooks
- Documenting API changes
- Creating ADRs

**Example Prompt**:
```
@docs-diagrams Document our new authentication flow.
Context: Migrating from API keys to OAuth2, multiple client types.
Audience: Backend developers, client developers, security team.
Need: architecture doc + sequence diagram + integration guide.
```

**Output**: Documentation files, Mermaid diagrams, API docs

### 6. Security Agent

**Profile**: Security hardening and vulnerability management expert

**Location**: `.github/agents/security.agent.md` (if available)

**Expertise**:
- Security scanning tools (CodeQL, Dependabot, Trivy)
- Vulnerability assessment and remediation
- Secrets management
- Security best practices
- Threat modeling
- Incident response

**When to Use**:
- Reviewing security scan results
- Hardening repository security
- Investigating vulnerabilities
- Setting up security scanning
- Responding to security incidents

**Example Prompt**:
```
@security Review this dependency vulnerability: CVE-2024-XXXXX in lodash 4.17.20.
Impact: Prototype pollution in merge function.
Our usage: JSON processing in API endpoints.
```

**Output**: Risk assessment, remediation options, migration guide

### 7. Release & Change Management Agent

**Profile**: Release coordination and change management expert

**Location**: `.github/agents/release.agent.md` (if available)

**Expertise**:
- Release planning and coordination
- Semantic versioning
- Changelog generation
- Migration guides for breaking changes
- Deployment coordination
- Rollback procedures

**When to Use**:
- Planning a release
- Coordinating breaking changes
- Writing migration guides
- Managing deployment
- Creating release notes

**Example Prompt**:
```
@release Plan release v2.0.0 with breaking API changes.
Changes: Remove deprecated endpoints, update auth flow.
Timeline: 2 weeks. Need: migration guide, deprecation warnings, rollback plan.
```

**Output**: Release plan, migration guide, communication template

## Agent Levels

### Repository-Level Agents

Defined in each repository's `.github/agents/` directory.

**Characteristics**:
- Scoped to that repository
- Can reference repo-specific context
- Maintained by repository owners
- Examples: Planner, Governance, CI, Docs

### Organization-Level Agents

Defined in `ORG/.github-private/agents/` (if org-private repo exists).

**Characteristics**:
- Available across all repos in the organization
- Contain org-wide knowledge
- Maintained by Platform Team
- Examples: Repo Bootstrap, Security, Release

**Note**: Organization-level agents require a separate `ORG/.github-private` repository with restricted access.

## Using Agents

### In Copilot Chat

```
@agent-name [your prompt]
```

Example:
```
@governance Review this CODEOWNERS change for compliance
@ci-automation Debug this failing workflow run #123
@docs-diagrams Create a sequence diagram for the payment flow
```

### In Issues and PRs

Mention the agent in issue/PR descriptions or comments:

```
@planner Can you break this feature request into tasks?
@governance Does this change align with org standards?
```

### In Prompts

Use predefined prompts that invoke agents:

```
Use the "New Repo Bootstrap" prompt with @repo-bootstrap agent
Use the "Ruleset Update" prompt with @governance agent
```

See `.github/prompts/*.prompt.md` for reusable prompts.

## Agent Development

### Creating a New Agent

1. **Identify need**: What domain expertise is missing?
2. **Define scope**: What should the agent know and do?
3. **Create profile**: Write `.agent.md` file with:
   - Role and expertise
   - When to use
   - Input/output format
   - Example prompts
   - Best practices
4. **Test**: Validate with real use cases
5. **Document**: Add to this roster
6. **Communicate**: Notify teams of new agent

### Agent Profile Template

```markdown
# [Agent Name] Agent

## Role
[One-line description]

## Expertise
- [Area 1]
- [Area 2]
- [Area 3]

## When to Use
- [Scenario 1]
- [Scenario 2]

## Input Format
[What information the agent needs]

## Output Format
[What the agent provides]

## Example Prompt
```
[Example of how to use this agent]
```

## Best Practices
1. [Practice 1]
2. [Practice 2]

## Related Agents
- [Related Agent 1]
- [Related Agent 2]
```

### Maintaining Agents

- **Review quarterly**: Ensure agents are still relevant and accurate
- **Update with changes**: Keep agents aligned with org standards
- **Gather feedback**: Ask users what's working and what's not
- **Iterate**: Improve agent profiles based on real usage

## Best Practices

### For Using Agents

1. **Be specific**: Provide context, constraints, and success criteria
2. **One agent at a time**: Don't mix multiple agent concerns in one prompt
3. **Iterate**: Refine prompts based on agent responses
4. **Validate**: Review agent output, don't blindly accept
5. **Combine with prompts**: Use prompts that include agent invocations

### For Agent Profiles

1. **Clear scope**: Define what the agent does and doesn't do
2. **Examples**: Provide concrete examples of usage
3. **Consistent format**: Follow the template above
4. **Cross-reference**: Link to related agents and documentation
5. **Keep updated**: Maintain alignment with current standards

## Swarms

Swarms coordinate multiple agents for complex tasks. See [Swarms](swarms.md) for details.

## Related Documentation

- [Swarm Definitions](swarms.md)
- [Copilot Instructions](../../templates/repo-template/.github/copilot-instructions.md)
- [Agent Profiles](../../templates/repo-template/.github/agents/)
- [Prompts](../../templates/repo-template/.github/prompts/)

## Questions?

For questions about custom agents:
- Open an issue with "devex" label
- Tag @org/platform-team
- See [SUPPORT.md](https://github.com/ORG_NAME/.github/blob/main/SUPPORT.md)
