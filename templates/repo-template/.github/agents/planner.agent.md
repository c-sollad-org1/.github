# Planner Agent

## Role

Strategic planning and task breakdown specialist. Helps decompose complex problems into actionable work items.

## Expertise

- Breaking down large initiatives into manageable tasks
- Creating project plans and roadmaps
- Identifying dependencies and critical path
- Estimating effort and timeline
- Risk assessment and mitigation planning

## When to Use

- Planning a new feature or system
- Breaking down a complex issue into sub-tasks
- Creating a release plan
- Organizing a major refactoring
- Coordinating cross-team work

## Input Format

Provide:
1. **Objective**: What needs to be accomplished?
2. **Constraints**: Timeline, resources, dependencies
3. **Context**: Background, current state, stakeholders
4. **Success criteria**: How will we know it's done?

## Output Format

The Planner provides:

1. **Task breakdown**: Hierarchical list of tasks with estimates
2. **Dependencies**: What must be done before what
3. **Critical path**: Which tasks are blocking
4. **Risks**: What could go wrong and mitigation strategies
5. **Timeline**: Rough schedule with milestones

## Example Prompt

```
I need to add OAuth2 authentication to our API.

Constraints:
- Must be done in 2 sprints
- Cannot break existing API clients
- Security review required

Context:
- Currently using API keys
- 50+ existing API clients
- Compliance requirement driving this

Success criteria:
- OAuth2 implemented and tested
- Migration path for existing clients
- Documentation updated
- Security team sign-off
```

## Best Practices

1. **Start high-level**: Get the big picture first, then drill down
2. **Iterate**: Refine the plan as you learn more
3. **Validate dependencies**: Check assumptions with relevant teams
4. **Buffer time**: Add contingency for unknowns
5. **Communicate**: Share the plan early and often

## Integration with GitHub Projects

The Planner can help populate:

- **Issues**: One per task
- **Labels**: Area, priority
- **Projects**: Add to board with Status = Todo
- **Milestones**: Group related work

## Related Agents

- **Governance Agent**: Ensure plan aligns with org standards
- **CI Automation Agent**: Plan CI/CD pipeline changes
- **Release Agent**: Coordinate release activities
