# Untitled UI Component API Reference

## Button

```typescript
import { Button } from "@/components/base/buttons/button";
```

**Props**: `size` (`sm|md|lg|xl`), `color`, `iconLeading`, `iconTrailing`, `isDisabled`, `isLoading`, `showTextWhileLoading`, `href`

**Color variants**: `primary`, `secondary`, `tertiary`, `link-gray`, `link-color`, `link-destructive`, `primary-destructive`, `secondary-destructive`, `tertiary-destructive`

```tsx
<Button size="md" color="primary" iconLeading={Check}>Save</Button>
<Button isLoading showTextWhileLoading>Submitting...</Button>
<Button color="primary-destructive" iconLeading={Trash02}>Delete</Button>
```

No separate Link component exists. Use Button with `href` and link color variants.

---

## Input

```typescript
import { Input } from "@/components/base/input/input";
import { InputGroup } from "@/components/base/input/input-group";
```

**Props**: `size` (`sm|md`), `label`, `placeholder`, `hint`, `tooltip`, `icon`, `isRequired`, `isDisabled`, `isInvalid`

```tsx
<Input label="Email" icon={Mail01} isRequired isInvalid hint="Enter a valid email" />
```

---

## Select / MultiSelect / ComboBox

```typescript
import { Select } from "@/components/base/select/select";
import { MultiSelect } from "@/components/base/select/multi-select";
```

**Props**: `size`, `label`, `placeholder`, `hint`, `tooltip`, `items`, `isRequired`, `isDisabled`, `placeholderIcon`

**Item props**: `id`, `supportingText`, `icon`, `avatarUrl`, `isDisabled`

```tsx
<Select label="Team member" items={users}>
  {(item) => <Select.Item id={item.id} supportingText={item.email}>{item.name}</Select.Item>}
</Select>

<Select.ComboBox label="Search" items={users}>
  {(item) => <Select.Item id={item.id}>{item.name}</Select.Item>}
</Select.ComboBox>
```

---

## Checkbox

```typescript
import { Checkbox } from "@/components/base/checkbox/checkbox";
```

**Props**: `size` (`sm|md`), `label`, `hint`, `isSelected`, `isDisabled`, `isIndeterminate`

```tsx
<Checkbox label="Remember me" hint="Save my login details for next time" />
```

---

## Badge / BadgeWithDot / BadgeWithIcon

```typescript
import { Badge, BadgeWithDot, BadgeWithIcon } from "@/components/base/badges/badges";
```

**Props**: `size` (`sm|md|lg`), `color`, `type` (`pill-color|color|modern`)

**Colors**: `gray`, `brand`, `error`, `warning`, `success`, `blue-gray`, `blue-light`, `blue`, `indigo`, `purple`, `pink`, `rose`, `orange`

```tsx
<Badge color="brand" size="md">New</Badge>
<BadgeWithDot color="success" type="pill-color">Active</BadgeWithDot>
<BadgeWithIcon iconLeading={ArrowUp} color="success">12%</BadgeWithIcon>
```

---

## Avatar / AvatarLabelGroup

```typescript
import { Avatar } from "@/components/base/avatar/avatar";
import { AvatarLabelGroup } from "@/components/base/avatar/avatar-label-group";
```

**Props**: `size` (`xs|sm|md|lg|xl|2xl`), `src`, `alt`, `initials`, `placeholderIcon`, `status` (`online|offline`), `verified`, `badge`

```tsx
<Avatar src="/avatar.jpg" status="online" size="md" />
<Avatar initials="OR" size="lg" />
<AvatarLabelGroup src="/avatar.jpg" title="Olivia Rhye" subtitle="olivia@untitledui.com" size="md" />
```

---

## FeaturedIcon

```typescript
import { FeaturedIcon } from "@/components/foundations/featured-icon/featured-icon";
```

**Props**: `icon` (required), `size` (`sm|md|lg|xl`), `color` (`brand|gray|error|warning|success`), `theme` (`light|gradient|dark|modern|modern-neue|outline`)

`modern` and `modern-neue` themes only work with `color="gray"`.

```tsx
<FeaturedIcon icon={CheckCircle} color="success" theme="light" size="lg" />
<FeaturedIcon icon={Settings} color="gray" theme="modern" size="lg" />
```

---

## Tooltip

```typescript
import { Tooltip, TooltipTrigger } from "@/components/base/tooltip/tooltip";
```

Wraps React Aria's Tooltip. Combines `TooltipTriggerComponentProps` with `TooltipProps`.

**Props**: `content` (tooltip text), `placement`, `delay`, plus all React Aria tooltip trigger props

```tsx
<Tooltip content="Save your changes">
  <TooltipTrigger><Button>Save</Button></TooltipTrigger>
</Tooltip>
```

---

## Toggle

```typescript
import { Toggle } from "@/components/base/toggle/toggle";
```

Wraps React Aria's Switch component.

**Props**: `size` (`sm|md`), `label`, `hint`, `slim` (boolean), `className`, plus all React Aria `SwitchProps`

```tsx
<Toggle label="Email notifications" hint="Get notified about updates" size="sm" />
<Toggle label="Dark mode" slim />
```

---

## TextArea

```typescript
import { TextArea } from "@/components/base/textarea/textarea";
```

Wraps React Aria's TextField with a multi-line text area.

**Props**: `size` (`sm|md`), `label`, `hint`, `tooltip`, `isRequired`, `isDisabled`, `isInvalid`, `textAreaClassName`, `textAreaRef`

```tsx
<TextArea label="Description" hint="Max 500 characters" isRequired />
```

---

## Table

```typescript
import { Table, TableCard } from "@/components/application/table/table";
```

Compound component wrapping React Aria's Table with sorting and selection.

**Sub-components**: `Table.Root`, `Table.Header`, `Table.Head`, `Table.Row`, `Table.Cell`, `TableCard.Header`

**Table.Root props**: `size` (`sm|md`), plus all React Aria `TableProps`
**Table.Head props**: `tooltip`, `label`, plus React Aria `ColumnProps`
**Table.Row props**: `highlightSelectedRow` (boolean)
**TableCard.Header props**: `title`, `badge`, `description`, `contentTrailing`

```tsx
<TableCard>
  <TableCard.Header title="Team members" badge={<Badge>10</Badge>} />
  <Table.Root size="md">
    <Table.Header>
      <Table.Head id="name" isRowHeader>Name</Table.Head>
      <Table.Head id="email">Email</Table.Head>
    </Table.Header>
    <Table.Body>
      <Table.Row><Table.Cell>John</Table.Cell><Table.Cell>john@example.com</Table.Cell></Table.Row>
    </Table.Body>
  </Table.Root>
</TableCard>
```

---

## Tabs

```typescript
import { Tabs, TabList, Tab, TabPanel } from "@/components/application/tabs/tabs";
```

Wraps React Aria's Tabs with styled variants.

**TabList props**: `type` (`button-gray|button-primary|underline-default|underline-color|underline-full|minimal`), `size` (`sm|md`), `fullWidth` (boolean), plus React Aria `TabListProps`
**Tab props**: `label`, `badge`, `icon`, plus React Aria `TabProps`

```tsx
<Tabs>
  <TabList type="underline-default" size="sm">
    <Tab id="general" label="General" />
    <Tab id="security" label="Security" badge="3" />
  </TabList>
  <TabPanel id="general">General content</TabPanel>
  <TabPanel id="security">Security content</TabPanel>
</Tabs>
```

---

## Modal

```typescript
import { Modal, ModalOverlay, Dialog, DialogTrigger } from "@/components/application/modals/modal";
```

Wraps React Aria's Modal and Dialog components.

**Props**: All React Aria `ModalOverlayProps` and `DialogProps`

```tsx
<DialogTrigger>
  <Button>Open Modal</Button>
  <ModalOverlay>
    <Modal>
      <Dialog>
        <h2>Modal Title</h2>
        <p>Modal content</p>
      </Dialog>
    </Modal>
  </ModalOverlay>
</DialogTrigger>
```

---

## EmptyState

```typescript
import { EmptyState } from "@/components/application/empty-state/empty-state";
```

Compound component for empty/zero-state views.

**Sub-components**: `EmptyState.Root`, `EmptyState.Header`, `EmptyState.FeaturedIcon`, `EmptyState.Illustration`, `EmptyState.FileTypeIcon`, `EmptyState.Content`, `EmptyState.Title`, `EmptyState.Description`, `EmptyState.Footer`

**Root props**: `size` (`sm|md|lg`)
**Header props**: `pattern` (`none|circle|grid|dots`), `patternSize` (`sm|md`)
**FeaturedIcon props**: `icon`, `color`, `theme`, `size`
**Illustration props**: `type` (`cloud|box|documents`), `color`, `size`

```tsx
<EmptyState.Root size="lg">
  <EmptyState.Header pattern="circle">
    <EmptyState.FeaturedIcon icon={SearchLg} />
  </EmptyState.Header>
  <EmptyState.Content>
    <EmptyState.Title>No results found</EmptyState.Title>
    <EmptyState.Description>Try adjusting your search</EmptyState.Description>
  </EmptyState.Content>
  <EmptyState.Footer>
    <Button color="primary">Clear filters</Button>
  </EmptyState.Footer>
</EmptyState.Root>
```

---

## FileUpload

```typescript
import { FileUpload, FileUploadDropZone, FileListItemProgressBar } from "@/components/application/file-upload/file-upload-base";
```

Compound component for file upload with drag-and-drop.

**Sub-components**: `FileUpload.Root`, `FileUpload.List`
**FileUploadDropZone props**: `onDrop`, `accept`, `maxSize`, `multiple`, `size`, `icon`, `description`, `actionLabel`
**FileListItemProgressBar props**: `name`, `size`, `progress`, `failed`, `type`, `onDelete`, `onRetry`

```tsx
<FileUpload.Root>
  <FileUploadDropZone onDrop={handleDrop} accept="image/*" maxSize={5242880} />
  <FileUpload.List>
    <FileListItemProgressBar name="photo.jpg" size={1024000} progress={75} onDelete={handleDelete} />
  </FileUpload.List>
</FileUpload.Root>
```

---

## Dropdown

```typescript
import { Dropdown } from "@/components/base/dropdown/dropdown";
```

Compound component wrapping React Aria's Menu.

**Sub-components**: `Dropdown.Trigger` (AriaMenuTrigger), `Dropdown.DotsButton`, `Dropdown.Popover`, `Dropdown.Menu`, `Dropdown.Item`, `Dropdown.Separator`

**Dropdown.Item props**: `label`, `icon`, `addon`, `unstyled`, plus React Aria `MenuItemProps`

```tsx
<Dropdown.Trigger>
  <Dropdown.DotsButton />
  <Dropdown.Popover>
    <Dropdown.Menu>
      <Dropdown.Item label="Edit" icon={Edit01} />
      <Dropdown.Item label="Copy" icon={Copy01} />
      <Dropdown.Separator />
      <Dropdown.Item label="Delete" icon={Trash01} />
    </Dropdown.Menu>
  </Dropdown.Popover>
</Dropdown.Trigger>
```

---

## HeaderNavigation

```typescript
import { HeaderNavigationBase } from "@/components/application/app-navigation/header-navigation";
import { NavList } from "@/components/application/app-navigation/base-components/nav-list";
import { NavAccountCard } from "@/components/application/app-navigation/base-components/nav-account-card";
```

Application header with navigation items, search, and account menu.

**HeaderNavigationBase props**: `logo`, `navItems`, `activeUrl`, `className`, `children`
**NavList props**: `activeUrl`, `items` (array of `NavItemType`), `className`

```tsx
<HeaderNavigationBase logo={<Logo />} navItems={navItems} activeUrl="/dashboard">
  <NavAccountCard name="John Doe" email="john@example.com" avatarSrc="/avatar.jpg" />
</HeaderNavigationBase>
```
