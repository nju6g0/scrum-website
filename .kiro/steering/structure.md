---
inclusion: always
---

# Project Structure

Use the following structure:

src/
app/
layout.tsx
page.tsx
globals.css

components/
ui/
layout/
features/

hooks/

lib/

types/

constants/

## Rules

- app/: Next.js routes and layouts.
- components/ui/: Reusable basic UI components.
- components/layout/: Header, Footer, Navigation.
- components/features/: Business-related components.
- hooks/: Custom React hooks.
- lib/: Utilities and shared logic.
- types/: Shared TypeScript definitions.
- constants/: Shared constants.

## Naming

- React components: PascalCase
- Hooks: camelCase with use prefix
- Utilities: camelCase
- Types and interfaces: PascalCase
