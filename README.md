# .github Repository

This repository contains the default community health files and GitHub Copilot configurations for the c-sollad-org1 organization.

## Contents

### Community Health Files
- `CODE_OF_CONDUCT.md` - Code of conduct for contributors
- `CONTRIBUTING.md` - Guidelines for contributing to projects
- `SECURITY.md` - Security policy and vulnerability reporting
- `SUPPORT.md` - Support resources
- `PULL_REQUEST_TEMPLATE.md` - Template for pull requests

### GitHub Copilot Configuration

This repository includes advanced GitHub Copilot configurations to enhance code reviews:

#### 📋 Copilot Instructions (`.github/copilot-instructions.md`)
Repository-wide instructions that guide GitHub Copilot's behavior during code reviews. These instructions cover:
- General code quality standards
- Security best practices
- Performance considerations
- Testing requirements
- Documentation guidelines
- Language-specific conventions

#### 🤖 Custom Copilot Agents (`.github/agents/`)
Specialized AI agents based on the [awesome-copilot](https://github.com/github/awesome-copilot) project:

**1. Code Reviewer** (`code-reviewer.agent.md`)
- General code quality and best practices
- Bug detection and edge case identification
- Design patterns and maintainability
- Test coverage analysis

**2. Security Reviewer** (`security-reviewer.agent.md`)
- OWASP Top 10 vulnerability detection
- Secure coding practices
- Authentication and authorization review
- Input validation and sanitization
- Dependency security

**3. Accessibility Expert** (`accessibility-expert.agent.md`)
- WCAG 2.1/2.2 Level AA compliance
- Keyboard navigation and screen reader support
- Semantic HTML and ARIA best practices
- Color contrast and visual accessibility

## Using GitHub Copilot Agents

### In VS Code

1. Open GitHub Copilot Chat (Ctrl+Shift+I / Cmd+Shift+I)
2. Reference an agent in your review request:
   ```
   @workspace Review this PR using the security-reviewer agent
   ```
   ```
   @workspace Check accessibility using the accessibility-expert agent
   ```

### In GitHub Pull Requests

When GitHub Copilot is enabled for automatic PR reviews, it will automatically apply the instructions and agent guidelines from this repository.

### For Comprehensive Reviews

Use multiple agents for thorough code review:
```
@workspace Review this PR using:
1. code-reviewer agent for general quality
2. security-reviewer agent for security issues
3. accessibility-expert agent for UI accessibility
```

## Setup for Your Repository

These configurations automatically apply to all repositories in the c-sollad-org1 organization. No additional setup is required!

### Customizing for Specific Repositories

If you need repository-specific instructions:
1. Create `.github/copilot-instructions.md` in your repository
2. Add custom agents to `.github/agents/` in your repository
3. Repository-specific configs will be used alongside organization defaults

## Benefits

✅ **Consistent Code Quality** - Automated checks for common issues
✅ **Security First** - Proactive vulnerability detection
✅ **Accessibility Built-In** - WCAG compliance from the start
✅ **Faster Reviews** - AI handles routine checks, humans focus on design
✅ **Educational** - Learn best practices from agent feedback

## Resources

### GitHub Copilot Documentation
- [Custom Agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Copilot Instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)
- [Automatic Code Review](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review)

### Awesome Copilot Project
- [Repository](https://github.com/github/awesome-copilot)
- [Agent Documentation](https://github.com/github/awesome-copilot/blob/main/docs/README.agents.md)
- [Blog: Writing Great Agents](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/)

### Security & Accessibility Standards
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)

## Contributing

To improve these configurations:
1. Test agents on real PRs and gather feedback
2. Document common patterns and edge cases
3. Submit PRs with improvements and examples
4. Keep agents updated with evolving best practices

## Feedback

These agents are designed to evolve with your team's needs. If you find:
- Missing patterns or common issues
- Areas where feedback could be more specific
- New vulnerabilities or accessibility patterns
- Team-specific conventions to add

Please open an issue or submit a PR!

## License

See [LICENSE](LICENSE) file for details.
