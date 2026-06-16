# Contributing to PhoneShop Pro Edition

Thank you for your interest in contributing to PhoneShop Pro Edition! This document provides guidelines and instructions for contributing to the project.

## 🤝 Code of Conduct

Please be respectful and inclusive in all interactions. We're committed to providing a welcoming environment for all contributors.

## 📋 How to Contribute

### 1. Reporting Bugs

If you find a bug, please create an issue with the following information:

- **Title**: Clear, concise description of the bug
- **Description**: Detailed explanation of what went wrong
- **Steps to Reproduce**: Step-by-step instructions to reproduce the issue
- **Expected Behavior**: What should happen
- **Actual Behavior**: What actually happened
- **Environment**: OS, browser, Node.js version, etc.
- **Screenshots**: If applicable

### 2. Suggesting Features

We welcome feature suggestions! Please:

- Check existing issues to avoid duplicates
- Provide a clear title and description
- Explain the use case and benefits
- Include mockups or examples if applicable

### 3. Submitting Code Changes

#### Getting Started

1. **Fork the repository**
   ```bash
   git clone https://github.com/jsadala35-ops/phoneshop-tanzania.git
   cd phoneshop-tanzania
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Follow the code style guidelines
   - Write clear commit messages
   - Add tests for new functionality

4. **Test your changes**
   ```bash
   npm test
   npm run lint
   ```

5. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create a Pull Request**
   - Use a clear title and description
   - Link related issues
   - Include screenshots if UI changes

#### Pull Request Guidelines

- **Title Format**: `[type]: Brief description`
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
  - Example: `feat: Add customer loyalty program module`

- **Description**: Include:
  - What changes were made
  - Why they were made
  - Any breaking changes
  - Testing notes

- **Commits**: Use clear, meaningful commit messages
  ```
  feat: Add customer loyalty points system
  
  - Implement points calculation logic
  - Add points display in customer profile
  - Create admin interface for points management
  ```

## 📐 Code Style Guidelines

### JavaScript/React

- Use **ES6+ features** (arrow functions, destructuring, etc.)
- Use **meaningful variable names**
- Keep functions **small and focused**
- Use **PropTypes or TypeScript** for type checking
- Write **JSDoc comments** for complex functions

### Example:

```javascript
/**
 * Calculate customer discount based on loyalty points
 * @param {number} points - Customer loyalty points
 * @param {number} purchaseAmount - Total purchase amount
 * @returns {number} Discount amount
 */
const calculateDiscount = (points, purchaseAmount) => {
  const discountPercentage = Math.min(points / 100, 0.2); // Max 20% discount
  return purchaseAmount * discountPercentage;
};
```

### CSS/Styling

- Use **BEM naming convention** for CSS classes
- Use **CSS variables** for theming
- Keep **mobile-first approach**
- Maintain **consistent spacing** and naming

### Example:

```css
.card {
  background: var(--color-white);
  border-radius: var(--radius-md);
  padding: var(--spacing-md);
}

.card__header {
  margin-bottom: var(--spacing-sm);
  font-weight: bold;
}

.card__content {
  color: var(--color-text-secondary);
}
```

## 🧪 Testing

- Write **unit tests** for utilities
- Write **component tests** for React components
- Aim for **80%+ code coverage**
- Test **edge cases** and **error scenarios**

```bash
# Run tests
npm test

# Run tests with coverage
npm test -- --coverage

# Run specific test file
npm test -- inventory.test.js
```

## 📚 Documentation

- Update **README.md** if adding features
- Add **JSDoc comments** for functions
- Update **API documentation** for API changes
- Create **user guides** for complex features

## 🔄 Development Workflow

1. **Create issue** → Discuss and plan
2. **Create branch** → Start development
3. **Make commits** → Regular, meaningful commits
4. **Open PR** → Request review
5. **Address feedback** → Iterate on feedback
6. **Merge** → Celebrate! 🎉

## 📦 Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types:
- **feat**: New feature
- **fix**: Bug fix
- **docs**: Documentation only
- **style**: Code style changes
- **refactor**: Code refactoring
- **perf**: Performance improvements
- **test**: Test additions/changes
- **chore**: Build process, dependencies

### Examples:

```
feat(inventory): Add IMEI validation

- Validate IMEI format on input
- Store IMEI in inventory system
- Display IMEI in product listings

Closes #123
```

```
fix(dashboard): Fix revenue calculation

The monthly revenue was calculating incorrectly for
invoices spanning multiple months.

Closes #456
```

## 🚀 Release Process

- Versions follow **Semantic Versioning** (MAJOR.MINOR.PATCH)
- Release notes are created for each version
- Changes are merged to `main` branch
- Tags are created for releases

## ❓ Questions?

- Open a **GitHub Discussion**
- Email: jsadala35@gmail.com
- Phone: +255 673 409 790

## 📝 License

By contributing, you agree that your contributions will be licensed under the project's license.

---

**Thank you for contributing to PhoneShop Pro Edition!** 🙏
