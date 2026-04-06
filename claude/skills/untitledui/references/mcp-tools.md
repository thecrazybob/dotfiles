# Untitled UI MCP Tools Reference

The Untitled UI MCP server provides 6 tools for discovering, searching, and installing components and page templates.

## Tool Overview

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `list_components` | Browse all components by category | Exploring what's available in a category |
| `search_components` | Search by name/description/functionality | Finding a specific component |
| `get_component` | Get install command for one component | Ready to install a single component |
| `get_component_bundle` | Get install command for multiple components | Installing several components at once |
| `get_page_templates` | Browse page templates | Looking for full page layouts |
| `get_page_template_files` | Get install command for a template | Ready to install a page template |

## Detailed Tool Usage

### list_components

Browse components by category.

**Parameters:**
- `category` (optional): `base`, `application`, `marketing`, `foundations`, `shared-assets`, `examples`
- `limit` (optional): Max results (default 100)
- `skip` (optional): Pagination offset

**Categories explained:**
- `base` — Primitive UI elements (Button, Input, Select, Checkbox, Avatar, Badge, Tooltip, Toggle, etc.)
- `application` — Complex UI patterns (Table, Tabs, Modal, DatePicker, Pagination, Navigation, Charts, etc.)
- `marketing` — Marketing sections (Hero, Pricing, Testimonials, CTAs, Footers, Headers, FAQs, etc.)
- `foundations` — Design tokens and foundational elements (FeaturedIcon, DotIcon, PaymentIcons, Logos)
- `shared-assets` — Reusable assets (Illustrations, BackgroundPatterns, CreditCard, QRCode, iPhoneMockup)

### search_components

Search across all components by query.

**Parameters:**
- `query` (required): Search term (e.g., "button", "navigation", "form input", "chart")
- `category_filter` (optional): Limit to a category
- `limit` (optional): Max results (default 20)

Returns scored results with match reasons.

### get_component

Get metadata and CLI install command for a single component.

**Parameters:**
- `component_name` (required): Component name from list/search results

**Returns:**
- `cli_command`: The `npx untitledui@latest add <name> --yes` command
- `usage_examples`: Import paths and JSX examples
- `related_components`: Suggested related components
- `file_count`: Number of files to be installed

### get_component_bundle

Install multiple components at once.

**Parameters:**
- `components` (required): Array of component names

Returns a single CLI command that installs all specified components.

### get_page_templates

Browse page templates (landing pages, dashboards, settings, etc.).

**Parameters:**
- `page_type` (optional): `dashboard`, `marketing`, `application`, `all`
- `category` (optional): `landing-pages`, `pricing-pages`, `about-pages`, `contact-pages`, `blog-pages`, `blog-posts`, `team-pages`, `faq-pages`, `legal-pages`, `404-pages`, `dashboards`, `settings`, `informational`
- `layout` (optional): `sidebar`, `header`, `full-width`
- `limit` (optional): Max results (default 10)

**Template types available:**
- 223+ total templates
- Dashboard layouts (sidebar, header)
- Landing pages (10+ variants)
- Pricing, About, Contact, Blog, Team, FAQ, Legal, 404, Settings pages

### get_page_template_files

Get CLI install command for a complete page template.

**Parameters:**
- `template_name` (required): Full template name from `get_page_templates` (e.g., `landing-pages/01`, `dashboards-01/01`)

Returns the CLI command to install all template files at once.

## Access Levels

- `public` — Free components, available without API key
- `pro` — PRO components, require API key

The MCP server will indicate `has_pro_access: true/false` in responses.

## Workflow Patterns

### "I need a specific component"
1. `search_components(query: "date picker")`
2. `get_component(component_name: "date-picker")`
3. Run the returned CLI command

### "What's available for forms?"
1. `search_components(query: "form input select")`
2. Or: `list_components(category: "base")` to see all base components

### "I need a full dashboard page"
1. `get_page_templates(page_type: "dashboard", layout: "sidebar")`
2. Pick a template
3. `get_page_template_files(template_name: "dashboards-01/01")`
4. Run the CLI command

### "Install Button, Input, and Select together"
1. `get_component_bundle(components: ["button", "input", "select"])`
2. Run the single CLI command
