---
inclusion: always
---

# Coding Standards

## React

- Use functional components.
- Prefer composition over complex conditional rendering.
- Use stable keys when rendering lists.
- Keep components focused on a single responsibility.
- Avoid unnecessary useEffect.

## TypeScript

- Avoid any and unnecessary type assertions.
- Define component props explicitly.
- Prefer type inference when types are obvious.
- Use discriminated unions when appropriate.

## Next.js

- Follow App Router conventions.
- Prefer Server Components by default.
- Add "use client" only when required.
- Do not access browser APIs in Server Components.

## Tailwind CSS

- Use utility classes consistently.
- Avoid inline styles unless necessary.
- Avoid duplicated class combinations.
- Follow the project's design tokens.

## Code Changes

- Inspect existing code before modifying it.
- Reuse existing components.
- Do not modify unrelated files.
- Do not introduce unnecessary dependencies.
- Explain significant architectural changes.

## Accessibility

- Use semantic HTML.
- Provide accessible labels.
- Support keyboard interaction.
- Maintain visible focus states.
- Use appropriate ARIA attributes when necessary.
