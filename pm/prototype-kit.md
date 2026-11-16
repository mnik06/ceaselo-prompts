## The prototype kit

Code supplies the whole design system: reset, theme tokens, font, icons, components, router and the prototype control bar. You write **semantic HTML that uses the kit's classes**, nothing else. The theme (accent, neutrals, type scale, spacing, radius) comes from the design brief, so the same markup restyles itself when the brief changes. Use only the classes below; an unknown class has no style.

### Never write

- a `<style>` element, a `<link>` stylesheet, or a `style` attribute that sets a colour, background, border colour, font or shadow (the only allowed inline style is a `--value` for `.meter` and `.bars__bar`, e.g. `style="--value:62%"`);
- a colour literal anywhere (hex, `rgb()`, `hsl()`, `oklch()`), a CSS `gradient(`;
- the prototype control bar, a router, a `hashchange` listener or any navigation script;
- emoji in buttons, links, nav items, tabs or headings (use kit icons);
- "lorem ipsum" or placeholder copy;
- external URLs, remote images, web fonts or CDN scripts: use icons, initials avatars, `.placeholder` and `.skeleton` blocks.

### The shell and the screens

The app shell wraps every screen. It holds the brand slot and exactly one element with `data-slot="screens"`; code places the screens inside it.

```html
<div class="app">
  <aside class="sidebar">
    <a class="sidebar__brand" href="#/dashboard" data-slot="logo"></a>
    <nav class="sidebar__group" aria-label="Main">
      <p class="sidebar__section">Workspace</p>
      <a class="nav__item" href="#/dashboard" aria-current="page"><svg class="icon" aria-hidden="true"><use href="#i-layout-dashboard"/></svg>Dashboard</a>
      <a class="nav__item" href="#/orders"><svg class="icon" aria-hidden="true"><use href="#i-package"/></svg>Orders<span class="nav__badge">12</span></a>
    </nav>
    <div class="sidebar__footer">
      <div class="media"><span class="avatar avatar--sm">MK</span><div class="media__body"><div class="media__title">Maria Kovacs</div><div class="media__meta">Admin</div></div></div>
    </div>
  </aside>
  <div class="app__main">
    <main data-slot="screens"></main>
  </div>
</div>
```

- **Top-bar layout**: `<div class="app app--topbar"><header class="topbar"><a class="topbar__brand" data-slot="logo" href="#/home"></a><nav class="topbar__nav" aria-label="Main"><a class="tab" href="#/home" aria-current="page">Home</a>…</nav><div class="topbar__actions">…</div></header><main data-slot="screens"></main></div>`.
- **Logo slot**: leave `[data-slot="logo"]` empty; code fills it with the uploaded logo (`.pk-logo`) or the product name (`.pk-wordmark`).
- **Mobile app nav**: a bottom tab bar inside a screen, `<nav class="tabbar" aria-label="Main"><a class="tabbar__item" href="#/home" aria-current="page"><svg class="icon" aria-hidden="true"><use href="#i-house"/></svg>Home</a>…</nav>`.
- The sidebar becomes a horizontal strip and grids collapse on narrow viewports by themselves; never write media queries.

**Screens.** A screen's markup is its content only; code wraps it in `<section data-screen="route">` (and a phone frame when the plan marks it mobile). Give every state the plan lists its own block, `default` first; every non-default block carries `hidden`:

```html
<div data-state="default"><div class="page">…</div></div>
<div data-state="empty" hidden><div class="page">…</div></div>
<div data-state="loading" hidden><div class="page">…</div></div>
```

### Page structure

```html
<div class="page">
  <nav class="breadcrumbs" aria-label="Breadcrumb"><ol><li><a href="#/orders">Orders</a></li><li aria-current="page">ORD-2041</li></ol></nav>
  <header class="page-header">
    <div><h1 class="page-header__title">Orders</h1><p class="page-header__description">Every order placed in the last 90 days.</p></div>
    <div class="page-header__actions"><button type="button" class="btn">Export</button><a class="btn btn--primary" href="#/orders/new"><svg class="icon" aria-hidden="true"><use href="#i-plus"/></svg>New order</a></div>
  </header>
  <section class="section"><h2>Recent activity</h2>…</section>
</div>
```

`.page--narrow` for forms and settings, `.page--wide` for boards and wide tables. Headings `h1`–`h4` are styled; one `h1` per screen.

### Layout utilities

- `.stack` vertical flow; `.cluster` a wrapping row; `.split` a row pushed to both ends; `.toolbar` a filter row (put `.grow` on the search field, `.push` to send an item right).
- `.grid` auto-fills cards (min 16rem); `.grid--2`, `.grid--3`, `.grid--4` fixed columns that collapse on small screens.
- `.columns` main content plus a side column (2:1), stacked on small screens.
- Gap modifiers on any of these: `.gap-xs`, `.gap-sm`, `.gap-md`, `.gap-lg`, `.gap-xl`. `.align-start` aligns a row to the top.
- Text: `.muted`, `.strong`, `.medium`, `.text-xs`, `.text-sm`, `.text-lg`, `.text-success`, `.text-warning`, `.text-danger`, `.num` (tabular figures), `.mono`, `.truncate`, `.measure` (65ch), `.sr-only`.

### Components

**Buttons.** `.btn` is the neutral button; add `--primary` (one per view), `--secondary`, `--ghost`, `--danger`; sizes `--sm`, `--lg`; `--icon` for an icon-only button (always with `aria-label`); `--block` full width. Disabled: `disabled` (or `aria-disabled="true"` on a link). Loading: `aria-busy="true"` with a label such as "Saving…".

```html
<button type="button" class="btn btn--primary">Save changes</button>
<button type="button" class="btn btn--ghost btn--icon" aria-label="More actions"><svg class="icon" aria-hidden="true"><use href="#i-ellipsis"/></svg></button>
<button type="button" class="btn btn--primary" aria-busy="true" disabled>Saving…</button>
```

**Form fields.** Wrap each control in `.field`; inputs inside `.field` are styled without a class (outside one, use `.input`, `.select`, `.textarea`). Invalid: `aria-invalid="true"` on the control plus a `.field__error` linked by `aria-describedby`.

```html
<div class="field">
  <label class="field__label" for="email">Work email</label>
  <input id="email" type="email" value="maria@" aria-invalid="true" aria-describedby="email-error">
  <p class="field__error" id="email-error"><svg class="icon icon--sm" aria-hidden="true"><use href="#i-circle-alert"/></svg>Enter a full email address, e.g. maria@northwind.com</p>
</div>
<div class="field"><label class="field__label" for="notes">Notes <span class="field__optional">(optional)</span></label><textarea id="notes"></textarea><p class="field__hint">Visible to your team only.</p></div>
<div class="input-icon grow"><svg class="icon" aria-hidden="true"><use href="#i-search"/></svg><input class="input" type="search" placeholder="Search orders" aria-label="Search orders"></div>
<label class="check"><input type="checkbox" checked> Email me when an order ships</label>
<label class="check"><input type="radio" name="plan"> Monthly</label>
<label class="switch"><input type="checkbox" role="switch" checked> Auto-renew</label>
```

**Card.** `.card` with optional `.card__header` (`.card__title`, `.card__description`), `.card__body`, `.card__footer`. `.card--flush` for a card that holds a table or list edge to edge; `.card--interactive` on an `<a class="card">` that opens something.

```html
<div class="card">
  <div class="card__header"><div><h2 class="card__title">Billing details</h2><p class="card__description">Used on every invoice.</p></div><button type="button" class="btn btn--sm">Edit</button></div>
  <div class="card__body">…</div>
  <div class="card__footer"><button type="button" class="btn">Cancel</button><button type="button" class="btn btn--primary">Save</button></div>
</div>
```

**Table.** Always inside `.table-wrap` (it scrolls on its own, never the page); `.table-wrap--scroll` caps its height with a sticky header. Numeric columns get `.num` on both `th` and `td`; the row actions cell `.table__actions`; a selected row `aria-selected="true"`; `.table--compact` for dense data.

```html
<div class="card card--flush">
  <div class="card__header"><h2 class="card__title">Open invoices</h2><span class="badge">24</span></div>
  <div class="table-wrap">
    <table class="table">
      <thead><tr><th>Invoice</th><th>Customer</th><th>Status</th><th class="num">Amount</th><th class="table__actions"><span class="sr-only">Actions</span></th></tr></thead>
      <tbody>
        <tr><td><a href="#/invoices/detail?id=1">INV-1042</a></td><td>Northwind Traders</td><td><span class="badge badge--warning badge--dot">Overdue</span></td><td class="num">€4,280.00</td><td class="table__actions"><button type="button" class="btn btn--ghost btn--icon btn--sm" aria-label="Actions for INV-1042"><svg class="icon" aria-hidden="true"><use href="#i-ellipsis"/></svg></button></td></tr>
      </tbody>
    </table>
  </div>
</div>
```

**Badge.** `.badge` (neutral) with `--success`, `--warning`, `--danger`, `--info`, `--accent`; add `--dot` for a status dot. Status text only, never decoration.

**Tabs.** In-page tabs (the runtime switches them):

```html
<div data-tabs>
  <div class="tabs" role="tablist" aria-label="Customer">
    <button type="button" class="tab" role="tab" aria-selected="true" aria-controls="tab-overview">Overview</button>
    <button type="button" class="tab" role="tab" aria-selected="false" aria-controls="tab-orders">Orders</button>
  </div>
  <div role="tabpanel" id="tab-overview">…</div>
  <div role="tabpanel" id="tab-orders" hidden>…</div>
</div>
```

Tabs that are routes are links: `<nav class="tabs" aria-label="Settings"><a class="tab" href="#/settings/profile" aria-current="page">Profile</a>…</nav>`.

**Alert / banner.** `.alert` with `--info`, `--success`, `--warning`, `--danger`; `.alert--banner` spans the top of a page.

```html
<div class="alert alert--warning" role="status"><svg class="icon" aria-hidden="true"><use href="#i-triangle-alert"/></svg><div class="alert__body"><p class="alert__title">Card expires in 6 days</p><p>Update it before 30 Nov to keep deliveries running.</p></div><button type="button" class="btn btn--sm">Update card</button></div>
```

**Empty state.**

```html
<div class="empty"><div class="empty__icon"><svg class="icon" aria-hidden="true"><use href="#i-inbox"/></svg></div><h3 class="empty__title">No orders yet</h3><p class="empty__text">Orders appear here as soon as a customer checks out.</p><a class="btn btn--primary" href="#/orders/new">Create an order</a></div>
```

**Loading.** `.skeleton` blocks shaped like the content they stand for: `--text`, `--title`, `--avatar`, `--block`; set a width with `.measure` or the surrounding layout. `.spinner` is an inline spinner; `class="icon spin"` with `#i-loader-circle` spins an icon.

```html
<div class="card"><div class="card__body"><span class="skeleton skeleton--title"></span><span class="skeleton skeleton--text"></span><span class="skeleton skeleton--text"></span></div></div>
```

**Image placeholder.** `<div class="placeholder"><svg class="icon" aria-hidden="true"><use href="#i-image"/></svg></div>` (16:9); `.placeholder--square` for 1:1.

**Dialog.** A `<dialog class="dialog">` with an `id`; `--sm`, `--lg`, `--drawer` (side panel). It opens from a button with `data-open-dialog="<dialog id>"` and closes from any element inside it with `data-close-dialog`.

```html
<button type="button" class="btn btn--danger" data-open-dialog="delete-order">Delete order</button>
<dialog class="dialog dialog--sm" id="delete-order" aria-labelledby="delete-order-title">
  <div class="dialog__header"><h2 class="dialog__title" id="delete-order-title">Delete ORD-2041?</h2><button type="button" class="btn btn--ghost btn--icon btn--sm" aria-label="Close" data-close-dialog><svg class="icon" aria-hidden="true"><use href="#i-x"/></svg></button></div>
  <div class="dialog__body"><p>The customer is not notified. This cannot be undone.</p></div>
  <div class="dialog__footer"><button type="button" class="btn" data-close-dialog>Cancel</button><button type="button" class="btn btn--danger" data-close-dialog>Delete order</button></div>
</dialog>
```

**Toast.** Show a toast as its own state of the screen (e.g. `data-state="saved"`): `<div class="toast-region"><div class="toast toast--success" role="status"><svg class="icon" aria-hidden="true"><use href="#i-circle-check"/></svg><div class="toast__body"><p class="toast__title">Invoice sent</p><p class="muted">Northwind Traders will get it in a minute.</p></div></div></div>`. Variants `--success`, `--warning`, `--danger`, `--info`.

**Avatar and identity.** Initials only: `<span class="avatar">MK</span>`, `--sm`, `--lg`; stacked with `.avatar-group`. A person or company row: `<div class="media"><span class="avatar">NT</span><div class="media__body"><div class="media__title">Northwind Traders</div><div class="media__meta">Customer since 2021</div></div></div>`.

**Stat tile.**

```html
<div class="grid grid--4">
  <div class="stat"><p class="stat__label"><svg class="icon icon--sm" aria-hidden="true"><use href="#i-dollar-sign"/></svg>Revenue, November</p><p class="stat__value">€48,920</p><p class="stat__delta stat__delta--up"><svg class="icon icon--sm" aria-hidden="true"><use href="#i-trending-up"/></svg>+12.4% vs October</p></div>
</div>
```

`stat__delta--down` for a drop, `.stat__meta` for a footnote.

**Description list.** `<dl class="dl"><div><dt>Customer</dt><dd>Northwind Traders</dd></div><div><dt>Placed</dt><dd>14 Nov 2026, 09:42</dd></div></dl>`.

**List.** For mobile screens and short collections: `<ul class="list"><li><a class="list__item" href="#/orders/detail?id=1"><span class="avatar avatar--sm">NT</span><div class="list__body"><p class="list__title">Northwind Traders</p><p class="list__meta">3 items · €1,240.00</p></div><span class="badge badge--success">Paid</span></a></li></ul>`. (The `<li>` may be the `.list__item` itself when it is not a link.)

**Charts.** Real proportions only, from the sample data:

- `<div class="meter" role="progressbar" aria-valuenow="72" aria-valuemin="0" aria-valuemax="100" aria-label="Storage used"><span style="--value:72%"></span></div>`; `--success`, `--warning`, `--danger`.
- Bars: `<div class="bars" role="img" aria-label="Orders per day, last 7 days: Mon 34 … Sun 12"><div class="bars__item"><span class="bars__bar" style="--value:68%" title="Mon: 34"></span><span class="bars__label">Mon</span></div>…</div>`; `.bars__bar--muted` for a comparison series.

**Pagination.** `<nav class="pagination" aria-label="Pagination"><p class="pagination__info">Showing 1–25 of 312</p><div class="pagination__pages"><a class="pagination__item" aria-disabled="true" aria-label="Previous page"><svg class="icon icon--sm" aria-hidden="true"><use href="#i-chevron-left"/></svg></a><a class="pagination__item" href="#/orders" aria-current="page">1</a><a class="pagination__item" href="#/orders">2</a>…</div></nav>`.

**Steps.** For a multi-step flow: `<ol class="steps"><li class="steps__item steps__item--done">Cart</li><li class="steps__item" aria-current="step">Delivery</li><li class="steps__item">Payment</li></ol>`.

**Dropdown menu.**

```html
<details class="menu">
  <summary class="btn btn--ghost btn--icon" aria-label="Order actions"><svg class="icon" aria-hidden="true"><use href="#i-ellipsis-vertical"/></svg></summary>
  <div class="menu__list" role="menu">
    <a class="menu__item" role="menuitem" href="#/orders/edit?id=1"><svg class="icon" aria-hidden="true"><use href="#i-pencil"/></svg>Edit</a>
    <hr class="divider">
    <button type="button" class="menu__item menu__item--danger" role="menuitem" data-open-dialog="delete-order"><svg class="icon" aria-hidden="true"><use href="#i-trash-2"/></svg>Delete</button>
  </div>
</details>
```

`.menu--start` opens it to the right of a left-aligned trigger. `.divider` is a rule; `.divider--vertical` inside a row.

### Icons

`<svg class="icon" aria-hidden="true"><use href="#i-NAME"/></svg>`; `icon icon--sm` for a smaller one. An icon next to text is decorative (`aria-hidden`); an icon-only control carries `aria-label`. Icons inherit the text colour. Only these names exist:

house, layout-dashboard, menu, panel-left, chevron-left, chevron-right, chevron-down, chevron-up, arrow-left, arrow-right, arrow-up-down, external-link, plus, minus, pencil, trash-2, copy, download, upload, search, funnel, sliders-horizontal, settings, ellipsis, ellipsis-vertical, x, check, refresh-cw, log-out, log-in, send, share-2, save, printer, history, user, users, user-plus, building-2, briefcase, store, calendar, clock, mail, phone, smartphone, map-pin, file, file-text, folder, image, camera, credit-card, shopping-cart, package, truck, tag, bell, message-square, star, heart, bookmark, lock, lock-open, eye, eye-off, shield, key, link, paperclip, layers, chart-column, chart-line, chart-pie, trending-up, trending-down, dollar-sign, wallet, receipt, clipboard-list, list, grid-3x3, kanban, inbox, archive, circle-help, info, triangle-alert, circle-alert, circle-check, circle-x, loader-circle, sun, moon, globe, wifi-off

### Runtime helpers

The runtime implements these; write the attributes, never the script.

- **Links**: `href="#/<route>"` to a planned route; a detail route may add a query, `#/orders/detail?id=3`.
- **Dialogs**: `data-open-dialog="<dialog id>"` on a button opens that `<dialog>`; `data-close-dialog` on an element inside a dialog closes it.
- **Roles**: `data-only-roles="slug slug"` shows an element only to those roles; `data-hide-roles="slug"` hides it from them. Use the exact role slugs.
- **Tabs**: a `data-tabs` container whose `role="tab"` buttons point at their panels with `aria-controls`; the selected tab has `aria-selected="true"`, the other panels `hidden`.
- **States**: the reviewer switches `data-state` blocks from the control bar; write each block complete.
