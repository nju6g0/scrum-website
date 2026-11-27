---
inclusion: fileMatch
fileMatchPattern:
  [
    "**/*.test.ts",
    "**/*.test.tsx",
    "**/*.spec.ts",
    "**/*.spec.tsx",
    "playwright.config.ts",
  ]
---

# Testing Guidelines

## General

- Test user-visible behavior.
- Prefer testing outcomes over implementation details.
- Keep tests independent and deterministic.
- Use mock data instead of external services.

## Component Tests

- Test important interactions.
- Test loading, empty and disabled states when applicable.
- Test form validation where relevant.

## E2E Tests

- Verify critical user flows.
- Verify navigation and responsive behavior.
- Avoid dependencies on real backend services.

## Quality Gates

- Run ESLint.
- Run TypeScript checks.
- Run relevant tests.
- Run production build before completion.

## Completion

Report:

- Tests executed.
- Tests passed.
- Tests failed.
- Known limitations.
