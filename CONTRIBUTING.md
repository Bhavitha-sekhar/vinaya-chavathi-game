# Contributing to Modak Maker Challenge

Thank you for your interest in contributing! We welcome contributions of all kinds, from bug reports to feature additions.

## How to Contribute

### Reporting Issues
- Check if the issue already exists before reporting
- Provide clear description of the bug
- Include steps to reproduce
- Mention your browser/device and OS

### Feature Requests
- Describe the feature clearly
- Explain why it would be useful
- Provide examples if applicable

### Code Contributions

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Follow the existing code style
   - Add comments for complex logic
   - Update documentation as needed

4. **Test your changes**
   ```bash
   npm test
   ```

5. **Commit with clear messages**
   ```bash
   git commit -m "feat: add new feature description"
   ```

6. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

7. **Create a Pull Request**
   - Provide a clear description
   - Link related issues
   - Follow the PR template

## Code Style Guidelines

- Use ES6+ syntax
- Use meaningful variable and function names
- Add comments for non-obvious code
- Keep functions small and focused
- Follow the existing project structure

## Commit Message Format

```
type(scope): description

[optional body]

[optional footer]
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Test updates
- `chore`: Build/tooling

Example:
```
feat(gameplay): add combo multiplier system

Implement a combo system that multiplies score when consecutive matches are made.
```

## Testing

- Write tests for new features
- Ensure existing tests pass
- Test on multiple devices/browsers

## Questions?

Feel free to ask by opening an issue or starting a discussion!

## License

By contributing, you agree your contributions will be licensed under the MIT License.

Happy coding! 🎮✨
