# GitHub Copilot Agents for Code Review

This directory contains custom GitHub Copilot agents designed to enhance pull request reviews. These agents are based on best practices from the [awesome-copilot](https://github.com/github/awesome-copilot) community repository.

> 📖 **For a comprehensive catalog of all available agents and prompts from awesome-copilot**, see [AWESOME_COPILOT_REFERENCE.md](../AWESOME_COPILOT_REFERENCE.md) which includes detailed tables with required inputs, outputs, and usage information for 10+ prompts and 5+ agents.

## Available Agents

### 1. Code Reviewer (`code-reviewer.agent.md`)
**Purpose**: General code quality and best practices review

**Specializes in**:
- Identifying bugs and potential issues
- Code readability and maintainability
- Design patterns and architecture
- Test coverage and quality
- Performance optimization

**When to use**: For all pull requests to ensure general code quality.

### 2. Security Reviewer (`security-reviewer.agent.md`)
**Purpose**: Security vulnerability detection and secure coding practices

**Specializes in**:
- OWASP Top 10 vulnerabilities
- Input validation and sanitization
- Authentication and authorization
- Cryptographic practices
- Dependency security
- Data protection

**When to use**: For PRs that touch authentication, data handling, external APIs, or any security-sensitive code.

### 3. Accessibility Expert (`accessibility-expert.agent.md`)
**Purpose**: Web accessibility and WCAG compliance

**Specializes in**:
- WCAG 2.1/2.2 Level AA compliance
- Keyboard navigation
- Screen reader compatibility
- Color contrast and visual accessibility
- Semantic HTML and ARIA

**When to use**: For PRs that modify UI components, forms, or any user-facing web content.

## How to Use These Agents

### In GitHub Copilot Chat

1. **Direct Agent Assignment**: When reviewing a PR in VS Code with GitHub Copilot, you can reference these agents:
   ```
   @workspace /reviewPR using the code-reviewer agent guidelines
   ```

2. **Specific Agent Review**: For targeted reviews:
   ```
   @workspace Review this PR for security issues using the security-reviewer agent
   ```
   ```
   @workspace Check accessibility compliance using the accessibility-expert agent
   ```

### In VS Code

1. Open the file you want reviewed
2. Open GitHub Copilot Chat (Ctrl+Shift+I or Cmd+Shift+I)
3. Reference the agent in your prompt:
   ```
   Review this component using the accessibility-expert agent guidelines from .github/agents/
   ```

### Automatic PR Reviews

GitHub Copilot can automatically review PRs if configured in your repository settings:

1. Go to repository Settings
2. Navigate to GitHub Copilot section
3. Enable automatic code review
4. The agents' instructions will be applied automatically

## Agent Configuration

These agents follow the structure recommended by the awesome-copilot project:

- **Clear role definition**: Each agent has a specific expertise area
- **Structured approach**: Step-by-step review process
- **Examples and patterns**: Concrete code examples for common issues
- **Priority levels**: Critical, High, and Medium priority classifications
- **Educational tone**: Explanations of why issues matter and how to fix them

## Customizing Agents

You can customize these agents for your team's specific needs:

1. Edit the `.agent.md` files to add your team's conventions
2. Add language-specific guidelines
3. Include references to your team's style guides
4. Add examples from your codebase

## Repository-Wide Instructions

The `.github/copilot-instructions.md` file contains general guidelines that apply to all code reviews. These complement the specialized agents and are automatically applied by GitHub Copilot.

## Best Practices

### Use Multiple Agents
For comprehensive reviews, consider using multiple agents:
- Start with **Code Reviewer** for general quality
- Add **Security Reviewer** for security-sensitive code
- Include **Accessibility Expert** for UI changes

### Combine with Human Review
These agents enhance but don't replace human code review:
- Agents catch common issues and enforce standards
- Humans evaluate design decisions and business logic
- Best results come from AI + human collaboration

### Iterative Improvement
- Review agent feedback and adjust agents as needed
- Add team-specific examples to agent files
- Update priority levels based on your team's needs
- Share successful patterns across agents

## Resources

### Awesome Copilot Repository
- [github/awesome-copilot](https://github.com/github/awesome-copilot) - Community-contributed agents and instructions
- [Agent Documentation](https://github.com/github/awesome-copilot/blob/main/docs/README.agents.md)

### GitHub Copilot Documentation
- [Custom Agents Guide](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Copilot Instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)
- [Code Review with Copilot](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review)

### Security Resources
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)

### Accessibility Resources
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [WebAIM](https://webaim.org/)

## Contributing

To improve these agents:
1. Test agents on real PRs
2. Document edge cases and improvements
3. Share examples of effective agent feedback
4. Keep agents updated with new best practices

## Feedback

These agents are living documents. As you use them, you'll discover:
- Missing patterns or common issues
- Areas where feedback could be more specific
- New security vulnerabilities or accessibility patterns
- Team-specific conventions to add

Update the agents regularly to make them more effective for your team.
