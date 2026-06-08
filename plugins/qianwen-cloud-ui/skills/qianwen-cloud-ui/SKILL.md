---
name: qianwen-cloud-ui
description: "Use when designing or implementing Qianwen Cloud / 千问云 / 千问工作台 2.0 style console, admin, analytics, billing, API key, settings, alert, drawer, dialog, popover, table, chart, or docs pages. Applies the observed Qianwen Cloud console and documentation visual system: pale gray workspaces, data-rich white cards, compact tables, capsule filters, black CTAs, purple states, restrained charts, blurred overlays, 420px drawers, and documentation reading layouts."
---

# qianwen-cloud-ui

## Direction

Build desktop-first Qianwen Cloud style product interfaces: calm, data-dense, operational pages on a pale gray workspace, with white rounded business surfaces, capsule controls, compact tables, subdued chart colors, black primary actions, purple selected/focus/link states, and blurred high-elevation overlays.

Use this skill for backend/admin/console/documentation pages, not marketing landing pages. Do not copy the Qianwen logo files, screenshots, real account names, emails, bills, API keys, invoice data, or any private data observed in a browser. Use masked and synthetic values in examples.

## Workflow

1. Reuse the app's existing framework, router, icons, table, form, drawer, dialog, and chart primitives.
2. Choose the surface type first: console workspace, data dashboard, resource table, settings form, overlay flow, or documentation page.
3. Build the shell before content: sidebar/topbar for console pages; top nav + doc sidebar + reading panel for docs pages.
4. Add real data states: filled, loading, empty, error, disabled, selected, expanded row, and overlay-open states.
5. Keep the style quiet. Use black for the main command, purple for interaction state, gray for structure, and charts as light analytical surfaces.
6. Validate desktop first. The observed console is desktop-oriented; below 1024px, prefer a compact unsupported/hand-off state unless the user explicitly asks for a full mobile version.

## Design Tokens

Map to local tokens or CSS variables. If the project uses Tailwind, use arbitrary values or theme aliases that preserve these exact colors.

```css
:root {
  --qw-bg: #f9fafd;
  --qw-card: #ffffff;
  --qw-muted-surface: #f2f4f8;
  --qw-selected-surface: #e6e9ef;
  --qw-line: #e6e9ef;
  --qw-line-strong: #d1d7e2;
  --qw-text: #0b0c0f;
  --qw-text-soft: #111317;
  --qw-text-muted: #535b6b;
  --qw-text-faint: #7f8798;
  --qw-disabled: #9fa7b7;
  --qw-primary: #5b58ff;
  --qw-primary-hover: #4500f3;
  --qw-primary-soft: #f0f3ff;
  --qw-primary-lighter: #e7eaff;
  --qw-primary-chart: #afb9fd;
  --qw-danger: #f33939;
  --qw-success: #0da740;
  --qw-warning: #ff7931;
  --qw-blue: #277fe4;
  --qw-purple-tint: #653aff;
  --qw-shadow-light: 0 8px 24px rgba(83, 91, 107, 0.06);
  --qw-shadow-normal: 0 16px 40px rgba(83, 91, 107, 0.10);
}
```

Source token mapping when available:

- `--pt-color-neutral-50` = `#ffffff`, `100` = `#f9fafd`, `150` = `#f2f4f8`, `200` = `#e6e9ef`, `300` = `#d1d7e2`, `650` = `#535b6b`, `950` = `#0b0c0f`.
- `--pt-color-primary-50` = `#f0f3ff`, `150` = `#e7eaff`, `250` = `#d1d7ff`, `350` = `#afb9fd`, `550` = `#5b58ff`, `650` = `#4500f3`.
- Supporting tints: red `#fff2f0/#f33939`, green `#ecfaed/#0da740`, orange `#fff5eb/#ff7931`, blue `#edf4fd/#277fe4`, purple `#f2effc/#653aff`.

Typography:

- Font family: `Inter`, `PingFang SC`, `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, `Roboto`, `Helvetica Neue`, `Arial`, `Noto Sans`, sans-serif.
- Code/API values: `RobotoMono`, `Consolas`, `Monaco`, monospace.
- Console page title: 28px / 36px, weight 600, color `#0b0c0f`.
- Docs H1: 36px / 46px, weight 600; docs H2: 28px / 36px, weight 600.
- Section title: 20px / 30px, weight 600.
- Body/help text: 14px / 20px, letter spacing about 0.4px, muted `#535b6b` or `#7f8798`.
- Controls and tables: 13px / 20px.
- Table headers/captions: 12px / 16px, muted.
- KPI numbers: 36px / 44px, weight 600 or 700.

## Console Shell

- Body/workspace: `#f9fafd`, no full-page outer card.
- Sidebar: 272px wide, full height, transparent on the workspace. Top logo area aligns to a 84px topbar.
- Sidebar item: 224px wide, 36px high, x padding about 40px for icon rows, 14px text, 10px icon/text gap.
- Selected sidebar item: capsule `#e6e9ef`, radius 999px, font-weight 500.
- Nested sidebar group: indented child links, 36px high, thin vertical guide line at the left of child items.
- Bottom workspace switcher: pinned to sidebar bottom; opened menu is about 160px wide, white, 24px radius, shadow normal, current row with checkmark and a management link.
- Topbar: 84px high, transparent, right aligned global links, 14px text, avatar as a round gradient button.
- Main: starts at x = 272px and y = 84px, scrolls independently. Let the first page title start at the main edge, then give cards 28px inner padding.

## Core Components

### Cards

- Standard console card: white, 24px radius, 28px padding, no hard border, usually no shadow.
- Dense table card: white, 24px radius, 28px outer padding, inner table may touch horizontal width with only cell padding.
- KPI card: white, 24px radius, 28px padding, optional faint grid/fade background on the right.
- Hero/banner card: 24px radius, pale blue/purple background art or gradient fade, text left, secondary button right.
- Docs cards: 16px radius, white, compact 24px inner rhythm; use inside the docs reading panel.
- Avoid cards inside cards unless the inner surface is a real data table, code block, or selectable resource tile.

### Tabs And Segmented Controls

- Tablist container: capsule, white or transparent, 36-40px high.
- Trigger: 32px high, 13px text, horizontal padding 24px, radius 999px.
- Selected: `#f2f4f8`, weight 500.
- Analytics table sub-tabs may sit inside chart panels as 32px pills with small info icons.

### Filters And Inputs

- Select/date/filter trigger: 36px high, radius 999px, `1px #e6e9ef`, transparent background, 13px text.
- Search input: 36px high, radius 999px, `#e6e9ef` border, search icon at left, placeholder `#7f8798`, width 276-360px in table toolbars.
- Read-only URL/API field: 40px high, radius 999px, `#e6e9ef` border, label prefix inside the capsule, copy icon at right.
- Form input in dialogs/drawers: 40-48px high, radius 999px, `#e6e9ef` border, 14px text; focus border/ring purple `#5b58ff`.
- Select popover: white, 24px radius, shadow normal, z-index around 1200; options are 36px rows with 12px radius hover/selected fill.
- Date quick picker: 488px wide, 24px radius, 12px padding, shadow normal; top has a capsule segmented control, then the range field, then 2 rows of quick buttons. Selected quick range uses `#f0f3ff` with purple text.

### Buttons

- Primary action: black `#0b0c0f`, white text, 36px or 40px high, radius 999px, 14px/500, horizontal padding 18-20px.
- Primary hover: purple `#5b58ff`.
- Disabled primary: `#9fa7b7`, white text, no hover.
- Secondary: white/transparent, `1px #d1d7e2`, black text, radius 999px.
- Link/text action: purple `#5b58ff`, no border, 13px/20px in tables.
- Danger text: red `#f33939`; avoid red filled buttons unless destructive emphasis is explicitly requested.
- Icon-only: 28-36px round buttons with neutral icon color; use lucide or the existing icon set.

### Tables

- Table header: 40px high, `#f9fafd` background, 12px muted text, no heavy border.
- Body row: about 52px high, 13px text, white/transparent, subtle separators.
- Cell padding: 8-16px horizontal depending density. Keep IDs/API keys monospace and masked.
- Row actions: purple text for view/edit, red text for delete.
- Switches: 32x16px, selected fill `#5b58ff`, white thumb.
- Expandable rows: chevron at first cell. Expanded content uses 12px-radius light panels (`#f2f4f8` or `neutral-150/30`) with chart tabs and loading/empty states.
- Empty table: centered icon, short title such as "暂无数据", muted help text, optional black or purple creation action.

### Metrics And Charts

- Chart surfaces are mostly white space with light grid lines. Do not saturate the card.
- Main line/area chart: line `#afb9fd`, pale primary area fill, optional diagonal stripe mask, axis labels `#535b6b`, grid `#e6e9ef`.
- Bar chart: use `#e7eaff` or `#d1d7ff` for normal bars; active/current bar can use `#5b58ff` with diagonal stripe texture and a purple value pill.
- KPI deltas: green `#0da740` for improvement, red `#f33939` for regressions or bad movement. Use small arrows and muted percent text.
- Multi-metric dashboard: one large chart card on the left and four 2-up KPI cards on the right at wide widths; collapse to stacked rows only if mobile is required.
- Expanded table charts: two side-by-side chart panels, each light gray, 12px radius, 12px padding, tabs at top, spinner centered during loading.
- Chart palette order for multiple series: `#5b58ff`, `#14c8c7`, `#277fe4`, `#0da740`, `#ff7931`, `#f33939`, with muted alpha fills.

## Overlays

### Dialogs

- Standard creation dialog: 480px wide for simple forms; 608px for complex multi-section forms.
- White, 24px radius, 28px padding, `0 16px 40px rgba(83,91,107,.10)`.
- Backdrop: strong blur over the page with very light translucent wash; the underlying page should be readable only as blurred context.
- Header: title 20px/30px/600, description 14px muted.
- Section dividers: pale horizontal rules.
- Footer: right aligned secondary + primary/disabled primary.
- Alert/advice box inside dialogs: 12px radius, 1px `#d1d7e2`, icon + text, purple inline links.

### Right Drawers

- Width: 420px for most forms.
- White, 24px radius, 28px padding, shadow normal.
- Top aligned with viewport or below topbar depending route; content scrolls inside the drawer.
- Title + muted description, then form sections.
- Footer actions fixed at bottom: secondary cancel + primary save/submit, right aligned.
- Use drawer for editing API keys, workspaces, alert rules, billing/invoice details, or long forms.

### Menus And Popovers

- Avatar menu: 304-320px wide, white, 24px radius, shadow normal, right aligned below avatar.
- Avatar menu top card: gradient avatar, masked email/account label, spending or account summary, small orange/purple status pill if needed. Never show real private values in examples.
- Avatar menu item: 48px high, icon + label, muted hover, logout as neutral text unless destructive confirmation is needed.
- Workspace menu: 160-200px wide, white, 24px radius, shadow normal; current space gets a checkmark.
- Notification/toast: white, 24px radius, shadow light/normal, concise title + action.

## Page Patterns

### Home Dashboard

- Top: "欢迎使用..." heading, then a full-width quick-link card with six evenly spaced icon+label links.
- Next row: benefits card, recent spend card, usage card. Use 24px radius and 28px padding.
- Benefits card may include a pale grid illustration or light blue/purple promotion strip.
- Usage card uses a simple bar mini-chart; active bar is purple and labeled.
- Learning/resource cards: 4-column, 16-18px radius, light border, icon badge at top right.
- Model cards: image/gradient media strip at top, white content, model ID copy pill, price/spec rows, black primary action + secondary API request.

### Analytics Usage

- Heading + muted subtitle, then tabs "用量/日志".
- Filter row: date range, model select, granularity select.
- At wide desktop: large chart card left; four KPI cards in a 2x2 grid right.
- Under metrics: full-width model table card. Each model row can expand into detailed charts.
- Include loading, empty, and partial-data states; use dashes for unavailable KPI values, not zero.

### Request Logs

- Same heading/tabs/filter language as usage.
- Toolbar should support request ID/model/status/date filters and search.
- Table columns should be compact and scannable: time, model, request ID, status, latency, tokens/cost, action.
- Use status pills with supporting tints. Avoid large colored rows.
- Empty state should explain that logs appear after API requests, with a link-style docs action.

### Billing And Payments

- Overview: summary spending cards first, then trend chart/table by day or product.
- Pay-as-you-go: balance/recharge card, spend trend, usage or transaction details.
- Token Plan: subscription/plan cards with a pale promotional background, plan comparison rows, black subscription CTA.
- Invoice: tabs or route segments for apply/history/title management; use table + form cards and disabled submit until valid.
- Money values in examples must be synthetic; never copy observed amounts.

### API Key Management

- Page title + subtitle.
- Top promotional banner for Token Plan or docs, 24px radius, pale blue/purple art on right, secondary capsule action.
- Base URL section: two read-only URL capsules, each with a prefix label and copy icon.
- Main card: search input left, black "创建 API Key" right, compact table below.
- API keys must be masked, e.g. `sk-a****1234`; use monospace.
- Row actions: view cost/edit purple, delete red, enabled switch purple.
- Create dialog: 480px, description input, character counter, advice box, disabled "生成 API Key" until description is valid.

### Settings And Alerts

- Settings overview: account/space cards first, then full-width settings rows about 108px high with icon, title, description, and chevron.
- Account page: profile/security cards, masked identity info, secondary edit buttons.
- Workspace page: search/create toolbar + table; drawer for create/edit workspace.
- Alerts page: segmented tabs for rules/templates/history, filter row, table or empty state, black create button.
- Alert rule drawer: 420px, sectioned form, model selector, thresholds, notification method, fixed footer.

### Model Production

- Use a product capability overview, not a marketing hero.
- Cards should describe datasets, fine-tuning, evaluation, deployment, and job history.
- Use empty states and disabled actions for unavailable capabilities.
- Keep icons monochrome or lightly tinted; avoid large illustrations unless a real workflow needs them.

### Support

- Support index/list should be sparse: ticket list or category cards, black create/contact action, status pills.
- Form flows use right drawer or centered dialog depending complexity.

## Documentation Pages

Use this pattern for `platform.qianwenai.com/docs` style pages or in-app docs/help surfaces.

- Page background: white around a central pale reading panel.
- Top nav: logo/breadcrumb left, product/doc nav right, black "工作台" pill button.
- Search trigger: 228px x 48px capsule, `#d1d7e2` border, search icon left, keyboard hint right.
- Left docs sidebar: about 264px wide, padding-right 24px, section labels, nested lists, 14px text, active item purple with a dot/guide line.
- Expandable nav item: chevron at right; expanded state inserts nested list under the item with indented links.
- Main reading panel: pale `#f9fafd`, 36px radius, 40px top/bottom and 80px horizontal padding at desktop.
- Article width: about 1032px; lead paragraph 16px/24px; links purple and underlined only when useful.
- Code block: outer white card, 12px radius, `1px #d1d7e2`; inner `#f9fafd` code surface, 12px radius, 16px padding; copy button in the top right.
- Docs cards: 3-column model cards or 2-column guide cards, white, 16px radius, 24px padding, small icon top left, external/open icon top right.
- Prev/next navigation: white, 18px radius, 8px padding, two columns where applicable.
- Footer is allowed on long docs pages; keep it outside the pale reading panel.

Docs search overlay:

- Center panel: about 580px wide, white, 24px radius, shadow normal, strong blurred backdrop.
- Search input: 556px wide, 48px high, capsule, gradient purple/cyan focus border, search icon left, `ESC` hint right.
- Result item: 556px wide, about 98px high, 12px radius, 12px padding, icon + title + snippet + breadcrumb; selected/hover fill `#f9fafd`.

## Implementation Notes

- Prefer local component primitives. If Ant Design is used, override locally with wrapper classes.
- If Tailwind is available, map directly: `bg-[#f9fafd]`, `rounded-[24px]`, `p-7`, `text-[13px]`, `h-9`, `rounded-full`.
- Use the existing icon library. If none exists, use lucide icons for sidebar, copy, search, calendar, chevron, settings, info, close, empty state, and table actions.
- Use the project chart library. Do not hand-roll axes unless there is no chart primitive.
- Keep visible copy operational and concise. Do not add instructional text for obvious controls.
- For mock data, include enough rows and non-zero metrics to demonstrate layout density; mask IDs, emails, keys, and billing values.
- Do not use oversized marketing heroes, decorative orbs, single-hue purple pages, heavy gradients, or nested decorative cards.

## Quality Checklist

- Console shell uses 272px sidebar, 84px topbar, `#f9fafd` main background.
- Page title is 28px/600; subtitle is muted 14px.
- Primary surfaces are white 24px cards with 28px padding.
- Filters, tabs, selects, dates, buttons, and search are capsule-shaped.
- Data pages include real filled, loading, empty, selected, and expanded-row states.
- Tables use 13px body, 12px header, 40px header rows, compact row actions, and masked sensitive values.
- Charts use light grid lines, pale purple/blue fills, and restrained deltas.
- Primary action is black; hover/focus/links/selected states are purple; destructive text is red.
- Dialogs/popovers use 24px radius, shadow normal, and blurred page backdrops.
- Drawers are 420px wide with fixed action footers.
- Docs pages use the pale 36px reading panel, 264px sidebar, 12px code blocks, and 580px search overlay.
- No real Qianwen account data, invoice data, API keys, screenshots, or private browser content appears in generated UI.
