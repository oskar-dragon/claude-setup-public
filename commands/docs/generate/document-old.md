---
description: Generate documentation for a specific component or feature.
---

## Usage

```
/document [code snippet, file path, or concept] [flags...]
```

### Flags

- `mode=analysis` (default): Full codebase analysis before documentation
- `mode=context`: Use existing context from previous `/explain` command
- `file=true|false`: (default: false) Creates a new file with documentation as an output in `docs` directory in root directory, and uses numbers as prefixes (e.g. `001-api.md`)

## Mode-Specific Behaviour

### Analysis Mode (default)

**Always start by analysing the codebase first:**

1. **Codebase Structure Analysis**

- Use filesystem tools to explore the target component/feature structure
- Identify all related files, dependencies, and configuration
- Map relationships between components, services, and utilities
- Understand the technology stack and external dependencies
- Identify environment-specific configurations and requirements

2. **Context Discovery**

- Search for existing related documentation
- Identify integration points with other systems/components
- Understand user personas and use cases
- Map testing strategies and patterns already in place

### Context Mode

**Use existing context from previous `/explain` command:**

1. **Context Validation**

- Check if previous `/explain` context is available and relevant
- Validate context freshness and accuracy
- Identify any gaps in existing context

2. **Context Enhancement**

- Supplement missing technical details if needed
- Validate current implementation against context
- Add recent changes not captured in original context

## Content Generation Standards

### Link-First Approach

**NEVER copy/paste code blocks - always link to files instead:**

```markdown
**Implementation**: See [`launch-darkly-adapter.ts`](../apps/buyers/src/core/flags/launch-darkly-adapter.ts)

**Location**: [`apps/buyers/src/core/flags/`](../apps/buyers/src/core/flags/)

**Configuration**: See [`middleware.ts`](../apps/buyers/src/middleware.ts)
```

**File Reference Patterns:**

- Use relative paths from documentation location
- Link to entire directories for comprehensive implementations
- Reference configuration files explicitly

### Technology Documentation Integration

**Always link external technologies to official documentation:**

```markdown
**SDK**: [LaunchDarkly Node.js SDK](https://docs.launchdarkly.com/sdk/server-side/node-js)
**Framework**: [Next.js App Router](https://nextjs.org/docs/app)
**Validation**: [Zod Schema Validation](https://zod.dev)
```

**Technology Linking Standards:**

- Link to specific sections of official docs when possible
- Include version-specific documentation where relevant
- Reference setup guides and best practices from official sources
- Link troubleshooting sections from official documentation

### Documentation Structure Template

Follow this structure, adapting sections based on the component/feature being documented:

```markdown
# [Component/Feature Name]

## Overview

[1-2 paragraph overview including technology stack and architecture approach]

## Architecture

[Explain the overall architecture - use diagrams where helpful]

## Environment Configuration

[Environment variables, setup requirements with links to config files]

## Implementation Details

[Organised by context/application with file links]

## Usage Examples

[Practical examples with file references, not code copies unless it's better to keep them here as they will change too often]

## Best Practices

### [Category] (e.g., Naming Conventions)

[Specific guidance with examples and optional diagrams]

### [Category] (e.g., Lifecycle Management)

[Specific guidance with examples and optional diagrams]

## Testing

[Testing approaches with links to test files and examples if applicable]

## Security Considerations

[Security implications, CSP, environment variables if applicable]

## Troubleshooting

### Common Issues

[Issue descriptions with solutions]

### Debug Mode

[How to enable debugging ]

## Quick Reference

### [Component] Checklist

- [ ] [Action item]
- [ ] [Action item]

## Related Documentation

[Links to related internal documentation]
[Links to related external documentation]
```

## Diagram Integration

For some cases, diagrams can provide a clearer understanding of complex systems or processes. Here are some guidelines for when I want you to use diagrams:

**Identify when diagrams would be helpful:**

- Architecture overviews
- Data flow diagrams
- Component relationship diagrams
- Integration patterns
- User journey flows

**Diagram Creation Pattern:**

```markdown
## Architecture Overview

[Architecture Diagram](./diagrams/feature-flags-architecture.md)
```

**When to suggest diagram creation:**

- Complex component relationships
- Multi-step processes or workflows
- Integration patterns between systems
- State management flows
- Error handling paths

## Cross-Reference Network

**Always include related documentation:**

```markdown
## Related Documentation

- [Team Processes Guide](./001-team-processes.md) - For coordination around feature rollouts
- [Testing Guide](./004-testing-guide.md) - For comprehensive testing strategies
- [API Documentation](./api-reference.md) - For related API endpoints
```

**Cross-reference discovery:**

- Search existing documentation for mentions of the current topic
- Identify parent/child relationships in feature hierarchies
- Link to setup guides, troubleshooting docs, and related tools
- Include links to team processes and workflow documentation

## Command Integration

**Include integration with other Claude Code commands:**

- `/diagram` to create visual representations

## Quality Assurance Standards

**Documentation Quality Checks:**

- Validate all file links point to existing files
- Ensure external links are current and accessible
- Check that code examples match current implementation patterns
- Verify environment variables and configuration examples are accurate
- Confirm technology versions match project dependencies

**Maintenance Planning:**

- Include last updated timestamps

## Specific Technical Requirements

**TypeScript Integration:**

- Include type definitions and interfaces where relevant
- Link to type definition files rather than copying types

**Testing Integration:**

- Link to test files rather than copying test code
- Include both unit and integration testing approaches
- Reference E2E testing patterns and setup
- Document mocking and test data strategies

**Performance Considerations:**

- Include performance implications and optimisations
- Reference monitoring and observability setup
- Document caching strategies and considerations
- Include scaling and load testing approaches
