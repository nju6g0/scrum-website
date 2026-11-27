---
inclusion: always
---

# Technology Stack

## Core Technologies

- Next.js
- React
- TypeScript
- Tailwind CSS

## Framework

- Next.js App Router
- Use Server Components by default.
- Use Client Components only when browser-side interactivity or React state is required.

## TypeScript

- Enable strict type checking.
- Avoid any.
- Define explicit types for shared data structures.
- Prefer type-safe component props.

## Styling

- Use Tailwind CSS.
- Follow Figma design tokens.
- Avoid unnecessary arbitrary values.
- Keep responsive styles consistent.

## Data

- Use local mock data.
- Keep mock data separate from UI components.
- Use TypeScript types for mock data.
- Do not create API routes or backend services unless explicitly requested.

## State Management

- Prefer React useState and useReducer.
- Keep state close to the components that use it.
- Avoid unnecessary global state libraries.

## Dependencies

- Avoid unnecessary packages.
- Explain the purpose of new dependencies before installation.
- Prefer native Next.js and React features when appropriate.

## Quality Checks

- npm run lint
- npx tsc --noEmit
- npm run build

## React Compiler

- React Compiler is enabled.
- Prefer compiler-managed memoization.
- Avoid unnecessary useMemo and useCallback.
- Do not add React.memo without a specific reason.
- Follow React Rules and keep components pure.
- Do not rely on memoization for correctness.
