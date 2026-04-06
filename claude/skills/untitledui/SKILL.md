---
name: untitledui
version: 1.0.0
description: >-
  This skill should be used when adding, installing, searching for, or building with
  UI components; installing page templates; working with Untitled UI, the Untitled UI
  MCP server, @untitledui/icons, semantic color tokens, sortCx styling, or React Aria
  components; building dashboards, landing pages, or application pages; styling with
  design tokens or theme.css; or working with any React component from the
  resources/components/ library. Also activates for "add a component", "install a
  template", "find a component", "use Untitled UI", "dark mode tokens", "design system",
  or referencing the component library.
---

# Untitled UI Component Library

Untitled UI is a React component library built with TypeScript, Tailwind CSS v4, and React Aria (Adobe) for accessibility. Components live in `resources/components/` and use semantic design tokens from `resources/styles/theme.css`.

## MCP Tools — Component Discovery and Installation

Six MCP tools are available, all prefixed with `mcp__untitledui__`. Load via ToolSearch before first use:

| Tool | Purpose |
|------|---------|
| `mcp__untitledui__search_components` | Search by name/description/functionality |
| `mcp__untitledui__list_components` | Browse all components in a category |
| `mcp__untitledui__get_component` | Get CLI install command for one component |
| `mcp__untitledui__get_component_bundle` | Get CLI install command for multiple components |
| `mcp__untitledui__get_page_templates` | Browse page templates (dashboards, landing pages, etc.) |
| `mcp__untitledui__get_page_template_files` | Get CLI install command for a page template |

### Component Categories

- **base** — Primitives: Button, Input, Select, Checkbox, Avatar, Badge, Tooltip, Toggle, Textarea, Slider, Dropdown, ComboBox
- **application** — Complex patterns: Table, Tabs, Modal, DatePicker, Pagination, Navigation, Charts, CommandMenu, FileUpload, EmptyState, Messaging
- **marketing** — Sections: Hero, Pricing, Testimonials, CTAs, Footers, Headers, FAQs, Banners, Features, Newsletter
- **foundations** — Design tokens: FeaturedIcon, DotIcon, PaymentIcons, SocialIcons, RatingStars, Logos
- **shared-assets** — Reusable assets: Illustrations, BackgroundPatterns, CreditCard, QRCode, iPhoneMockup, Cropper

Not all components are installed locally. Check `resources/components/` for what exists on disk. Install missing components via MCP tools.

### Installation Workflow

1. Search or list to find the component
2. Call `get_component` or `get_component_bundle` to get the CLI command
3. Run the returned `npx untitledui@latest add <name> --yes` command in the terminal
4. The CLI handles dependencies and file placement automatically

For page templates: `get_page_templates` → pick a template → `get_page_template_files` → run the CLI command.

## Critical Conventions

### Semantic Color Tokens

**NEVER use raw Tailwind color classes.** Always use semantic variables:

| Instead of | Use |
|-----------|-----|
| `text-gray-900` | `text-primary` |
| `text-gray-600` | `text-secondary` |
| `bg-blue-700` | `bg-primary` |
| `border-gray-300` | `border-secondary` |

For the full token reference, consult `references/color-tokens.md`.

### React Aria Import Prefix

All React Aria imports MUST use an `Aria*` prefix:

```typescript
import { Button as AriaButton, TextField as AriaTextField } from "react-aria-components";
```

### File Naming

All files use **kebab-case**: `date-picker.tsx`, `user-profile.tsx`. Never `DatePicker.tsx`.

### Import Paths

Components use the `@/` alias (resolves to `resources/`):

```typescript
import { Button } from "@/components/base/buttons/button";
import { Input } from "@/components/base/input/input";
import { Badge } from "@/components/base/badges/badges";
import { Avatar } from "@/components/base/avatar/avatar";
import { FeaturedIcon } from "@/components/foundations/featured-icon/featured-icon";
import { Table } from "@/components/application/table/table";
import { cx, sortCx } from "@/utils/cx";
```

### Icon Usage

```typescript
import { Home01, ChevronDown, Settings01 } from "@untitledui/icons";

// As component reference (preferred for component props)
<Button iconLeading={ChevronDown}>Options</Button>

// As JSX element (must include data-icon attribute)
<Button iconLeading={<ChevronDown data-icon className="size-4" />}>Options</Button>

// Standalone
<Home01 className="size-5 text-brand-600" aria-hidden="true" />
```

Size classes: `size-4` (16px), `size-5` (20px), `size-6` (24px).

### Style Pattern (sortCx)

```typescript
import { cx, sortCx } from "@/utils/cx";

export const styles = sortCx({
    common: { root: "base-classes" },
    sizes: { sm: { root: "..." }, md: { root: "..." } },
    colors: { primary: { root: "..." }, secondary: { root: "..." } },
});
```

## Commonly Used Components

| Component | Import | Key Props |
|-----------|--------|-----------|
| Button | `@/components/base/buttons/button` | `size`, `color`, `iconLeading`, `isLoading`, `href` |
| Input | `@/components/base/input/input` | `size`, `label`, `icon`, `isRequired`, `isInvalid`, `hint` |
| Select | `@/components/base/select/select` | `label`, `items`, `placeholder` |
| Badge | `@/components/base/badges/badges` | `size`, `color`, `type` |
| Avatar | `@/components/base/avatar/avatar` | `size`, `src`, `initials`, `status` |
| FeaturedIcon | `@/components/foundations/featured-icon/featured-icon` | `icon`, `size`, `color`, `theme` |
| Checkbox | `@/components/base/checkbox/checkbox` | `size`, `label`, `hint`, `isSelected` |
| Toggle | `@/components/base/toggle/toggle` | Standard toggle props |
| Tooltip | `@/components/base/tooltip/tooltip` | Standard tooltip props |

For complete API details, consult `references/component-api.md`.

## Before Building UI

1. **Check existing components** in `resources/components/` before creating new ones
2. **Search MCP** for components not yet installed: `search_components(query: "...")`
3. **Use semantic tokens** — never raw Tailwind colors
4. **Follow kebab-case** for all new files
5. **Prefix React Aria imports** with `Aria*`

## Additional Resources

### Reference Files

- **`references/color-tokens.md`** — Complete semantic color token reference (text, border, fg, bg)
- **`references/component-api.md`** — Detailed component props, variants, and usage examples
- **`references/mcp-tools.md`** — Full MCP tool documentation with parameters and workflow patterns
- **`references/icons-and-patterns.md`** — Icon packages, sortCx pattern, compound components, project structure

### Key Project Files

- `resources/styles/theme.css` — Design tokens (brand colors, semantic variables)
- `resources/styles/globals.css` — Global stylesheet
- `resources/utils/cx.ts` — Class name utilities (cx, sortCx)
- `resources/utils/is-react-component.ts` — Component type checking
