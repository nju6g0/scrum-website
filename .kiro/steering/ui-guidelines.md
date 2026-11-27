---
inclusion: fileMatch
fileMatchPattern:
  [
    "src/components/**/*.tsx",
    "src/features/**/*.tsx",
    "src/app/**/*.tsx",
    "src/app/**/*.css",
  ]
---

# UI Implementation Guidelines

## Design Source

Figma is the source of truth for UI implementation.

## Visual Accuracy

- Follow the original layout and hierarchy.
- Match spacing, typography, colors and dimensions.
- Reuse extracted design tokens.
- Do not approximate values when exact design information is available.
- Do not invent missing visual details.

## Responsive Design

- Implement responsive behavior based on available design references.
- Use mobile-first responsive styles where appropriate.
- Avoid fixed widths that cause overflow.
- Preserve visual hierarchy across screen sizes.

## Components

- Build reusable UI components.
- Keep feature-specific UI inside its feature directory.
- Avoid premature abstraction.
- Keep component APIs simple and typed.

## Interactions

- Buttons must have meaningful actions.
- Inputs must support appropriate state changes.
- Dialogs and menus must support open and close behavior.
- Provide hover, focus, active and disabled states where appropriate.

## Assets

- Prefer original Figma assets.
- Do not replace supplied icons or images without a reason.
- Avoid emoji as substitutes for designed icons.

## Visual QA

- Compare the browser output with Figma.
- Check alignment, spacing, typography and dimensions.
- Verify responsive behavior.
- Fix visual differences without changing unrelated functionality.
