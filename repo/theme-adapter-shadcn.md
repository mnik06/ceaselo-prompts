## UI theme adapter

Library: shadcn/ui on Tailwind CSS 4, with `lucide-react` icons (the prototype's icon set). The prototype's design tokens reach the boilerplate session as CSS custom properties (`--<token>: <value>`), grouped by DTCG group: color, font, type, space, radius, border, shadow, motion, component. Every token is applied; no value is invented or rounded.

**Tokens file.** Write every token, unchanged, as `:root { --ds-<token>: <value>; … }` in `src/styles/tokens.css` (the prototype's `--accent` becomes `--ds-accent`: shadcn's own `--accent`, `--border` and `--radius` mean something else), imported at the top of the global CSS. It is the one place the values live: everything below reads them as `var(--ds-…)`.

**Theme** (the global CSS shadcn's `components.json` points at; no `.dark` block unless the preset asks for dark mode):

| shadcn / Tailwind variable | Token |
| --- | --- |
| `--background`, `--foreground` | `bg`, `text` |
| `--card`, `--card-foreground`, `--popover`, `--popover-foreground` | `card-bg`, `text`, `surface`, `text` |
| `--primary`, `--primary-foreground` | `accent`, `accent-ink` |
| `--secondary`, `--secondary-foreground` | `surface-2`, `text` |
| `--muted`, `--muted-foreground` | `surface-2`, `text-muted` |
| `--accent`, `--accent-foreground` | `accent-subtle`, `accent-text` |
| `--destructive`, `--border`, `--input`, `--ring` | `danger`, `border`, `control-border`, `focus` |
| `--chart-1` … `--chart-5` | `accent`, `info`, `success`, `warning`, `danger` |
| `--sidebar`, `--sidebar-foreground`, `--sidebar-border`, `--sidebar-ring` | `nav-bg`, `nav-text-strong`, `nav-border`, `focus` |
| `--sidebar-primary`, `--sidebar-primary-foreground`, `--sidebar-accent`, `--sidebar-accent-foreground` | `accent`, `accent-ink`, `nav-active-bg`, `nav-active-text` |
| `@theme inline` `--radius-sm` / `--radius-md` / `--radius-lg` / `--radius-xl` (replacing the scale computed from `--radius`; `--radius` itself is `radius-lg`) | `radius-sm`, `radius`, `radius-lg`, `radius-lg` |
| `@theme inline` `--font-sans`, `--font-heading`, `--font-mono` | `font-body`, `font-heading`, `font-mono` |
| `@theme inline` `--text-xs` … `--text-3xl` | `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl` |
| `@theme inline` `--spacing` (Tailwind's step, so `p-4` is `space-4`) | `space-1` |
| `@theme inline` `--shadow-sm`, `--shadow-md`, `--shadow-lg` | `shadow-sm`, `shadow`, `shadow-lg` |
| `@theme inline` `--default-transition-duration`, `--default-transition-timing-function` | `dur`, `ease` |
| `@theme inline` `--color-success`, `--color-warning`, `--color-info` and their `-subtle` | `success`, `warning`, `info`, `success-subtle`, `warning-subtle`, `info-subtle` |

Component sizes go into the generated components: `Button` and `Input` heights from `control-h-sm`, `control-h`, `control-h-lg` (`h-[var(--ds-control-h)]` in their size variants), `SidebarProvider` `--sidebar-width` from `sidebar-w`, the header height from `topbar-h`, page containers from `page-max` / `page-narrow`, card padding from `card-pad`, table cells from `cell-pad-y` / `cell-pad-x`. Every other token (weights, tracking, border widths, `table-*`, `btn-*`, the remaining component sizes) is read as `var(--ds-<token>)` by the component it names. Load the families the font tokens name from `@fontsource` packages (self-hosted, no CDN).

**Vocabulary.** The prototype is written in the kit's classes; build its screens with these components (add each with the shadcn CLI), never by copying its CSS:

| Prototype class | shadcn/ui |
| --- | --- |
| `.app`, `.sidebar` (`__brand`, `__group`, `__footer`), `.app__main` | `SidebarProvider`, `Sidebar` (`SidebarHeader`, `SidebarGroup`, `SidebarFooter`), `SidebarInset` |
| `.nav__item` (`aria-current`), `.nav__badge`, `.sidebar__section` | `SidebarMenuButton isActive` in `SidebarMenuItem`, `SidebarMenuBadge`, `SidebarGroupLabel` |
| `.topbar` (`__nav`, `__actions`), `.tabbar` | a `header` with `NavigationMenu` and the actions; a fixed bottom `nav` of icon-and-label links |
| `.page`, `.page--narrow`, `.page--wide` | a container `mx-auto max-w-[var(--ds-page-max)]`, `max-w-[var(--ds-page-narrow)]`, full width |
| `.page-header` (`__title`, `__description`, `__actions`), `.breadcrumbs` | a `header` `flex justify-between` with `h1`, a muted `p`, the buttons; `Breadcrumb` |
| `.stack`, `.cluster`, `.split`, `.toolbar` (`.grow`, `.push`), `.gap-*` | `flex flex-col`, `flex flex-wrap`, `flex justify-between`, `flex items-center` (`flex-1`, `ml-auto`), `gap-*` |
| `.grid`, `.grid--2` / `--3` / `--4`, `.columns` | `grid grid-cols-[repeat(auto-fill,minmax(var(--ds-grid-min),1fr))]`, `grid sm:grid-cols-n`, `grid lg:grid-cols-3` with a `col-span-2` main |
| `.btn`, `--primary`, `--secondary`, `--ghost`, `--danger` | `Button variant="outline"`, `"default"`, `"secondary"`, `"ghost"`, `"destructive"` |
| `.btn--sm` / `--lg`, `--icon`, `--block`, `aria-busy` | `size="sm"` / `"lg"`, `size="icon"` (with `aria-label`), `w-full`, `disabled` with a spinner |
| `.card` (`__header`, `__title`, `__description`, `__body`, `__footer`), `--interactive` | `Card` (`CardHeader`, `CardTitle`, `CardDescription`, `CardContent`, `CardFooter`), a link-wrapped `Card` with a hover style |
| `.table`, `.table--compact`, `.table__actions` | `Table` (`TableHeader`, `TableRow`, `TableHead`, `TableBody`, `TableCell`), smaller cell padding, a right-aligned cell of buttons |
| `.field` (`__label`, `__hint`, `__error`, `__optional`) | `Field` with `FieldLabel`, `FieldDescription`, `FieldError` (`Label` and a muted `p` where `Field` is not installed) |
| `.input`, `.select`, `.textarea`, `.check`, `.switch` | `Input`, `Select`, `Textarea`, `Checkbox`, `Switch` |
| `.badge` (`--accent`, `--success`, `--warning`, `--danger`, `--info`, `--dot`), `.status` | `Badge` with `success`, `warning`, `info` variants added to `badge.tsx` from those tokens, `destructive`, `outline` with a dot |
| `.alert` (`--info`, `--success`, `--warning`, `--danger`, `--banner`) | `Alert` (`AlertTitle`, `AlertDescription`), variants added the same way, `destructive` |
| `.toast`, `.dialog` (`--sm`, `--lg`), `.dialog--drawer` | `Sonner`; `Dialog` (`sm:max-w-[var(--ds-dialog-w-sm)]` …); `Sheet side="right"` |
| `.menu`, `.menu__item--danger`, `.tabs`, `.tab` | `DropdownMenu`, `DropdownMenuItem variant="destructive"`, `Tabs`, `TabsTrigger` |
| `.avatar` (`--sm`, `--lg`), `.avatar-group` | `Avatar` (`AvatarFallback` for initials), overlapping `Avatar`s |
| `.stat`, `.meter`, `.bars` | a `Card` with a muted label, the value and a coloured delta; `Progress`; `Chart` (Recharts bar) |
| `.list`, `.media`, `.empty` | a `divide-y` list; `flex gap-3` with `Avatar`; `Empty` (or a centred icon, title and text) |
| `.skeleton`, `.spinner`, `.pagination`, `.steps`, `.dl`, `.divider` | `Skeleton`, `Spinner`, `Pagination`, a numbered `ol` with done states, a two-column `dl` grid, `Separator` |
| `.placeholder`, `.icon` | `AspectRatio` over a `bg-secondary` box; the `lucide-react` icon of the same name |
| `.muted`, `.strong`, `.text-sm`, `.num`, `.mono`, `.truncate` | `text-muted-foreground`, `font-semibold`, `text-sm`, `tabular-nums`, `font-mono`, `truncate` |
