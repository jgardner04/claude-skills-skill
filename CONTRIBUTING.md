# Contributing to Claude Skills Skill

Thank you for your interest in contributing! This document provides guidelines and instructions for contributing to the project.

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive experience for everyone. We pledge to make participation in our project harassment-free for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

### Our Standards

**Positive behaviors include:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Unacceptable behaviors include:**
- Harassment, trolling, or insulting/derogatory comments
- Public or private harassment
- Publishing others' private information without permission
- Other conduct which could reasonably be considered inappropriate

## How to Contribute

### Reporting Issues

Before creating an issue, please:
1. Check if the issue already exists
2. Verify you're using the latest version
3. Test with the validation script if relevant

When creating an issue, include:
- Clear, descriptive title
- Steps to reproduce (for bugs)
- Expected vs actual behavior
- Environment details (OS, Python version, Claude surface)
- Relevant logs or error messages

### Suggesting Enhancements

Enhancement suggestions are welcome! Please include:
- Clear description of the enhancement
- Use cases and benefits
- Potential implementation approach
- Any relevant examples or mockups

### Pull Requests

We love pull requests! Here's the process:

1. **Fork and Clone**
   ```bash
   git clone https://github.com/YOUR-USERNAME/claude-skills-skill.git
   cd claude-skills-skill
   ```

2. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

3. **Set Up Development Environment**
   ```bash
   # Install dependencies
   pip install pyyaml

   # Copy local settings template
   cp .claude/settings.local.json.example .claude/settings.local.json
   ```

4. **Make Your Changes**
   - Follow the coding standards (see below)
   - Write clear commit messages
   - Add tests if applicable
   - Update documentation as needed

5. **Test Your Changes**
   ```bash
   # Validate the skill itself
   python .claude-plugin/scripts/validate_skill.py .claude-plugin/

   # Test your changes manually
   # (create a test skill, validate it, package it)
   ```

6. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "feat: add new validation rule for X"
   ```

7. **Push and Create PR**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then create a pull request on GitHub.

## Development Guidelines

### Python Code Standards

All Python code must:

#### Follow PEP 8
- Use 4 spaces for indentation
- Max line length: 88 characters (Black formatter)
- Two blank lines between top-level definitions
- Use descriptive variable names (snake_case)

#### Include Type Hints
```python
from pathlib import Path
from typing import Dict, List, Optional, Tuple

def validate_skill(
    skill_path: Path,
    strict: bool = False
) -> Tuple[bool, str]:
    """Validate a skill file.

    Args:
        skill_path: Path to skill directory
        strict: Enable strict validation

    Returns:
        Tuple of (is_valid, error_message)
    """
    pass
```

#### Write Docstrings
Use Google-style docstrings for all public functions and classes:

```python
def parse_skill(content: str) -> Dict[str, Any]:
    """Parse skill file into frontmatter and body.

    Args:
        content: Full content of SKILL.md file

    Returns:
        Dictionary containing parsed frontmatter and body

    Raises:
        SkillValidationError: If file format is invalid

    Examples:
        >>> content = "---\\nname: test\\n---\\nBody"
        >>> result = parse_skill(content)
        >>> result['name']
        'test'
    """
    pass
```

#### Handle Errors Properly
```python
class SkillValidationError(Exception):
    """Raised when skill validation fails."""
    pass

def validate_name(name: str) -> None:
    """Validate skill name.

    Raises:
        SkillValidationError: If name is invalid
    """
    if not name:
        raise SkillValidationError("Skill name is required")
```

#### Ensure Security
- Validate all user inputs
- Prevent path traversal attacks
- Never use eval() or exec()
- Use pathlib.Path for file operations
- Sanitize data before processing

```python
def safe_path(base: Path, user_input: str) -> Path:
    """Safely resolve path, preventing traversal."""
    resolved = (base / user_input).resolve()
    if not resolved.is_relative_to(base):
        raise ValueError(f"Path traversal detected: {user_input}")
    return resolved
```

### Markdown Documentation Standards

#### Skill Documentation (SKILL.md)
- Start with YAML frontmatter
- Use clear heading hierarchy
- Include concrete examples
- Provide "When to Use" section
- Keep token-efficient (main instructions only)

#### Reference Documentation
- Can be comprehensive and detailed
- Include code examples with syntax highlighting
- Use tables for structured information
- Link to related resources
- Keep sections focused

### Git Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

**Format**:
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Code style changes
- `refactor`: Code refactoring
- `perf`: Performance improvement
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples**:
```
feat(validator): add check for description length

fix(packaging): handle missing scripts directory

docs(readme): add installation instructions

refactor(utils): simplify path validation logic
```

### Testing Requirements

#### Manual Testing Checklist
- [ ] Validate the skill-creator skill itself
- [ ] Create a test skill using the skill
- [ ] Validate the test skill
- [ ] Package the test skill
- [ ] Test on multiple platforms if possible

#### For Python Scripts
- [ ] Test with valid inputs
- [ ] Test with invalid inputs
- [ ] Test error handling
- [ ] Test edge cases
- [ ] Verify error messages are clear

#### For SKILL.md Changes
- [ ] Validate against spec
- [ ] Check examples are accurate
- [ ] Ensure instructions are clear
- [ ] Test that skill is invoked properly

### Documentation Updates

When making changes, update:

- **README.md**: If adding features or changing usage
- **CLAUDE.md**: If changing project structure or workflow
- **SKILL.md**: If changing skill behavior
- **References**: If adding new concepts or patterns

## Project Structure

```
claude-skills-skill/
├── .claude/                    # Claude Code configuration
│   ├── agents/                 # Custom agents
│   └── settings.json           # Project settings
├── .claude-plugin/             # The skill itself
│   ├── SKILL.md               # Skill definition
│   ├── scripts/               # Python utilities
│   └── references/            # Reference docs
├── .gitignore
├── LICENSE
├── README.md
├── CONTRIBUTING.md            # This file
└── CLAUDE.md                  # Project context
```

## Using the Python Development Agent

All Python code should be written using the `python-dev` agent:

```
Use the python-dev agent to implement the new validation rule
```

This ensures:
- PEP 8 compliance
- Comprehensive type hints
- Detailed docstrings
- Security best practices
- Robust error handling

## Review Process

### What We Look For

- **Code Quality**: Follows standards, well-documented
- **Functionality**: Works as intended, handles edge cases
- **Tests**: Includes appropriate testing
- **Documentation**: Clear and accurate
- **Security**: No vulnerabilities introduced

### Review Timeline

- Initial review: Within 3-5 days
- Feedback provided with requested changes
- Follow-up review: Within 2-3 days after updates
- Merge when approved by at least one maintainer

### After Your PR is Merged

- Your contribution will be acknowledged in release notes
- The change will be included in the next release
- You're welcome to contribute more!

## Getting Help

- **Questions**: Open a discussion on GitHub
- **Bugs**: Open an issue with details
- **Security**: Email security@example.com (do not open public issue)
- **Chat**: Join our community (link TBD)

## Recognition

Contributors are recognized in:
- README.md acknowledgments section
- Release notes
- Project documentation

Thank you for contributing to making Claude skills easier to create!

## Resources

- **Claude Skills Docs**: https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview
- **Python Style Guide**: https://pep8.org/
- **Conventional Commits**: https://www.conventionalcommits.org/
- **Type Hints Guide**: https://docs.python.org/3/library/typing.html

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
