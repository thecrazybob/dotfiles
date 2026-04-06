# Untitled UI Semantic Color Token Reference

**CRITICAL**: Never use raw Tailwind color classes (e.g. `text-gray-900`, `bg-blue-700`). Always use semantic tokens.

## Text Colors

| Token | Purpose |
|-------|---------|
| `text-primary` | Page headings, highest contrast text |
| `text-secondary` | Labels, section headings |
| `text-tertiary` | Supporting/paragraph text |
| `text-quaternary` | Footer headings, subtle text |
| `text-disabled` | Disabled fields/buttons |
| `text-placeholder` | Input placeholders |
| `text-brand-primary` | Brand headings |
| `text-brand-secondary` | Accented text, subheadings |
| `text-error-primary` | Error states |
| `text-success-primary` | Success states |
| `text-warning-primary` | Warning states |
| `text-white` | Always white regardless of mode |
| `text-primary_on-brand` | Text on solid brand backgrounds |

## Border Colors

| Token | Purpose |
|-------|---------|
| `border-primary` | Input fields, checkboxes (high contrast) |
| `border-secondary` | Cards, tables, dividers (default) |
| `border-tertiary` | Subtle dividers, chart axes |
| `border-disabled` | Disabled component borders |
| `border-brand` | Active input states |
| `border-error` | Error state borders |

## Foreground Colors (Icons)

| Token | Purpose |
|-------|---------|
| `fg-primary` | Highest contrast icons |
| `fg-secondary` | High contrast icons |
| `fg-tertiary` | Medium contrast icons |
| `fg-quaternary` | Help icons, input icons |
| `fg-brand-primary` | Featured icons, progress bars |
| `fg-error-primary` | Error featured icons |
| `fg-success-secondary` | Online indicators, positive metrics |
| `fg-white` | Always white foreground |
| `fg-disabled` | Disabled icon states |

## Background Colors

| Token | Purpose |
|-------|---------|
| `bg-primary` | Main layout background |
| `bg-secondary` | Section backgrounds |
| `bg-tertiary` | Toggles, contrast elements |
| `bg-disabled` | Disabled buttons/toggles |
| `bg-brand-solid` | Brand toggles, messages |
| `bg-error-solid` | Error buttons, featured icons |
| `bg-overlay` | Modal overlays |
| `bg-active` | Selected dropdown items |

## Brand Color Customization

Edit `resources/styles/theme.css` to update `--color-brand-*` variables. A complete scale from `25` to `950` is required, with `--color-brand-600` as the primary interactive color.

## Dark Mode

Dark mode is handled through CSS variables — no component-level changes needed. The design tokens in `theme.css` define both light and dark values automatically.
