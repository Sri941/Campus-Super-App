# Contributing to Campus Super-App

We appreciate your interest in contributing to the Campus Super-App project! This document provides guidelines and information for contributors.

## Table of Contents
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Code Guidelines](#code-guidelines)
- [Pull Request Process](#pull-request-process)
- [Issue Reporting](#issue-reporting)
- [Code Review Process](#code-review-process)

## Getting Started

### Prerequisites
Before contributing, ensure you have:
- Node.js >= 16.0.0
- PostgreSQL >= 13
- Redis >= 6.0
- Git
- Docker (recommended)

### Development Environment Setup

1. **Fork the repository**
   ```bash
   git clone https://github.com/yourusername/campus-super-app.git
   cd campus-super-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   cd frontend && npm install
   cd ../backend && npm install
   ```

3. **Environment configuration**
   ```bash
   cp .env.example .env.local
   # Fill in your configuration values
   ```

4. **Database setup**
   ```bash
   cd backend
   npx prisma migrate dev
   npm run db:seed
   ```

5. **Start development servers**
   ```bash
   npm run dev
   ```

## Code Guidelines

### Code Style
- Use TypeScript for all new code
- Follow ESLint and Prettier configurations
- Use meaningful variable and function names
- Add JSDoc comments for public APIs
- Maintain consistent indentation (2 spaces)

### Commit Messages
Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(delivery): add real-time order tracking
fix(auth): resolve JWT token expiration issue
docs(api): update authentication endpoints
```

### Code Structure

#### Frontend (React/Next.js)
```
frontend/
├── components/
│   ├── common/          # Reusable components
│   ├── modules/         # Module-specific components
│   └── ui/              # UI primitives
├── pages/
│   ├── api/             # API routes
│   └── [module]/        # Module pages
├── hooks/               # Custom React hooks
├── utils/               # Utility functions
├── stores/              # State management (Zustand)
└── types/               # TypeScript type definitions
```

#### Backend (Node.js/Express)
```
backend/
├── src/
│   ├── controllers/     # Request handlers
│   ├── services/        # Business logic
│   ├── models/          # Database models
│   ├── middleware/      # Express middleware
│   ├── routes/          # API route definitions
│   ├── utils/           # Utility functions
│   └── types/           # TypeScript types
├── prisma/              # Database schema and migrations
└── tests/               # Test files
```

### Testing Requirements

All contributions should include appropriate tests:

#### Frontend Testing
```bash
cd frontend
npm run test              # Run unit tests
npm run test:coverage     # Generate coverage report
```

#### Backend Testing
```bash
cd backend
npm run test              # Run unit tests
npm run test:e2e          # Run integration tests
npm run test:coverage     # Generate coverage report
```

**Testing Guidelines:**
- Write unit tests for utility functions
- Add integration tests for API endpoints
- Include component tests for React components
- Maintain minimum 80% code coverage
- Use meaningful test descriptions

## Pull Request Process

### Before Creating a PR

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**
   - Follow code guidelines
   - Add tests for new functionality
   - Update documentation as needed

3. **Run quality checks**
   ```bash
   npm run lint              # Check code style
   npm run type-check        # TypeScript validation
   npm test                  # Run all tests
   npm run build             # Ensure build succeeds
   ```

### Creating a Pull Request

1. **Push your branch**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create PR on GitHub**
   - Use a clear, descriptive title
   - Reference related issues (#123)
   - Fill out the PR template completely

3. **PR Title Format**
   ```
   [Module] Brief description of changes
   
   Examples:
   [Delivery] Add real-time order tracking
   [Auth] Fix JWT token refresh mechanism
   [UI] Improve mobile responsiveness
   ```

### PR Template

Your PR description should include:

```markdown
## Summary
Brief description of changes made.

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Screenshots (if applicable)
Add screenshots for UI changes.

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added to complex code
- [ ] Documentation updated
- [ ] Tests added/updated
```

## Issue Reporting

### Bug Reports

Use the bug report template:

```markdown
**Describe the bug**
Clear description of the issue.

**Steps to Reproduce**
1. Step one
2. Step two
3. Step three

**Expected Behavior**
What should happen.

**Actual Behavior**
What actually happens.

**Environment**
- OS: [e.g., macOS 12.0]
- Browser: [e.g., Chrome 95.0]
- Node.js version: [e.g., 16.14.0]

**Screenshots**
Add screenshots if applicable.

**Additional Context**
Any other relevant information.
```

### Feature Requests

Use the feature request template:

```markdown
**Feature Description**
Clear description of the proposed feature.

**Problem Statement**
What problem does this solve?

**Proposed Solution**
How should this feature work?

**Alternatives Considered**
Other approaches you've considered.

**Additional Context**
Any other relevant information.
```

## Code Review Process

### Review Guidelines

**For Reviewers:**
- Check code quality and adherence to guidelines
- Verify functionality through testing
- Provide constructive feedback
- Approve when satisfied with changes

**For Contributors:**
- Respond to feedback promptly
- Make requested changes
- Re-request review after updates
- Be open to suggestions and improvements

### Review Criteria

Code reviews should verify:
- **Functionality**: Code works as intended
- **Quality**: Follows coding standards
- **Performance**: No significant performance regressions
- **Security**: No security vulnerabilities introduced
- **Testing**: Adequate test coverage
- **Documentation**: Updated where necessary

## Development Workflow

### Branch Strategy
- `main`: Production-ready code
- `develop`: Integration branch for features
- `feature/*`: New features
- `fix/*`: Bug fixes
- `hotfix/*`: Critical production fixes

### Release Process
1. Features merged to `develop`
2. Testing and quality assurance
3. Release candidate created
4. Merge to `main` after approval
5. Tag release version
6. Deploy to production

## Module-Specific Guidelines

### Delivery System
- Use real-time updates for order tracking
- Implement proper error handling for payment failures
- Follow geolocation best practices

### CodeQuest Platform
- Ensure AI responses are helpful and accurate
- Implement proper code execution sandboxing
- Add comprehensive test cases for problems

### E-Library
- Handle file uploads securely
- Implement proper search indexing
- Ensure copyright compliance

### Event Management
- Validate event capacity and timing
- Implement QR code security measures
- Handle timezone considerations

## Getting Help

If you need help with contributions:

1. **Documentation**: Check existing docs first
2. **Issues**: Search existing issues
3. **Discussions**: Use GitHub Discussions
4. **Contact**: Reach out to maintainers

## Recognition

Contributors will be recognized in:
- README.md contributors section
- Release notes for significant contributions
- Hall of Fame for outstanding contributions

Thank you for contributing to Campus Super-App!