# Contributing to Resource Hacker Icon Replacer Action

Thank you for your interest in contributing! 🎉

## 📋 Code of Conduct

Please be respectful and constructive in all interactions.

## 🐛 Reporting Bugs

If you find a bug, please create an issue with:
- Clear description of the problem
- Steps to reproduce
- Expected vs actual behavior
- Your workflow file (if applicable)
- Relevant logs

## 💡 Suggesting Features

Feature suggestions are welcome! Please:
- Check if the feature has already been requested
- Clearly describe the use case
- Explain why it would be useful

## 🔧 Pull Requests

### Before Submitting

1. Fork the repository
2. Create a new branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test your changes thoroughly
5. Update documentation if needed

### PR Guidelines

- Keep changes focused and atomic
- Write clear commit messages
- Update CHANGELOG.md
- Ensure all tests pass
- Follow existing code style

### Testing

Before submitting a PR, please test your changes:

```yaml
# Test locally by creating a workflow in your fork
name: Test My Changes
on: workflow_dispatch

jobs:
  test:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ./
        with:
          exe-path: 'path/to/test.exe'
          icon-path: 'path/to/test.ico'
```

## 📝 Documentation

If you update functionality:
- Update README.md
- Update examples
- Add comments to complex code
- Update CHANGELOG.md

## ⚖️ Legal Notes

- Ensure your contribution doesn't include Resource Hacker executables
- All code must be compatible with MIT license
- Respect Resource Hacker's license terms

## 🙏 Thank You!

Every contribution helps make this project better!
