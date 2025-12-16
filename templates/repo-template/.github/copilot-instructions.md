# Copilot Workspace Instructions

This file provides high-level coding standards, preferences, and context for GitHub Copilot when working in this repository.

## Project Overview

<!-- Describe what this repository does, its architecture, and key technologies -->

This repository is part of the **ORG_NAME** organization and follows the "Dev Workflow OS v1" governance model.

## Coding Standards

### General Principles

- **Clarity over cleverness**: Write code that is easy to understand and maintain
- **Test before commit**: Ensure all tests pass before pushing
- **Small, focused changes**: Keep PRs small and purposeful
- **Documentation matters**: Update docs when changing behavior

### Code Style

<!-- Customize based on your language/framework -->

- Follow existing code style in the repository
- Use meaningful variable and function names
- Add comments for complex logic only
- Keep functions small and focused

### Testing

- Write tests for new features
- Update tests when changing behavior
- Aim for meaningful test coverage (not just metrics)
- Use descriptive test names

### Commits and PRs

- Write clear commit messages (present tense, imperative mood)
- Reference issue numbers in commits: "Fix #123: Description"
- Keep PRs focused on a single concern
- Fill out the PR template completely

## Architecture Guidelines

<!-- Describe key architectural patterns, boundaries, and conventions -->

### Project Structure

```
/src - Source code
/tests - Test files
/docs - Documentation
/.github - GitHub configuration
```

### Dependencies

- Prefer well-maintained, widely-used libraries
- Check for security vulnerabilities before adding dependencies
- Document why each major dependency is needed

## Security

- Never commit secrets, API keys, or credentials
- Use environment variables for configuration
- Review SECURITY.md for vulnerability reporting
- Follow principle of least privilege

## Performance

- Optimize for readability first, performance second
- Profile before optimizing
- Document performance-critical sections

## Integration with Governance

This repository follows organization-wide governance:

- Required files: README, LICENSE, .gitignore, CODEOWNERS
- Required workflows: policy-check, add-to-project, ci
- CODEOWNERS review required for sensitive paths
- See [dev-workflow-os](https://github.com/ORG_NAME/dev-workflow-os) for full governance docs

## Custom Agents

This repository includes custom agent profiles in `.github/agents/`:

- **Planner**: Strategic planning and task breakdown
- **Governance**: Ensure compliance with org standards
- **CI Automation**: Build, test, and deployment pipeline management
- **Docs/Diagrams**: Documentation and architecture diagram maintenance

Use these agents for specialized tasks via GitHub Copilot.

## Prompts

Reusable prompts are in `.github/prompts/`:

- `new-repo-bootstrap.prompt.md`: Initialize a new repository
- `ruleset-update.prompt.md`: Update repository rulesets
- `coverage-matrix-update.prompt.md`: Update coverage matrix
- `incident-triage.prompt.md`: Triage production incidents

## Additional Instructions

See `.github/instructions/*.instructions.md` for specialized guidance on:

- Governance changes
- Documentation standards

## Questions?

- Tag @org/platform-team in issues or PRs
- See [CONTRIBUTING.md](https://github.com/ORG_NAME/.github/blob/main/CONTRIBUTING.md)
