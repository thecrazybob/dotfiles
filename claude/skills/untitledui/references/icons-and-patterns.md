# Untitled UI Icons and Component Patterns

## Icon Packages

| Package | Contents | Access |
|---------|----------|--------|
| `@untitledui/icons` | 1,100+ line-style icons | Free |
| `@untitledui/file-icons` | File type icons | Free |
| `@untitledui-pro/icons` | 4,600+ icons in 4 styles | PRO |

### PRO Icon Style Imports

```typescript
import { Home01 } from "@untitledui-pro/icons/duocolor";
import { Home01 } from "@untitledui-pro/icons/duotone";
import { Home01 } from "@untitledui-pro/icons/solid";
```

### Icon Usage Patterns

**As component reference (preferred for component props):**
```tsx
import { ChevronDown } from "@untitledui/icons";
<Button iconLeading={ChevronDown}>Options</Button>
```

**As JSX element (must include `data-icon` attribute):**
```tsx
<Button iconLeading={<ChevronDown data-icon className="size-4" />}>Options</Button>
```

**Standalone:**
```tsx
<Home01 className="size-5 text-brand-600" aria-hidden="true" />
```

### Icon Size Classes

| Class | Size |
|-------|------|
| `size-4` | 16px |
| `size-5` | 20px |
| `size-6` | 24px |

---

## React Aria Import Convention

All React Aria imports MUST use an `Aria*` prefix to prevent naming conflicts:

```typescript
import { Button as AriaButton, TextField as AriaTextField } from "react-aria-components";
```

---

## File Naming Convention

All files MUST use kebab-case:
- `date-picker.tsx` not `DatePicker.tsx`
- `user-profile.tsx` not `userProfile.tsx`
- `auth-context.tsx` not `AuthContext.tsx`

Applies to all `.tsx`, `.ts`, `.js`, `.css` files.

---

## Style Utility Pattern (sortCx)

```typescript
import { cx, sortCx } from "@/utils/cx";

export const styles = sortCx({
    common: { root: "base-classes", icon: "icon-classes" },
    sizes: {
        sm: { root: "small-size-classes" },
        md: { root: "medium-size-classes" },
    },
    colors: {
        primary: { root: "primary-color-classes" },
        secondary: { root: "secondary-color-classes" },
    },
});
```

- `cx()` — Class name merging (wraps tailwind-merge with custom tokens)
- `sortCx()` — Organized style objects for variant-based styling
- `isReactComponent()` — Component type checking utility from `@/utils/is-react-component`

---

## Compound Component Pattern

```typescript
const Select = SelectComponent as typeof SelectComponent & {
    Item: typeof SelectItem;
    ComboBox: typeof ComboBox;
};
Select.Item = SelectItem;
Select.ComboBox = ComboBox;
```

---

## Conditional Rendering Pattern

```tsx
{label && <Label isRequired={isRequired}>{label}</Label>}
{hint && <HintText isInvalid={isInvalid}>{hint}</HintText>}
```

---

## Animation

For hover/state transitions:
```tsx
className="transition duration-100 ease-linear"
```

Complex animations: use `motion` (Framer Motion).
Utility animations: `tailwindcss-animate`.

---

## Project Structure

```
resources/
├── components/
│   ├── base/              # Button, Input, Select, Checkbox, Avatar, Badge, Tooltip
│   ├── application/       # DatePicker, Modal, Pagination, Table, Tabs, Navigation
│   ├── foundations/        # FeaturedIcon, DotIcon, Logos, PaymentIcons
│   ├── marketing/          # Marketing sections (installed via MCP/CLI)
│   └── shared-assets/      # Illustrations, BackgroundPatterns, QRCode
├── styles/
│   ├── globals.css         # Global stylesheet
│   ├── theme.css           # Design tokens (73KB, all semantic variables)
│   └── typography.css      # Typography tokens
├── utils/
│   ├── cx.ts               # Class name utilities (cx, sortCx)
│   └── is-react-component.ts  # Component type checking
└── js/                     # Application pages consuming components
```

The `@/` alias resolves to `resources/`, enabling imports like:
```typescript
import { Button } from "@/components/base/buttons/button";
import { cx } from "@/utils/cx";
```
