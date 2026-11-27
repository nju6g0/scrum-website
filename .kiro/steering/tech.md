---
inclusion: always
---

# Technology Stack

## Core

- Next.js (App Router)
- React
- TypeScript
- Tailwind CSS

## Development Rules

- Use TypeScript for all application code.
- Use functional React components.
- Use Next.js App Router.
- Prefer Server Components by default.
- Use Client Components only when interactivity is required.
- Use Tailwind CSS for styling.
- Avoid unnecessary external dependencies.
- Use semantic HTML.
- Ensure responsive layouts.

## Styling

- Follow the Figma design system.
- Extract reusable colors, spacing,
  typography and border radius into design tokens.
- Avoid arbitrary styling values when
  an existing design token can be reused.

## Quality

- Keep components small and reusable.
- Avoid using `any`.
- Handle loading and error states where applicable.
- Ensure TypeScript has no errors.

## React Compiler

- React Compiler is enabled.
- Prefer compiler-managed memoization.
- Avoid unnecessary useMemo and useCallback.
- Do not add React.memo without a specific reason.
- Follow React Rules and keep components pure.
- Do not rely on memoization for correctness.
