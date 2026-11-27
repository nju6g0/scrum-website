---
inclusion: always
---

# Project Architecture

Use a feature-oriented component structure.

## Directory Structure

src/
app/
components/
ui/
layout/
features/
data/
hooks/
lib/
types/
constants/

public/
images/
icons/

## Responsibilities

### app/

Next.js routes, layouts and global styles.

### components/ui/

Reusable primitive components such as buttons, inputs and dialogs.

### components/layout/

Shared layout components such as header, navigation and footer.

### features/

Feature-specific components, state and business logic.

### data/

Mock data and local data definitions.

### hooks/

Reusable custom React hooks.

### lib/

Shared utility functions.

### types/

Shared TypeScript types and interfaces.

### constants/

Application constants and configuration.

## Architecture Rules

- Keep page.tsx focused on page composition.
- Move reusable UI into components.
- Keep feature-specific code inside its feature directory.
- Keep mock data separate from presentation components.
- Avoid oversized components.
- Avoid circular dependencies.
- Do not create abstractions without a clear reuse requirement.

## Naming

- Components: PascalCase
- Hooks: camelCase with use prefix
- Variables: camelCase
- Types: PascalCase
- Constants: UPPER_SNAKE_CASE
