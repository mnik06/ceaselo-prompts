## UI theme adapter

Library: Mantine (`@mantine/core` 7 or later) with `@tabler/icons-react`. The prototype's design tokens reach the boilerplate session as CSS custom properties (`--<token>: <value>`), grouped by DTCG group: color, font, type, space, radius, border, shadow, motion, component. Every token is applied; no value is invented or rounded.

**Tokens file.** Write every token, unchanged, as `:root { --ds-<token>: <value>; … }` in `src/theme/tokens.css` (the prototype's `--accent` becomes `--ds-accent`), imported once before any other style. It is the one place the values live: the theme below repeats them where Mantine needs a literal and reads them as `var(--ds-…)` everywhere else.

**Theme** (`src/theme/theme.ts`, `createTheme`, passed to `MantineProvider` with the resolver below):

| Mantine | Tokens |
| --- | --- |
| `colors.brand` (10 shades), `primaryColor: 'brand'`, `primaryShade: 6`, `autoContrast: true` | 0 `accent-subtle`, 1 `accent-subtle`, 2–4 steps from `accent-subtle` to `accent-border`, 5 `accent-border`, 6 `accent`, 7 `accent-hover`, 8–9 `accent-text` (literal values) |
| `colors.red`, `colors.green`, `colors.yellow`, `colors.blue` (shades 0–1 and 6–7) | `danger-subtle` / `danger` / `danger-hover`, `success-subtle` / `success`, `warning-subtle` / `warning`, `info-subtle` / `info` |
| `fontFamily`, `fontFamilyMonospace`, `headings.fontFamily` | `font-body`, `font-mono`, `font-heading` |
| `fontSizes` xs / sm / md / lg / xl | `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl` |
| `headings.sizes` h1 / h2 / h3 / h4, `headings.fontWeight` | `text-3xl`, `text-2xl`, `text-xl`, `text-lg`; `weight-heading` |
| `lineHeights.md`, `headings` line height | `leading`, `leading-tight` |
| `spacing` xs / sm / md / lg / xl | `space-2`, `space-3`, `space-4`, `space-6`, `space-8` |
| `radius` xs / sm / md / lg / xl, `defaultRadius: 'md'` | `radius-sm`, `radius-sm`, `radius`, `radius-lg`, `radius-lg` |
| `shadows` xs / sm / md / lg / xl | `shadow-sm`, `shadow-sm`, `shadow`, `shadow-lg`, `shadow-lg` |
| `cssVariablesResolver` (light) | `--mantine-color-body` `bg`, `--mantine-color-text` `text`, `--mantine-color-dimmed` `text-muted`, `--mantine-color-placeholder` `text-subtle`, `--mantine-color-anchor` `accent-text`, `--mantine-color-error` `danger`, `--mantine-color-default` `btn-bg`, `--mantine-color-default-hover` `btn-hover-bg`, `--mantine-color-default-color` `btn-text`, `--mantine-color-default-border` `btn-border` |
| `components` (`Button.extend`, `Input.extend`, … `vars`) | `--button-height-sm` / `-md` / `-lg` and `--input-height-sm` / `-md` / `-lg` from `control-h-sm`, `control-h`, `control-h-lg`; `Card` padding `card-pad`, radius `radius-card`, shadow `shadow-card`; `Table` cell padding `cell-pad-y` / `cell-pad-x`; `AppShell` navbar width `sidebar-w`, header height `topbar-h` |

Every other token (motion, borders, the nav, table and card colours, the remaining component sizes) is read as `var(--ds-<token>)` in the theme's `components` styles or a CSS module: `dur-fast` / `dur` / `ease` for transitions, `focus` and `focus-width` for the focus ring, `nav-*` for the navbar, `table-*` for tables, `page-max` / `page-narrow` for `Container` sizes. Load the families the font tokens name from `@fontsource` packages (self-hosted, no CDN).

**Vocabulary.** The prototype is written in the kit's classes; build its screens with these components, never by copying its CSS:

| Prototype class | Mantine |
| --- | --- |
| `.app`, `.sidebar`, `.topbar`, `.app__main` | `AppShell` with `AppShell.Navbar`, `AppShell.Header`, `AppShell.Main` |
| `.nav__item` (`aria-current`), `.nav__badge`, `.sidebar__section` | `NavLink` (`active`), `Badge` as its `rightSection`, `Text size="xs" tt="uppercase" c="dimmed"` |
| `.tabbar`, `.tabbar__item` | a fixed bottom `Group` of `UnstyledButton`s with icon and label |
| `.page`, `.page--narrow`, `.page--wide` | `Container` sized by `page-max`, `page-narrow`, `fluid` |
| `.page-header` (`__title`, `__description`, `__actions`) | `Group justify="space-between"` with `Title order={1}`, `Text c="dimmed"`, a `Group` of buttons |
| `.breadcrumbs`, `.section` | `Breadcrumbs`; `Stack` with `Title order={2}` |
| `.stack`, `.cluster`, `.split`, `.toolbar` (`.grow`, `.push`) | `Stack`, `Group wrap="wrap"`, `Group justify="space-between"`, `Group` (`flex={1}`, `ml="auto"`) |
| `.grid`, `.grid--2` / `--3` / `--4`, `.columns` | `SimpleGrid` (`minColWidth` from `grid-min` on Mantine 9, else `cols` by breakpoint), `SimpleGrid` with `cols` 1 on phones and n from `sm`, `Grid` with spans 8 and 4 |
| `.btn`, `--primary`, `--secondary`, `--ghost`, `--danger` | `Button variant="default"`, `variant="filled"`, `variant="light"`, `variant="subtle"`, `color="red"` |
| `.btn--sm` / `--lg`, `--block`, `--icon`, `aria-busy` | `size="sm"` / `"lg"`, `fullWidth`, `ActionIcon` (with `aria-label`), `loading` |
| `.card` (`__header`, `__title`, `__description`, `__body`, `__footer`), `--interactive`, `--flush` | `Card withBorder` (`Card.Section`, `Title order={3}`, `Text c="dimmed"`), `component="a"` with hover style, `padding={0}` |
| `.table`, `.table--compact`, `.table-wrap--scroll`, `.table__actions` | `Table highlightOnHover`, `verticalSpacing="xs"`, `Table.ScrollContainer`, `Group justify="flex-end"` |
| `.field` (`__label`, `__hint`, `__error`, `__optional`) | the input's `label`, `description`, `error`; a required field gets `withAsterisk`, an optional one none |
| `.input`, `.select`, `.textarea`, `.check`, `.switch`, `.input-icon` | `TextInput`, `Select`, `Textarea`, `Checkbox`, `Switch`, `leftSection` |
| `.badge` (`--accent`, `--success`, `--warning`, `--danger`, `--info`, `--dot`), `.status` | `Badge variant="light"` with `brand`, `green`, `yellow`, `red`, `blue`; `variant="dot"` |
| `.alert` (`--info`, `--success`, `--warning`, `--danger`, `--banner`) | `Alert` with the same colours; `radius={0}` full width |
| `.toast` | `@mantine/notifications` |
| `.dialog`, `--sm` / `--lg`, `--drawer` | `Modal size="sm"` / `"lg"`, `Drawer position="right"` |
| `.menu`, `.menu__item--danger` | `Menu`, `Menu.Item color="red"` |
| `.tabs`, `.tab` | `Tabs`, `Tabs.Tab` |
| `.avatar` (`--sm`, `--lg`), `.avatar-group` | `Avatar` (`size`), `Avatar.Group` |
| `.stat` (`__label`, `__value`, `__delta--up` / `--down`) | `Paper withBorder` with `Text size="sm" c="dimmed"`, `Title order={3}`, `Text c="green"` / `"red"` |
| `.meter` (`--success`, `--warning`, `--danger`), `.bars` | `Progress` (`color`), `@mantine/charts` `BarChart` |
| `.list`, `.list__item`, `.media` | `Stack` of rows divided by `Divider`; `Group` with `Avatar` and `Stack gap={0}` |
| `.empty`, `.skeleton`, `.spinner` | `Stack align="center"` with `ThemeIcon`, `Title`, `Text`; `Skeleton`; `Loader` |
| `.pagination`, `.steps`, `.dl`, `.divider` | `Pagination`, `Stepper`, `SimpleGrid cols={2}` of label and value, `Divider` |
| `.placeholder`, `.icon` | `AspectRatio` over a `surface-2` box; the Tabler icon closest to the Lucide icon the prototype names |
| `.muted`, `.strong`, `.text-sm`, `.num`, `.mono`, `.truncate` | `Text` props `c="dimmed"`, `fw`, `size`, a `fontVariantNumeric: 'tabular-nums'` style, `ff="monospace"`, `truncate` |
