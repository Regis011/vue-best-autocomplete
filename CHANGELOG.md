# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.3.0] - 2025-11-27

### Added
- Comprehensive documentation structure organized in `docs/` folder
  - Complete API reference documentation (`docs/API.md`)
  - Detailed styling guide with 7+ customization examples (`docs/STYLING.md`)
  - Development guide for contributors (`docs/DEVELOPMENT.md`)
  - Documentation index (`docs/README.md`)
- Interactive demo application with three working examples:
  - City search with success state
  - Country search with validation and error state
  - Programming languages selection
- Support for modern Sass compiler (dart-sass)
- `npm run dev` script for easier local testing
- CHANGELOG.md for tracking version history

### Changed
- Reorganized README.md to be user-focused (removed development instructions)
- Development documentation moved from root to `docs/` folder
- Improved code formatting and ESLint compliance in demo app
- Updated package structure following npm best practices

### Fixed
- ARM64 (Apple Silicon) compatibility by replacing node-sass with sass
- Development server setup and configuration
- ESLint errors in demo application
- Peer dependency conflicts with `--legacy-peer-deps` workaround documented

### Removed
- node-sass dependency (replaced with modern sass)

## [0.2.4] - Previous Release

### Features
- Vue 3 autocomplete component
- Keyboard navigation support
- Visual states (success/error)
- ARIA accessibility attributes
- Real-time filtering
- Customizable styling

---

## How to Update This Changelog

### Types of Changes
- **Added** for new features
- **Changed** for changes in existing functionality
- **Deprecated** for soon-to-be removed features
- **Removed** for now removed features
- **Fixed** for any bug fixes
- **Security** in case of vulnerabilities

### Example Entry

```markdown
## [1.0.0] - 2025-12-01

### Added
- New prop `placeholder` for custom placeholder text
- Support for async data loading

### Fixed
- Selection bug when using keyboard navigation
- Memory leak in event listeners

### Changed
- Improved filtering algorithm performance
```
