# Claude Skills Skill - Project Context

## Project Overview

This project provides a Claude skill that enables the creation, validation, and packaging of other Claude skills. It's a self-referential tool designed to bootstrap the skill creation process and ensure all skills meet Claude's requirements and best practices.

## Purpose

The skill-creator skill automates the process of creating new Claude skills by:
- Guiding users through skill design and requirements
- Automatically generating proper skill structure and files
- Validating skill files against Claude's specifications
- Packaging skills for distribution across Claude surfaces
- Providing platform-specific guidance for Claude.ai, API, and Claude Code

## Technology Stack

- **Python 3.8+**: All scripts and utilities
- **PyYAML**: For parsing and validating YAML frontmatter
- **Markdown**: For skill definitions and documentation
- **Standard library**: pathlib, argparse, re, json, typing

## Project Structure

```
claude-skills-skill/
├── .claude/                           # Claude Code configuration
│   ├── agents/
│   │   └── python-dev.md             # Python development agent
│   ├── settings.json                  # Team-shared settings
│   └── settings.local.json.example    # Local settings template
├── .claude-plugin/                    # Distributable skill plugin
│   ├── SKILL.md                      # Main skill definition
│   ├── scripts/                      # Python utilities
│   │   ├── __init__.py
│   │   ├── skill_utils.py           # Shared utilities
│   │   ├── validate_skill.py        # Skill validator
│   │   └── package_skill.py         # Skill packager
│   └── references/                   # Reference documentation
│       ├── skill-specification.md    # Technical spec
│       ├── platform-differences.md   # Platform guidance
│       └── skill-examples.md         # Example skills
├── .gitignore                        # Git ignore patterns
├── LICENSE                           # MIT License
├── README.md                         # Project documentation
├── CONTRIBUTING.md                   # Contribution guidelines
└── CLAUDE.md                         # This file
```

## Development Conventions

### Code Style

- **Python**: PEP 8 compliant, use Black formatter (88 char line length)
- **Type Hints**: Required for all function signatures
- **Docstrings**: Google-style docstrings for all public functions/classes
- **Error Handling**: Specific exceptions with clear, actionable messages

### Security Standards

- **Input Validation**: All user inputs must be validated
- **Path Safety**: Use pathlib and prevent path traversal attacks
- **No Code Execution**: Never use eval(), exec(), or unsafe deserialization
- **Secure Defaults**: Fail closed, validate before processing

### Git Workflow

- **Branch**: Create feature branches from main
- **Commits**: Use conventional commits (feat:, fix:, docs:, etc.)
- **Pull Requests**: Required for all changes, include tests
- **Reviews**: At least one approval required

## Using the Python Development Agent

All Python code in this project should be written using the `python-dev` agent:

```
Use the python-dev agent to implement the validation script
```

The python-dev agent automatically:
- Follows PEP 8 standards
- Adds comprehensive type hints
- Includes detailed docstrings
- Implements security best practices
- Creates robust error handling

## Testing Approach

### Manual Testing
- Test skill creation with various inputs
- Verify validation catches common errors
- Test packaging produces valid distributions
- Ensure cross-platform compatibility

### Validation Tests
- Valid skill files pass validation
- Invalid names, descriptions, frontmatter are caught
- Error messages are clear and actionable

### Integration Tests
- Test full workflow: create → validate → package
- Test on actual skill examples
- Verify output works on all Claude surfaces

## Skill Creation Workflow

When a user asks to create a skill, the skill-creator:

1. **Gather Requirements**
   - Ask about skill purpose and functionality
   - Determine if scripts/references are needed
   - Identify target platform(s)

2. **Generate Structure**
   - Create appropriate directory structure (.claude-plugin/ or .claude/skills/)
   - Generate SKILL.md with proper frontmatter
   - Create placeholder directories as needed

3. **Populate Content**
   - Write comprehensive skill instructions
   - Add platform-specific guidance
   - Include examples and best practices
   - Create helper scripts if requested

4. **Validate**
   - Run validation checks on generated files
   - Ensure all requirements are met
   - Provide feedback on any issues

5. **Package**
   - Create distributable format
   - Include all necessary files
   - Generate metadata/manifest

## Platform Considerations

### Claude.ai
- Skills are user-specific (not workspace-shared)
- Network access varies by user/admin settings
- Upload required through UI

### Claude API
- Skills are workspace-wide accessible
- No network access by default
- No package installation, pre-configured only
- Requires API integration

### Claude Code
- Full network access available
- Project-level and user-level skills
- Can use local file system
- CLI-based management

## Key Constraints

### Skill Naming
- Maximum 64 characters
- Lowercase letters, numbers, hyphens only
- Cannot contain "anthropic" or "claude"
- No XML tags

### Descriptions
- Non-empty, maximum 1024 characters
- Should clarify both functionality AND when to use
- No XML tags
- Action-oriented language for auto-invocation

### Token Efficiency
- Skills should be 30-50 tokens when inactive (frontmatter only)
- Use progressive loading (references loaded on-demand)
- Keep SKILL.md focused, move details to reference files

## Common Issues and Solutions

### Issue: Skill not being invoked automatically
**Solution**: Improve description with action-oriented language ("Use when...", "MUST be used for...")

### Issue: Validation fails on valid skill
**Solution**: Check YAML formatting, ensure all required fields present

### Issue: Path errors during packaging
**Solution**: Verify all referenced files exist and paths are relative to skill directory

### Issue: Cross-platform incompatibility
**Solution**: Use pathlib for all paths, avoid platform-specific assumptions

## Resources

- **Claude Skills Documentation**: https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview
- **Skills Blog Post**: https://claude.com/blog/skills
- **Engineering Post**: https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- **Skills Cookbook**: https://github.com/anthropics/claude-cookbooks/tree/main/skills

## Contributing

See CONTRIBUTING.md for detailed guidelines on:
- Setting up development environment
- Code review process
- Testing requirements
- Documentation standards

## License

This project is licensed under the MIT License - see LICENSE file for details.
