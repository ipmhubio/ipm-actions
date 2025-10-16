# Contributing to IPM GitHub Actions

Thanks for your interest in improving these actions. We welcome contributions that make IPM easier to use in CI/CD workflows.

## How to Contribute

### Reporting Issues

Found a bug or have a suggestion? Open an issue with:
- Clear description of the problem or enhancement
- Steps to reproduce (for bugs)
- Expected vs actual behavior
- OS and GitHub runner information
- IPM version if relevant

### Submitting Changes

1. Fork the repository
2. Create a branch for your changes
3. Make your modifications
4. Test across all platforms (Windows, Linux, macOS)
5. Submit a pull request

We'll review PRs when we can and merge them if we see the benefits. IPMHub maintains full control over what gets merged and when.

## Testing Requirements

All contributions must pass the existing test workflow before being considered. The test workflow runs on all three platforms:

```yaml
runs-on: ${{ matrix.os }}
strategy:
  matrix:
    os: [ubuntu-latest, macos-latest, windows-latest]
```

### Running Tests Locally

You can trigger the test workflow manually to verify your changes:

1. Push your branch to your fork
2. Go to Actions tab in your fork
3. Select "Test IPM Composite Actions" workflow
4. Click "Run workflow"

### What Gets Tested

The test workflow validates:
- IPM setup and installation
- Workspace initialization
- Package synchronization
- Status checks
- Cross-platform compatibility

## Pull Request Guidelines

- Keep changes focused and atomic
- Include clear commit messages
- Reference related issues if applicable
- Ensure all tests pass
- Don't worry about code formatting (we'll handle it if needed)

## What We're Looking For

Contributions that:
- Fix bugs or issues
- Improve error handling
- Add useful functionality
- Enhance documentation
- Improve cross-platform compatibility

## Review Process

IPMHub reviews and merges contributions at our discretion. We appreciate all submissions but make final decisions based on:
- Alignment with project goals
- Code quality and maintainability
- Test coverage and platform compatibility
- Overall benefit to users

## Questions?

Not sure if your idea fits? Open an issue to discuss it before investing time in a PR.

## Code of Conduct

This project follows our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to uphold these standards.