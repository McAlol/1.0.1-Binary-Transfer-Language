# Contributing to BTL (Binary Transfer Language)

Thank you for your interest in contributing to BTL! This project aims to create an open, interoperable meta-classification system for media across global registries.

## Table of Contents

- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Contributing Guidelines](#contributing-guidelines)
- [Code Style](#code-style)
- [Testing](#testing)
- [Documentation](#documentation)
- [Pull Request Process](#pull-request-process)
- [Communication](#communication)

---

## Getting Started

### Prerequisites

- **Node.js** v18+ (for TypeScript parser)
- **Python** 3.9+ (for Python parser)
- **Git** for version control
- Familiarity with:
  - International registry standards (ISBN, ISRC, EIDR, DOI)
  - Binary encoding systems
  - JSON Schema validation

### Quick Start

1. **Fork the repository**:
   ```bash
   git clone https://github.com/nwc/btl.git
   cd btl
   ```

2. **Install dependencies**:
   ```bash
   # TypeScript/Node
   npm install

   # Python
   pip install -r requirements.txt
   ```

3. **Run tests**:
   ```bash
   # TypeScript
   npm test

   # Python
   pytest
   ```

4. **Read the specification**:
   - Start with `README.md`
   - Review `spec/btl-v0.1.md` for technical details
   - Check `examples/` for usage patterns

---

## Development Setup

### TypeScript Environment

```bash
npm install
npm run build
npm test
npm run lint
```

### Python Environment

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
pytest
```

### Editor Configuration

Recommended VS Code extensions:
- **ESLint** (for TypeScript)
- **Pylint** (for Python)
- **Prettier** (code formatting)
- **JSON Schema Validator**

---

## Project Structure

```
btl/
├── spec/                # Specifications
│   ├── btl-v0.1.md      # Technical specification (RFC-style)
│   ├── art-id-spec.md   # ART-ID specification
│   └── btl-v0.1.schema.json  # JSON Schema
├── src/
│   ├── core/            # Core BTL logic
│   ├── parser/          # Parsers (TS, Python)
│   ├── registry/        # Registry integrations
│   │   ├── isbn/        # ISBN validation
│   │   ├── isrc/        # ISRC validation
│   │   └── art/         # ART-ID validation
│   ├── search/          # NWC search utilities
│   └── utils/           # Shared utilities
├── tests/               # Test suites
├── examples/            # Usage examples
└── docs/                # Additional documentation
```

---

## Contributing Guidelines

### What We're Looking For

✅ **Parser improvements** (TypeScript, Python, other languages)  
✅ **Registry integrations** (ISBN, ISRC, EIDR, ART-ID validators)  
✅ **Test coverage** (unit tests, integration tests)  
✅ **Documentation** (examples, guides, translations)  
✅ **Bug fixes** and **performance optimizations**  
✅ **NWC integration** work (Phase 2)

### What to Avoid

❌ Breaking changes to BTL v0.1 format without discussion  
❌ Adding dependencies without justification  
❌ Large PRs without prior discussion (open an issue first)  
❌ Modifying canonical gate order (this is fixed by design)

---

## Code Style

### TypeScript

- **Formatter**: Prettier
- **Linter**: ESLint
- **Style**: 
  - Use `const` over `let` where possible
  - Prefer functional style (map, filter, reduce)
  - Use explicit types (avoid `any`)

**Example**:
```typescript
export interface Gate {
  active: boolean;
  name: GateName;
  metadata?: Record<string, string>;
}

export function parseCanonicalBTL(btl: string): BTL {
  // Implementation
}
```

### Python

- **Formatter**: Black
- **Linter**: Pylint / Flake8
- **Style**:
  - PEP 8 compliance
  - Type hints for all public functions
  - Docstrings (Google style)

**Example**:
```python
from typing import Dict, Optional

class Gate:
    """Represents a BTL gate with optional metadata."""
    
    def __init__(self, active: bool, name: str, metadata: Optional[Dict[str, str]] = None):
        self.active = active
        self.name = name
        self.metadata = metadata or {}
```

---

## Testing

### Test Requirements

- **All new features** must include tests
- **Bug fixes** must include regression tests
- **Aim for 80%+ code coverage**

### TypeScript Testing

```bash
npm test                # Run all tests
npm run test:watch      # Watch mode
npm run test:coverage   # Coverage report
```

### Python Testing

```bash
pytest                     # Run all tests
pytest --cov=src          # Coverage report
pytest -k test_parse      # Run specific test
```

### Test Organization

```
tests/
├── parser/
│   ├── test_parse_ts.spec.ts
│   └── test_parse_py.py
├── registry/
│   ├── test_isbn.py
│   └── test_art_id.py
└── integration/
    └── test_btl_nwc.py
```

---

## Documentation

### Writing Documentation

- **Keep it concise** but complete
- **Use examples** wherever possible
- **Link to specifications** when referencing standards
- **Update README** if you change public API

### Documentation Types

| Type | Location | Purpose |
|------|----------|---------|
| Specification | `spec/btl-v0.1.md` | Technical RFC-style spec |
| API Docs | Inline comments | Public function documentation |
| Examples | `examples/` | Usage demonstrations |
| Guides | `docs/` | How-to guides, tutorials |

### Example Documentation

```typescript
/**
 * Parses a canonical BTL string into a structured BTL object.
 * 
 * @param btl - The canonical BTL string (e.g., "1(type=ISBN;9781234567890).0.0...")
 * @returns A BTL object with 10 gates
 * @throws {BTLParseError} If the string is malformed
 * 
 * @example
 * ```typescript
 * const parsed = parseCanonicalBTL("1(type=ISBN;9781234567890).0.0.0.0.0.0.0.1(type=ISO3166;US).0");
 * console.log(parsed.gates[0].active); // true
 * ```
 */
export function parseCanonicalBTL(btl: string): BTL {
  // Implementation
}
```

---

## Pull Request Process

### Before Submitting

1. **Open an issue** to discuss major changes
2. **Update documentation** if changing public API
3. **Add tests** for new functionality
4. **Run linter** and fix all warnings
5. **Update CHANGELOG** (if applicable)

### PR Template

```markdown
## Description
Brief description of changes

## Related Issue
Closes #123

## Changes Made
- Added X feature
- Fixed Y bug
- Updated Z documentation

## Testing
- [ ] Added unit tests
- [ ] All tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Documentation updated
- [ ] Tests added/updated
- [ ] CHANGELOG updated
```

### Review Process

1. Automated checks run (linting, tests, coverage)
2. Maintainer reviews code
3. Feedback provided (if needed)
4. Approval + merge

**Expected turnaround**: 3-7 days for initial review

---

## Communication

### Where to Ask Questions

- **GitHub Issues**: Bug reports, feature requests
- **GitHub Discussions**: General questions, ideas
- **Discord** (coming soon): Real-time chat
- **Email**: contact@nwcbtl.org

### Issue Labels

- `bug` - Something isn't working
- `enhancement` - New feature or request
- `documentation` - Documentation improvements
- `good first issue` - Good for newcomers
- `help wanted` - Extra attention needed
- `parser` - Parser-related
- `registry` - Registry integration work
- `nwc` - NWC-related (Phase 2)

---

## Versioning

BTL follows **semantic versioning** (semver):

- **Major** (1.0.0): Breaking changes to BTL format
- **Minor** (0.1.0): New features, backward compatible
- **Patch** (0.1.1): Bug fixes

**Current version**: v0.1 (BTL Foundation phase)

---

## Code of Conduct

### Our Standards

- **Be respectful** and inclusive
- **Be collaborative** and constructive
- **Focus on** what's best for the community
- **Show empathy** toward others

### Unacceptable Behavior

- Harassment, discrimination, or trolling
- Publishing others' private information
- Spam or off-topic content

**Enforcement**: Violations may result in temporary or permanent ban.

---

## Licensing

By contributing, you agree that your contributions will be licensed under the **MIT License** (or project license specified in `LICENSE` file).

All contributions must be your original work or properly attributed.

---

## Recognition

Contributors will be acknowledged in:
- `CONTRIBUTORS.md` file
- Release notes
- Project README

**Thank you for making BTL better!** 🎉

---

## Additional Resources

- **BTL Specification**: `spec/btl-v0.1.md`
- **ART-ID Specification**: `spec/art-id-spec.md`
- **JSON Schema**: `spec/btl-v0.1.schema.json`
- **Website**: https://www.nwcbtl.org
- **GitHub**: https://github.com/nwc/btl

---

**Questions?** Open an issue or contact us at contact@nwcbtl.org.
