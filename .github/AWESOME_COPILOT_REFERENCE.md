# Awesome Copilot PR Review - Custom Prompts and Agents Reference

This document catalogs custom prompts and agents from the [github/awesome-copilot](https://github.com/github/awesome-copilot) repository that are relevant to reviewing PRs and PR automation. Each entry includes required inputs, output documents, and usage information.

## Table of Contents
- [Custom Agents for PR Review](#custom-agents-for-pr-review)
- [Custom Prompts for PR Automation](#custom-prompts-for-pr-automation)
- [Instructions for Code Review](#instructions-for-code-review)
- [How to Use](#how-to-use)

---

## Custom Agents for PR Review

Custom agents are specialized AI assistants that can be invoked in GitHub Copilot Chat or VS Code to perform specific tasks.

### 1. Code Review Agent (Gilfoyle)

| Attribute | Details |
|-----------|---------|
| **Agent Name** | Gilfoyle / Code Review Agent |
| **Source** | `agents/gilfoyle.agent.md` in awesome-copilot |
| **Purpose** | Conducts technically rigorous code reviews focusing on quality, architecture, performance, and security |
| **Required Inputs** | - Code files or PR to review<br>- Optional: Specific review focus (security, performance, architecture) |
| **Output Documents** | - Code review comments<br>- Inline suggestions<br>- Severity-ranked issues<br>- Architectural feedback |
| **Use With** | - GitHub Pull Requests<br>- VS Code Copilot Chat<br>- Copilot CLI |
| **Example Usage** | `@workspace /review using Gilfoyle agent guidelines` |

### 2. Accessibility Expert Agent

| Attribute | Details |
|-----------|---------|
| **Agent Name** | Accessibility Expert |
| **Source** | `agents/accessibility-expert.agent.md` (custom implementation) |
| **Purpose** | Reviews code for WCAG 2.1/2.2 compliance and web accessibility |
| **Required Inputs** | - HTML/JSX/TSX files<br>- UI components<br>- Form implementations |
| **Output Documents** | - WCAG compliance report<br>- Accessibility violations<br>- ARIA implementation suggestions<br>- Keyboard navigation issues |
| **Use With** | - Frontend PRs<br>- UI component reviews<br>- Web application development |
| **Example Usage** | `@workspace Check this component for WCAG compliance using accessibility-expert agent` |

### 3. Security Reviewer Agent

| Attribute | Details |
|-----------|---------|
| **Agent Name** | Security Reviewer |
| **Source** | `agents/security-reviewer.agent.md` (custom implementation) |
| **Purpose** | Identifies security vulnerabilities and ensures secure coding practices |
| **Required Inputs** | - Source code files<br>- API implementations<br>- Database queries<br>- Authentication/authorization code |
| **Output Documents** | - Security vulnerability report<br>- OWASP Top 10 findings<br>- Remediation steps<br>- Security best practice violations |
| **Use With** | - Security-sensitive PRs<br>- Backend code reviews<br>- API implementations |
| **Example Usage** | `@workspace Review this PR for security vulnerabilities using security-reviewer agent` |

### 4. API Architect Agent

| Attribute | Details |
|-----------|---------|
| **Agent Name** | API Architect |
| **Source** | `agents/api-architect.agent.md` in awesome-copilot |
| **Purpose** | Reviews and designs RESTful APIs, ensures best practices |
| **Required Inputs** | - API endpoint definitions<br>- OpenAPI/Swagger specs<br>- Controller/route implementations |
| **Output Documents** | - API design recommendations<br>- RESTful best practices<br>- Versioning strategies<br>- Documentation suggestions |
| **Use With** | - API development PRs<br>- Backend architecture reviews<br>- Microservices design |
| **Example Usage** | `@workspace Review this API design using API Architect agent` |

### 5. Migration Specialist Agent

| Attribute | Details |
|-----------|---------|
| **Agent Name** | Migration Specialist |
| **Source** | `agents/migration-specialist.agent.md` in awesome-copilot |
| **Purpose** | Assists with code migrations, framework upgrades, and refactoring |
| **Required Inputs** | - Source code to migrate<br>- Target framework/version<br>- Migration requirements |
| **Output Documents** | - Migration plan<br>- Code transformation suggestions<br>- Breaking changes report<br>- Test updates needed |
| **Use With** | - Framework upgrade PRs<br>- Language version updates<br>- Library migration projects |
| **Example Usage** | `@workspace Help migrate this code to React 18 using Migration Specialist` |

---

## Custom Prompts for PR Automation

Custom prompts are reusable templates that can be invoked to perform specific review or automation tasks.

### 1. Conventional Commit Validator

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | conventional-commit.prompt.md |
| **Source** | `prompts/conventional-commit.prompt.md` in awesome-copilot |
| **Purpose** | Validates and suggests conventional commit messages |
| **Required Inputs** | - Commit message or PR description<br>- Changed files context |
| **Output Documents** | - Validated commit message<br>- Suggestions for improvement<br>- Conventional Commits compliance report |
| **Use With** | - Pre-commit hooks<br>- PR title validation<br>- Commit message standardization |
| **Example Usage** | `@workspace Validate this commit message against Conventional Commits` |

### 2. Add Educational Comments

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | add-educational-comments.prompt.md |
| **Source** | `prompts/add-educational-comments.prompt.md` in awesome-copilot |
| **Purpose** | Adds helpful, educational comments to code during review |
| **Required Inputs** | - Source code files<br>- Target audience (junior, mid, senior developers) |
| **Output Documents** | - Code with inline educational comments<br>- Explanations of patterns and practices<br>- Links to documentation |
| **Use With** | - Code reviews for learning<br>- Onboarding documentation<br>- Knowledge transfer |
| **Example Usage** | `@workspace Add educational comments to this code for junior developers` |

### 3. .NET Best Practices Review

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | dotnet-best-practices.prompt.md |
| **Source** | `prompts/dotnet-best-practices.prompt.md` in awesome-copilot |
| **Purpose** | Reviews .NET/C# code for best practices and patterns |
| **Required Inputs** | - C# source files<br>- .NET project structure |
| **Output Documents** | - Best practices violations<br>- Performance recommendations<br>- C# idiom suggestions<br>- LINQ optimization tips |
| **Use With** | - .NET PRs<br>- C# code reviews<br>- ASP.NET Core applications |
| **Example Usage** | `@workspace Review this C# code for .NET best practices` |

### 4. .NET Design Pattern Review

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | dotnet-design-pattern-review.prompt.md |
| **Source** | `prompts/dotnet-design-pattern-review.prompt.md` in awesome-copilot |
| **Purpose** | Analyzes .NET code for design pattern usage and suggests improvements |
| **Required Inputs** | - C# class implementations<br>- Architecture context |
| **Output Documents** | - Design pattern identification<br>- Pattern misuse warnings<br>- Alternative pattern suggestions<br>- SOLID principles violations |
| **Use With** | - Architecture reviews<br>- Refactoring PRs<br>- Design discussions |
| **Example Usage** | `@workspace Analyze design patterns in this C# code` |

### 5. Create GitHub PR from Specification

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | create-github-pull-request-from-specification.prompt.md |
| **Source** | `prompts/create-github-pull-request-from-specification.prompt.md` in awesome-copilot |
| **Purpose** | Generates a complete pull request from a specification document |
| **Required Inputs** | - Specification document (markdown, doc)<br>- Target repository<br>- Base branch |
| **Output Documents** | - Implementation code<br>- PR description<br>- Tests<br>- Documentation updates |
| **Use With** | - Feature development automation<br>- Specification-driven development<br>- Automated PR creation |
| **Example Usage** | `@workspace Create a PR implementing this specification` |

### 6. Pytest Coverage Analysis

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | pytest-coverage.prompt.md |
| **Source** | `prompts/pytest-coverage.prompt.md` in awesome-copilot |
| **Purpose** | Analyzes Python test coverage and suggests improvements |
| **Required Inputs** | - Python source files<br>- Existing test files<br>- Coverage report (optional) |
| **Output Documents** | - Coverage gaps report<br>- Suggested test cases<br>- Missing edge case tests<br>- Test quality assessment |
| **Use With** | - Python PR reviews<br>- Test improvement tasks<br>- Quality gate enforcement |
| **Example Usage** | `@workspace Analyze test coverage for this Python module` |

### 7. Model Recommendation

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | model-recommendation.prompt.md |
| **Source** | `prompts/model-recommendation.prompt.md` in awesome-copilot |
| **Purpose** | Recommends the best AI model for a given review or coding task |
| **Required Inputs** | - Task description<br>- Code complexity<br>- Domain (web, data science, etc.) |
| **Output Documents** | - Recommended model (GPT-4, Claude, etc.)<br>- Justification<br>- Alternative models<br>- Cost considerations |
| **Use With** | - Complex code reviews<br>- Specialized domain tasks<br>- Optimization of AI usage |
| **Example Usage** | `@workspace What AI model should I use for reviewing this algorithm?` |

### 8. Code Exemplars Blueprint Generator

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | code-exemplars-blueprint-generator.prompt.md |
| **Source** | `prompts/code-exemplars-blueprint-generator.prompt.md` in awesome-copilot |
| **Purpose** | Extracts and documents code best practices from existing codebase |
| **Required Inputs** | - Codebase or specific modules<br>- Language/framework<br>- Target patterns to document |
| **Output Documents** | - Best practice examples<br>- Pattern documentation<br>- Anti-pattern warnings<br>- Team coding standards |
| **Use With** | - Creating team guidelines<br>- Onboarding documentation<br>- Style guide generation |
| **Example Usage** | `@workspace Generate code examples showing our React best practices` |

### 9. Dockerfile Best Practices

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | dockerfile-best-practices.prompt.md |
| **Source** | `prompts/dockerfile-best-practices.prompt.md` in awesome-copilot |
| **Purpose** | Reviews Dockerfiles for security, performance, and best practices |
| **Required Inputs** | - Dockerfile<br>- docker-compose.yml (optional)<br>- Deployment context |
| **Output Documents** | - Security issues<br>- Image optimization suggestions<br>- Layer caching improvements<br>- Multi-stage build recommendations |
| **Use With** | - Container PRs<br>- DevOps reviews<br>- Security audits |
| **Example Usage** | `@workspace Review this Dockerfile for best practices` |

### 10. Generate GitHub Issue from Unmet Requirements

| Attribute | Details |
|-----------|---------|
| **Prompt Name** | generate-github-issue-from-unmet-requirements.prompt.md |
| **Source** | `prompts/generate-github-issue-from-unmet-requirements.prompt.md` in awesome-copilot |
| **Purpose** | Creates GitHub issues for requirements not met in implementation |
| **Required Inputs** | - Requirements document<br>- Current implementation<br>- PR or code context |
| **Output Documents** | - GitHub issue descriptions<br>- Requirements gap analysis<br>- Implementation suggestions<br>- Acceptance criteria |
| **Use With** | - Requirements tracking<br>- Post-PR analysis<br>- Project management |
| **Example Usage** | `@workspace Find unmet requirements and create issues` |

---

## Instructions for Code Review

Instructions are passive guidelines that automatically apply to matching files during code completion and review.

### 1. Generic Code Review Instructions

| Attribute | Details |
|-----------|---------|
| **Instruction Name** | code-review-generic.instructions.md |
| **Source** | `instructions/code-review-generic.instructions.md` in awesome-copilot |
| **Purpose** | General code review standards for all languages |
| **Applies To** | All files (*.* or configurable patterns) |
| **Guidelines Include** | - Code quality standards<br>- Security basics<br>- Performance tips<br>- Documentation requirements |
| **Use With** | - Repository-wide standards<br>- Baseline code quality<br>- Cross-language projects |
| **Installation** | Place in `.github/copilot-instructions.md` |

### 2. Language-Specific Instructions

| Language | Instruction File | Key Guidelines |
|----------|-----------------|----------------|
| **Python** | `python.instructions.md` | - PEP 8 compliance<br>- Type hints<br>- Docstring conventions |
| **JavaScript/TypeScript** | `typescript.instructions.md` | - ESLint rules<br>- TypeScript types over any<br>- Async/await patterns |
| **Java** | `java.instructions.md` | - JavaDoc standards<br>- Exception handling<br>- Design patterns |
| **Go** | `go.instructions.md` | - Go idioms<br>- Error handling<br>- Package structure |
| **Rust** | `rust.instructions.md` | - Ownership patterns<br>- Error handling with Result<br>- Cargo best practices |

### 3. Framework-Specific Instructions

| Framework | Instruction File | Key Guidelines |
|-----------|-----------------|----------------|
| **React** | `react.instructions.md` | - Component patterns<br>- Hooks usage<br>- Performance optimization |
| **Vue** | `vue.instructions.md` | - Composition API<br>- Reactivity patterns<br>- Component organization |
| **Django** | `django.instructions.md` | - Model best practices<br>- View patterns<br>- Security settings |
| **Spring Boot** | `spring-boot.instructions.md` | - Bean management<br>- REST API design<br>- Security configuration |

---

## How to Use

### In VS Code

1. **Using Agents:**
   ```
   @workspace /review using [agent-name] guidelines
   ```
   Example: `@workspace Review this PR using security-reviewer agent`

2. **Using Prompts:**
   ```
   @workspace [prompt-description]
   ```
   Example: `@workspace Check this code for .NET best practices`

3. **Combining Multiple Agents:**
   ```
   @workspace Review using code-reviewer, security-reviewer, and accessibility-expert agents
   ```

### In GitHub Copilot Chat

1. Open Copilot Chat in your IDE
2. Reference the agent or prompt you want to use
3. Provide context (files, code selection, PR number)
4. Review the output and suggestions

### Automatic Application

When you place instruction files in `.github/copilot-instructions.md` or use language-specific instructions, Copilot automatically applies them during:
- Code completion
- Code review
- Copilot Chat interactions
- PR reviews (if automatic review is enabled)

### Installing from Awesome Copilot

1. **Via MCP Server (Recommended):**
   - Install the awesome-copilot MCP server in VS Code
   - Browse and install agents/prompts from the catalog
   - Use directly in Copilot Chat

2. **Manual Installation:**
   - Download agent/prompt files from [github/awesome-copilot](https://github.com/github/awesome-copilot)
   - Place in `.github/agents/` directory
   - Reference in Copilot Chat

3. **Via Package Manager:**
   ```bash
   # Using the awesome-copilot CLI (if available)
   copilot-install agent gilfoyle
   copilot-install prompt conventional-commit
   ```

---

## Priority Guidelines for PR Review

When using multiple agents or prompts, follow this priority order:

### 1. Critical Reviews (Must Complete)
- **Security Reviewer**: Check for vulnerabilities first
- **Conventional Commit**: Ensure proper commit messages
- **Accessibility Expert**: For any UI changes

### 2. Important Reviews (Should Complete)
- **Code Reviewer**: General quality check
- **Best Practices Prompts**: Language/framework specific
- **Test Coverage**: Ensure adequate testing

### 3. Optional Reviews (Nice to Have)
- **Educational Comments**: For team learning
- **Design Pattern Review**: For architecture discussions
- **Model Recommendation**: For optimization

---

## Examples by Use Case

### Use Case 1: Full Stack PR Review
```
@workspace Review this PR using:
1. security-reviewer for backend files
2. accessibility-expert for frontend components  
3. code-reviewer for overall quality
```

### Use Case 2: API Development
```
@workspace Review this API implementation using:
1. API Architect agent for design
2. security-reviewer for vulnerabilities
3. .NET best practices prompt (if applicable)
```

### Use Case 3: Frontend UI PR
```
@workspace Review this UI PR using:
1. accessibility-expert for WCAG compliance
2. code-reviewer for component quality
3. React best practices instructions
```

### Use Case 4: Database Migration
```
@workspace Review this migration using:
1. security-reviewer for SQL injection risks
2. Migration Specialist for upgrade path
3. Best practices for database schema
```

---

## Additional Resources

- **Awesome Copilot Repository**: [github.com/github/awesome-copilot](https://github.com/github/awesome-copilot)
- **Awesome Copilot Index**: [pez.github.io/awesome-copilot-index](https://pez.github.io/awesome-copilot-index/)
- **Agent Documentation**: [docs/README.agents.md](https://github.com/github/awesome-copilot/blob/main/docs/README.agents.md)
- **Prompt Documentation**: [docs/README.prompts.md](https://github.com/github/awesome-copilot/blob/main/docs/README.prompts.md)
- **Instructions Guide**: [docs/README.instructions.md](https://github.com/github/awesome-copilot/blob/main/docs/README.instructions.md)

---

## Contributing

To add new agents or prompts to this reference:
1. Test the agent/prompt in your workflow
2. Document inputs, outputs, and usage
3. Add examples and use cases
4. Submit a PR to update this document

---

## Version History

- **v1.0** - Initial reference document with core agents and prompts for PR review
- Based on awesome-copilot repository as of December 2024
