# Claude Skills Skill

A Claude skill that creates, validates, and packages other Claude skills. This meta-skill automates the process of building new skills that extend Claude's capabilities across all platforms (Claude.ai, API, and Claude Code).

---

> [!IMPORTANT]
> **📦 This repository has been archived and is now read-only.**
>
> The skill-creator skill has moved to the [jgardner04/skills](https://github.com/jgardner04/skills) repository.
>
> **➡️ Find the latest version here: [skills/skill-creator](https://github.com/jgardner04/skills/tree/main/skills/skill-creator)**
>
> Please submit any issues, pull requests, or questions to the new repository.

---

## What Are Claude Skills?

Claude Skills are modular capabilities that extend Claude's functionality. Each skill packages instructions, metadata, and optional resources (scripts, templates) that Claude uses automatically when relevant. Skills enable:

- **Specialized workflows** - Multi-step processes tailored to specific tasks
- **Domain expertise** - Deep knowledge in particular areas
- **Tool integration** - Combining Claude with external tools and APIs
- **Reusable patterns** - Standardized approaches to common problems

## What Does This Skill Do?

The skill-creator skill helps you build new Claude skills by:

1. **Guiding creation** - Asks the right questions to understand your skill requirements
2. **Generating structure** - Creates proper directory structure and files automatically
3. **Ensuring quality** - Validates that skills meet all Claude requirements
4. **Enabling distribution** - Packages skills for sharing across platforms
5. **Teaching best practices** - Provides platform-specific guidance and examples

## Features

- ✅ **Automated skill generation** - Complete skill structure with one request
- ✅ **Cross-platform support** - Works on Claude.ai, API, and Claude Code
- ✅ **Validation tools** - Ensures skills meet all technical requirements
- ✅ **Packaging utilities** - Creates distributable skill plugins
- ✅ **Security-focused** - Prevents common vulnerabilities in generated code
- ✅ **Type-safe Python** - All utilities use comprehensive type hints
- ✅ **Comprehensive docs** - Includes spec, examples, and best practices

## Quick Start

### Installation

#### Option 1: Claude Code (Recommended for development)

```bash
# Clone the repository
git clone https://github.com/jgardner04/claude-skills-skill.git
cd claude-skills-skill

# The skill is ready to use! Claude will automatically detect it.
```

#### Option 2: As a Plugin (For distribution)

```bash
# Download the latest release
curl -L https://github.com/jgardner04/claude-skills-skill/releases/latest/download/skill-creator.zip -o skill-creator.zip

# Install the plugin
# - For Claude.ai: Upload through the Skills UI
# - For Claude Code: Extract to ~/.claude/plugins/skill-creator/
# - For API: Add to your workspace skills directory
```

### Basic Usage

Simply ask Claude to create a skill:

```
Create a new skill called "git-helper" that helps with git commands and workflow
```

Claude will:
1. Ask clarifying questions about your skill
2. Generate the complete skill structure
3. Validate all files
4. Optionally package it for distribution

### Command-Line Tools

The skill includes standalone validation and packaging tools:

```bash
# Validate a skill
python .claude-plugin/scripts/validate_skill.py path/to/skill/

# Package a skill for distribution
python .claude-plugin/scripts/package_skill.py path/to/skill/ --output skill-name.zip
```

## Project Structure

```
claude-skills-skill/
├── .claude/                           # Claude Code configuration
│   ├── agents/
│   │   └── python-dev.md             # Python development agent
│   ├── settings.json                  # Team settings
│   └── settings.local.json.example    # Local settings template
├── .claude-plugin/                    # The skill itself
│   ├── SKILL.md                      # Skill definition
│   ├── scripts/                      # Python utilities
│   │   ├── skill_utils.py           # Shared utilities
│   │   ├── validate_skill.py        # Validator
│   │   └── package_skill.py         # Packager
│   └── references/                   # Documentation
│       ├── skill-specification.md    # Technical spec
│       ├── platform-differences.md   # Platform guide
│       └── skill-examples.md         # Examples
├── LICENSE                           # MIT License
├── README.md                         # This file
├── CONTRIBUTING.md                   # Contribution guide
└── CLAUDE.md                         # Project context
```

## Examples

### Creating a Simple Skill

```
User: Create a skill that helps format commit messages according to Conventional Commits

Claude: I'll create a commit-formatter skill. Let me ask a few questions:

1. Should it validate existing commits or generate new ones?
2. Do you want it to enforce specific scopes or types?
3. Should it integrate with git commands?

[After answering questions, Claude generates the complete skill]

✅ Created .claude/skills/commit-formatter/
  - SKILL.md (with proper frontmatter and instructions)
  - Validated successfully
```

### Creating a Complex Skill with Scripts

```
User: Create a database migration skill that validates SQL, checks for breaking changes, and generates rollback scripts

Claude: I'll create a comprehensive database migration skill with Python utilities...

[Claude generates SKILL.md, validation scripts, and reference documentation]

✅ Created .claude-plugin/db-migrator/
  - SKILL.md
  - scripts/validate_migration.py
  - scripts/generate_rollback.py
  - references/sql-best-practices.md
```

## Requirements

- **Python 3.8+** - For validation and packaging scripts
- **PyYAML** - For parsing YAML frontmatter (`pip install pyyaml`)
- **Claude Code, Claude.ai, or Claude API** - To use the skill

## Platform-Specific Guidance

### Claude.ai
- Skills are user-specific (not shared across workspace)
- Network access depends on user/admin settings
- Upload skills through the Skills management UI

### Claude API
- Skills are workspace-wide accessible
- No network access by default
- No dynamic package installation
- Integrate via API configuration

### Claude Code
- Supports both project and user-level skills
- Full network access available
- Best for development and testing
- Use `.claude/agents/` for project-specific skills

## Skill Requirements

All skills must have:

### Required YAML Frontmatter
```yaml
---
name: your-skill-name          # lowercase, hyphens, max 64 chars
description: What it does and when to use it  # max 1024 chars
---
```

### Naming Rules
- Lowercase letters, numbers, and hyphens only
- Maximum 64 characters
- Cannot contain "anthropic" or "claude"
- No XML tags

### Description Guidelines
- Non-empty, maximum 1024 characters
- Explain WHAT the skill does
- Explain WHEN to use it
- Use action-oriented language for auto-invocation
- No XML tags

## Development

### Setup Development Environment

```bash
# Clone the repository
git clone https://github.com/jgardner04/claude-skills-skill.git
cd claude-skills-skill

# Install dependencies
pip install pyyaml

# Copy local settings template
cp .claude/settings.local.json.example .claude/settings.local.json

# Run validation tests
python .claude-plugin/scripts/validate_skill.py .claude-plugin/
```

### Using the Python Development Agent

All Python code should be written using the `python-dev` agent:

```
Use the python-dev agent to add a new validation rule
```

The agent ensures:
- PEP 8 compliance
- Comprehensive type hints
- Detailed docstrings
- Security best practices
- Robust error handling

## Testing

### Manual Testing
```bash
# Test skill creation
# (Ask Claude to create a test skill)

# Validate the generated skill
python .claude-plugin/scripts/validate_skill.py path/to/test-skill/

# Package the skill
python .claude-plugin/scripts/package_skill.py path/to/test-skill/
```

### Validation Tests
- ✅ Valid skills pass validation
- ✅ Invalid names are rejected
- ✅ Invalid descriptions are rejected
- ✅ Malformed YAML is detected
- ✅ Missing required fields are caught

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Code of conduct
- Development workflow
- Coding standards
- Pull request process
- Testing requirements

## Security

This project takes security seriously:

- **Input validation** - All user inputs are validated
- **Path safety** - Prevents path traversal attacks
- **No code execution** - Never uses eval() or exec()
- **Secure defaults** - Fails closed, validates before processing

Report security vulnerabilities to: security@example.com

## Resources

- **Claude Skills Documentation**: https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview
- **Skills Blog Post**: https://claude.com/blog/skills
- **Engineering Deep Dive**: https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- **Skills Cookbook**: https://github.com/anthropics/claude-cookbooks/tree/main/skills

## License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## Roadmap

- [ ] Add automated testing framework
- [ ] Create skill template library
- [ ] Add skill versioning support
- [ ] Build skill marketplace integration
- [ ] Add skill analytics and metrics
- [ ] Create interactive skill designer UI

## FAQ

### How is this different from the official skill-creator?

This is an independent implementation that focuses on:
- Distribution as a plugin
- Standalone CLI tools
- Comprehensive validation
- Cross-platform packaging

### Can I use this to create private skills?

Yes! Skills can be project-specific (.claude/skills/) or user-specific (~/.claude/agents/). They don't need to be published.

### Does this work with the Claude API?

Yes, the skill works across all Claude surfaces. The generated skills are compatible with Claude.ai, Claude API, and Claude Code.

### How do I update an existing skill?

Simply ask Claude to modify the skill, and it will update the appropriate files while maintaining validation.

## Support

- **Issues**: https://github.com/jgardner04/claude-skills-skill/issues
- **Discussions**: https://github.com/jgardner04/claude-skills-skill/discussions
- **Documentation**: See CLAUDE.md for detailed project context

## Acknowledgments

- Built on the excellent Claude Skills framework by Anthropic
- Inspired by the official skills cookbook examples
- Community contributions and feedback

---

**Made with ❤️ for the Claude community**
