# Contributing to MoiraWeave

Thank you for your interest in contributing to MoiraWeave! We welcome contributions from the community. This guide will help you understand how to contribute effectively.

## Code of Conduct

Please review our [Code of Conduct](CODE_OF_CONDUCT.md) before contributing. We are committed to providing a welcoming and inclusive environment for all contributors.

## How to Contribute

### Reporting Bugs

If you encounter a bug, please:

1. **Check existing issues** to avoid duplicates
2. **Create a new issue** with:
   - Clear, descriptive title
   - Detailed description of the bug
   - Steps to reproduce
   - Expected vs. actual behavior
   - Environment details (OS, Python version, etc.)
   - Code snippets or screenshots if applicable

### Suggesting Features

To suggest a feature:

1. **Check open issues** to see if it's already been proposed
2. **Create a new issue** with:
   - Clear, descriptive title
   - Detailed description of the feature
   - Use cases and benefits
   - Possible implementation approach (optional)

### Pull Requests

We follow a structured PR workflow:

1. **Fork the repository** and create a feature branch
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** following our coding standards:
   - Write clear, descriptive commit messages
   - Include tests for new functionality
   - Update documentation as needed
   - Follow the project's code style

3. **Test your changes**:
   ```bash
   uv run pytest
   uv run mypy
   uv run ruff check .
   ```

4. **Push to your fork** and create a pull request
   - Link related issues in the PR description
   - Provide a clear summary of changes
   - Include any breaking changes

5. **Address review feedback**
   - We may request changes or clarifications
   - Update your PR as needed
   - Mark conversations as resolved once addressed

## Development Setup

### Prerequisites

- Python 3.13+
- `uv` package manager
- Docker and Docker Compose (for local testing)

### Setup Local Environment

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/moiraweave-REPO.git
cd moiraweave-REPO

# Create virtual environment
uv venv

# Install dependencies
uv sync
```

### Running Tests

```bash
# Run all tests
uv run pytest

# Run specific test file
uv run pytest tests/test_file.py

# Run with coverage
uv run pytest --cov=src
```

### Code Quality

```bash
# Type checking
uv run mypy src

# Linting
uv run ruff check src

# Format code
uv run ruff format src
```

## Commit Message Guidelines

Use clear, descriptive commit messages following conventional commits:

```
type(scope): brief description

Longer explanation if necessary.

Fixes #issue_number
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`

Examples:
- `feat(cli): add project init command`
- `fix(core): resolve race condition in scheduler`
- `docs: update quickstart guide`

## Documentation

- Update relevant documentation when making changes
- Include docstrings for public functions and classes
- Update README if adding new features or changing behavior
- Follow the documentation style of the project

## Security

If you discover a security vulnerability, please email [security@moiraweave.dev](mailto:security@moiraweave.dev) instead of using the issue tracker. See our [Security Policy](SECURITY.md) for details.

## Questions?

- Join our community discussions
- Check the [documentation](https://docs.moiraweave.dev)
- Review existing issues and PRs

Thank you for contributing to MoiraWeave! 🚀
