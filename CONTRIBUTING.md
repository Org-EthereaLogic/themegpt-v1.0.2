# Contributing to ThemeGPT

Thank you for your interest in contributing to ThemeGPT! We welcome contributions from everyone, whether you're fixing a bug, adding a new theme, or improving documentation.

## Table of Contents

- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Features](#suggesting-features)
  - [Submitting Themes](#submitting-themes)
  - [Pull Requests](#pull-requests)
- [Development Guidelines](#development-guidelines)
- [Code of Conduct](#code-of-conduct)

## Getting Started

1. Fork the repository
2. Clone your fork locally:
   ```bash
   git clone https://github.com/your-username/themegpt.git
   ```
3. Load the extension in Chrome:
   - Navigate to `chrome://extensions/`
   - Enable Developer mode
   - Click "Load unpacked" and select the project directory

## How to Contribute

### Reporting Bugs

Found a bug? Please help us fix it by opening an issue with the following information:

- **Description** — Clear description of the bug
- **Steps to reproduce** — How can we recreate the issue?
- **Expected behavior** — What should happen?
- **Actual behavior** — What actually happens?
- **Environment** — Browser version, OS, ChatGPT subscription type
- **Screenshots** — If applicable, add screenshots to help explain the problem

### Suggesting Features

Have an idea to make ThemeGPT better? We'd love to hear it!

1. Check existing issues to see if it's already been suggested
2. Open a new issue with the "Feature Request" label
3. Describe the feature and why it would be useful
4. Include mockups or examples if possible

### Submitting Themes

Want to create a new theme? Here's how:

1. Study the existing themes in `themes.css`
2. Create your theme following the established CSS variable pattern
3. Test your theme thoroughly on ChatGPT
4. Submit a pull request with:
   - Your theme CSS
   - A brief description of the theme
   - Screenshot(s) showing the theme in action

**Theme Guidelines:**
- Ensure sufficient contrast for readability
- Test with both light and dark system preferences
- Keep the theme focused and cohesive
- Avoid overly bright or distracting colors

### Pull Requests

1. Create a new branch for your changes:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes and test thoroughly

3. Commit with clear, descriptive messages:
   ```bash
   git commit -m "Add: description of what you added"
   git commit -m "Fix: description of what you fixed"
   ```

4. Push to your fork and open a pull request

5. Fill out the PR template with:
   - What changes you made
   - Why you made them
   - How you tested them

## Development Guidelines

- **Keep it simple** — ThemeGPT values simplicity and lightweight code
- **Test thoroughly** — Test on multiple ChatGPT pages and subscription types
- **No tracking** — Never add analytics, tracking, or data collection
- **Respect privacy** — The extension should only do what's necessary for theming
- **Comment when needed** — Add comments for complex logic, but don't over-document

## Code of Conduct

We are committed to providing a welcoming and inclusive environment. Please:

- Be respectful and considerate in all interactions
- Welcome newcomers and help them get started
- Focus on constructive feedback
- Accept responsibility for mistakes and learn from them

Harassment, discrimination, or disrespectful behavior will not be tolerated.

---

Thank you for helping make ThemeGPT better!
