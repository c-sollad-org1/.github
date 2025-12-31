# GitHub Copilot Instructions for Code Review

This file contains instructions for GitHub Copilot when reviewing pull requests in this repository.

## General Code Review Standards

### Code Quality
- Review code for clarity, maintainability, and adherence to best practices
- Flag overly complex logic that could be simplified
- Identify potential bugs or edge cases not handled
- Suggest more descriptive variable and function names where appropriate
- Check for proper error handling and edge case coverage

### Security
- Identify potential security vulnerabilities (SQL injection, XSS, CSRF, etc.)
- Flag hardcoded secrets, API keys, or sensitive data
- Verify proper input validation and sanitization
- Check for secure authentication and authorization practices
- Ensure sensitive data is properly encrypted and handled

### Performance
- Identify inefficient algorithms or operations
- Flag unnecessary loops, redundant operations, or memory leaks
- Suggest optimization opportunities where performance could be improved

### Testing
- Verify that code changes include appropriate tests
- Check test coverage for new features and bug fixes
- Ensure tests are meaningful and test actual behavior, not implementation details

### Documentation
- Verify that complex logic includes explanatory comments
- Check that public APIs have proper documentation
- Ensure README and other documentation is updated when relevant

### Accessibility (for web content)
- Verify WCAG 2.1 AA compliance for UI changes
- Check for proper ARIA labels and semantic HTML
- Ensure keyboard navigation works properly
- Verify color contrast meets accessibility standards

## Review Approach

1. **Start with the big picture**: Understand the purpose of the PR before diving into details
2. **Be constructive**: Provide actionable feedback with specific suggestions
3. **Prioritize issues**: Distinguish between critical issues (security, bugs) and minor improvements (style, optimization)
4. **Recognize good work**: Acknowledge well-written code and clever solutions
5. **Ask questions**: When uncertain, ask clarifying questions rather than making assumptions

## Language-Specific Guidelines

### Python
- Follow PEP 8 style guidelines
- Use type hints where appropriate
- Prefer list comprehensions over map/filter when readable
- Use context managers (with statements) for resource management

### JavaScript/TypeScript
- Follow consistent naming conventions (camelCase for variables/functions, PascalCase for classes)
- Use async/await over raw promises for better readability
- Prefer const over let, avoid var
- Use TypeScript types instead of any when possible

### Markdown
- Use proper heading hierarchy
- Keep lines under 120 characters when reasonable
- Use code blocks with language specification for syntax highlighting

## What NOT to Flag

- Minor style inconsistencies that don't affect functionality (unless they violate established team standards)
- Personal coding preferences that are valid alternatives
- Existing issues not introduced by this PR (unless they're critical security issues)

## Output Format

When providing review comments:
- Be specific about the file and line number
- Explain WHY something should be changed, not just WHAT to change
- Provide code suggestions when possible
- Use a professional and helpful tone
