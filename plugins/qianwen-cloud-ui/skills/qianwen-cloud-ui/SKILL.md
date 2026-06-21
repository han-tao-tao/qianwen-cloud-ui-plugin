---
name: qianwen-cloud-ui
description: "Use when designing or implementing Qianwen Cloud / 千问云 / 千问工作台 2.0 style console, admin, analytics, billing, API key, settings, alert, drawer, dialog, popover, table, status tag, sidebar icon, tab switch, chart, or docs pages. Applies the observed Qianwen Cloud console and documentation visual system: pale gray workspaces, data-rich white cards, compact tables, capsule filters, compact status tags, line sidebar icons, black CTAs, purple states, restrained charts, blurred overlays, 420px drawers, and documentation reading layouts."
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
  --qw-menu-hover-surface: #f2f4f8;
  --qw-menu-selected-surface: #e6e9ef;
  --qw-menu-text: #1d2129;
  --qw-menu-icon: #535b6b;
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
  --qw-status-success-bg: #ecfaed;
  --qw-status-warning-bg: #fff5eb;
  --qw-status-danger-bg: #fff2f0;
  --qw-status-info-bg: #edf4fd;
  --qw-status-neutral-bg: #f2f4f8;
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
- Sidebar scroll area begins below the topbar at y = 84px, has `mx-3`/12px outer gutter, inner nav width 224px, and 4px vertical item gap.
- Top-level sidebar item: 224px wide, 36px high, radius 12px, 14px / 20px text, weight 400, letter spacing 0.4px, menu text about `#1d2129`, `10px 10px 10px 40px` padding, 10px icon/text gap. Avoid using pure-looking black for long menu lists.
- Selected child sidebar item: 173px wide, 36px high, capsule `#e6e9ef`, radius 999px, font-weight 400, text about `#1d2129`, icon about `#535b6b`. Do not bold selected child labels or icons; the selected capsule is the state indicator.
- Nested sidebar group: x about 45px, width 194px, top margin about 4px, `2px 10px` inner padding, 4px row gap, thin left border `#e6e9ef`; nested links are 173px x 36px with 8px radius unless selected. Tune the actual margin to hit x≈45 in the host framework instead of blindly stacking parent indentation.
- Nested sidebar item content must be left aligned inside its 173px row/capsule. If the framework auto-adds level padding or uses a centered absolute trigger, reset the child item/trigger padding so the label does not drift right in the selected capsule.
- Active/open parent rows, child rows, labels, icons, and chevrons stay regular weight. Never use font-weight >400 in the sidebar just to show selected/open state.
- Collapsed-sidebar affordance: bottom-right 36px round icon button, transparent background, 20px line icon, neutral text/icon color.
- Bottom workspace switcher: pinned to sidebar bottom, trigger 188px x 36px, transparent capsule, `8px 10px` padding, 6px gap. Avatar tile is 24px square, 8px radius, dark `#1d2129`, white 16px/600 initial; label is 14px/500 truncated to about 112px.
- Workspace menu: 160px wide, white, 24px radius, 12px padding, 8px gap, shadow normal, z-index about 1150. Current workspace row is 136px x 40px, capsule `#f2f4f8`, 14px/500; management link row is 136px x 40px, purple `#5b58ff`, 18px icon, separated by a `#e6e9ef` top rule.
- Topbar: 84px high, transparent, right aligned global links, 14px text, avatar as a round gradient button. Keep it clean: do not show old route breadcrumb chips or multi-page tabbar tags in the topbar unless the product explicitly asks for that workflow.
- Main: starts at x = 272px and y = 84px, scrolls independently. Let the first page title start at the main edge, then give cards 28px inner padding.

## Core Components

### Content Width And Alignment

- Standard home/dashboard/settings workspaces use a centered content rail, not a left-pinned panel. The observed Qianwen Cloud home page uses `max-w-[1600px] mx-auto` inside the main area; at a 2560px viewport with a 272px sidebar, the content rail is 1600px wide and centered in the remaining workspace.
- Cards inside that standard rail are full width of the rail: broad cards are about 1576px after the page's right padding, and 3-column cards are equal columns inside the same rail. Do not invent page-specific widths such as 920px for ordinary settings pages.
- Single settings/configuration pages should follow the same centered 1600px rail with one white 24px panel unless the content is genuinely a small dialog/drawer flow. The panel can have sparse content, but the page container should stay consistent with other Qianwen workspace pages.
- Dense analytics/request-log table pages are the exception: they use the available content width directly so wide tables can scan and scroll horizontally. Do not constrain request-log-like tables to the 1600px home rail.
- Keep one width policy per surface type. Avoid making every page a different card width; use centered 1600px for home/settings/card dashboards and full available width for dense table/log pages.

### Cards

- Standard console card: white, 24px radius, 28px padding, no hard border, usually no shadow.
- Dense table card: white, 24px radius, 28px outer padding, inner table may touch horizontal width with only cell padding.
- KPI card: white, 24px radius, 28px padding, optional faint grid/fade background on the right.
- Hero/banner card: 24px radius, pale blue/purple background art or gradient fade, text left, secondary button right.
- Docs cards: 16px radius, white, compact 24px inner rhythm; use inside the docs reading panel.
- Avoid cards inside cards unless the inner surface is a real data table, code block, or selectable resource tile.

### Tabs And Segmented Controls

- Route-level tablist container: capsule, white, 40px high, `0 4px` padding, width fits content. Do not use underlines or colored bars for console page tabs.
- Route-level tab trigger: 32px high, 13px / 20px text, letter spacing 0.4px, `4px 24px` padding, radius 999px, transparent border, neutral `#111317`; selected trigger uses `#f2f4f8` background and font-weight 500.
- Framework route tabbars, browser-like page tags, and breadcrumb bars are not Qianwen console shell chrome. Disable or restyle them away when rebuilding a global admin shell unless the user explicitly wants multi-page tabs.
- Panel/detail segmented tablist: capsule `#f2f4f8`, 40px high, `0 4px` padding. Selected trigger is white, unselected trigger is transparent; same 32px trigger height and 13px text.
- Analytics table sub-tabs may sit inside chart panels as 32px pills with small info icons.

### Sidebar And Utility Icons

- Use the product's existing icon component set. If a project has no icon library, use lucide icons with the same geometry.
- Sidebar icons are monochrome line icons, 20px square, `stroke: currentColor`, no fill, neutral gray such as `#535b6b`, flex-shrink allowed, aligned at x padding 40px. Do not make sidebar icons bold, filled, scaled on hover, or pure black; they should read lighter than primary text.
- Expand/collapse chevrons in grouped menu items are 16px square line icons, right aligned near the item edge.
- Popover and workspace utility icons are 18px square; the management link icon uses purple `#5b58ff`, while current-item/check icons stay neutral.
- Collapse-sidebar control uses a 20px line icon inside a 36px round transparent button.
- Reasonable lucide mapping: `Home`, `Sparkles` or `Bot` for model experience, `BarChart3` for analytics, `CreditCard` or `WalletCards` for billing, `Factory` or `Boxes` for model production, `KeyRound` for API keys, `Settings` for settings, `User`, `BriefcaseBusiness`, `Bell`, `ChevronDown`, `PanelLeftClose`, `Check`, and `ExternalLink`.
- Small promotional nav badges such as "Hot" should stay tiny: about 20px high, 12px / 16px text, 999px radius, compact horizontal padding. They should not compete with selected navigation state.

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

### Status Tags And Badges

- Table status tags should match the request-log status style: `inline-flex`, 22px high, `2px 10px` padding, radius 999px, 12px / 16px text, font-weight 400, letter spacing 0.4px, no shadow, and a transparent 1px border.
- Do not use large, bold, saturated, or square status labels. Avoid default framework tags such as solid Ant Design green/red pills unless they are restyled to this scale.
- HTTP 2xx / success: background `#ecfaed`, text `#0da740`, label can be the numeric code such as `200`.
- HTTP 0 / interrupted or unknown-but-not-error: background `#f2f4f8`, text `#535b6b`.
- HTTP 3xx / informational: background `#edf4fd`, text `#277fe4`.
- HTTP 4xx / user-caused exception: background `#fff5eb`, text `#ff7931`.
- HTTP 5xx / service unavailable: background `#fff2f0`, text `#f33939`.
- Status filter trigger: 200px wide, 36px high, radius 999px, transparent background, `1px #e6e9ef`, 13px / 20px text, 0.4px letter spacing, left padding 6px and right padding 12px. Expanded/focused border becomes `#5b58ff`.
- Status filter popover: 300px wide, white, 24px radius, shadow normal, z-index about 1150. Inner scroll area uses 12px padding and up to 280px height.
- Status filter option row: 276px x 36px, radius 999px, 14px / 20px text, `0 12px` padding, 16px gap, hover `#f9fafd`, selected `#f2f4f8`.
- Multi-select checkbox inside option rows: 16px square, 6px radius, inset `1px #d1d7e2`; selected state should use primary purple, not a separate brand color.

### Tables

- Put dense data tables inside a white 24px card with 28px padding. The table itself sits in a `relative w-full overflow-x-auto` wrapper; use `border-collapse: collapse`, no outer table border, no zebra stripes, and no card-within-card treatment.
- For request-log-like pages, do not merely repaint Ant/Vben table chrome. Build or override down to the data-surface level so the visible result is a native-looking table: one white 24px panel, one filter toolbar, one `table`-like grid, no framework title bar, no boxed toolbar, no column-setting buttons, no thick grid borders, and no nested table card.
- Table header row: 40px high with a `#e6e9ef` bottom rule. Header cells use `#f9fafd` background, 12px / 16px text, weight 400, `#535b6b`, 0.4px letter spacing, left alignment, `0 8px` padding, nowrap. Do not uppercase, bold, center, or add strong grid lines.
- Body rows: transparent/white by default with a `#e6e9ef` bottom rule and hover/selected fill `#f2f4f8`. Base text is 13px / 20px, weight 400, `#0b0c0f`, 0.4px letter spacing. Use 8px cell padding for request-log density.
- A selected/active row in the live request-log table uses a full-row neutral fill close to `#f2f4f8`, while the sticky action column stays visually fused with that row. Avoid separate selected-cell outlines.
- Row height is content-driven. Simple rows can be about 52px, but request-log rows with 3 usage lines should be about 81px; rows with an extra usage line such as image/cached/reasoning tokens may reach about 103px. Do not force fixed 52px rows when metric stacks need space.
- Request-log column order should be: `Request ID`, `创建时间`, `模型`, `请求来源`, `API Key`, `用量`, `首包延迟`, `延迟`, `状态`, `操作`. At wide desktop, let the table grow horizontally and scroll instead of squeezing cells.
- Width rhythm for request-log tables: Request ID/API Key min 140px and max about 225px for constrained layouts, Request ID may expand wider in open desktop tables; time about 300px column with 13px timestamp; model about 300px; source about 130px; usage about 260px; first-byte latency about 130px; total latency about 105px; status about 120px; action about 100px.
- Keep the right action column sticky: `position: sticky; right: 0; z-index: 10`; header uses the same `#f9fafd` background, body cells stay transparent/white, and action cells use left padding about 16px.
- ID and API key cells: render as a single-line flex row with 4px gap. The value is 12px / 16px monospace, truncated with ellipsis, masked in examples. The copy affordance is a 24px round icon-only target, transparent, neutral `#7f8798`, with a 14px copy icon and no visible button border.
- Model cells: use a 16px inline model/vendor icon, 4px gap, then a 13px / 20px truncated model name in `#111317`. Keep icons monochrome or native tiny product icons; do not turn model names into colored badges.
- Usage cells: never collapse usage into one number. Use a vertical stack with 2px row gap; each usage line is 20px high. Labels use 13px / 20px, weight 400, `#3c424f`; values use 13px / 20px, weight 600, `#111317`. Order common lines as `全部 Token`, `输出 Token`, `输入 Token`, then optional extra lines such as `图片 Token`, cached tokens, reasoning tokens, audio/video tokens, or other model-specific usage subfields.
- Latency cells are plain text, not tags. Use `-` for unavailable first-token latency, and values like `8.09s` for total duration. Avoid warning colors unless the product explicitly defines an SLA state.
- Row actions: table detail/view actions are 13px / 20px, weight 400, purple `#5b58ff`, transparent background, no border, no underline, zero extra padding, and about 20px high. Destructive text stays red.
- Switches: 32x16px, selected fill `#5b58ff`, white thumb.
- Expandable rows: chevron at first cell. Expanded content uses 12px-radius light panels (`#f2f4f8` or `neutral-150/30`) with chart tabs and loading/empty states.
- Pagination: right align below the table as a compact `nav[aria-label="pagination"]`, not as a left/right split footer. The observed request-log pagination uses a full-width footer row with `justify-end`; the nav itself is `w-fit`, 30px high, with `ul` gap about 8px.
- Pagination page/arrow targets are 30px round buttons, 13px / 20px text, font-weight 400, transparent by default, active/current fill `#f2f4f8`, text `#111317`, and neutral arrow/icon color about `#8e96a7`; disabled arrows can use `#d1d7e2`.
- Pagination ellipsis is a centered 30px target with a 16px neutral three-dot icon. Avoid rendering raw `...` text that sits off baseline.
- Request-log-style table pagination does not show "共 x 条", page-size selectors, boxed square controls, or Ant/Vben pagination chrome unless the host product explicitly requires those controls.
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
- Avoid default Ant/Vben modal masks and default modal chrome when the request asks for Qianwen overlay fidelity. Use a custom overlay class or custom dialog shell so the mask is a pale blurred wash, the panel is a clean 24px white surface, and the footer uses Qianwen capsule buttons rather than framework square/blue defaults.
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

- Use the standard centered 1600px content rail. Qianwen Cloud home is a wide centered workspace, not a left-pinned settings panel.
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
- Above the table, include the retention note as muted 14px text, then a filter toolbar inside the same white card. Keep filter controls 36px high and capsule-shaped: date range min about 280px, model/API key comboboxes, source select 160px, status multi-select 200px, Request ID input 220px, and a secondary "导出" button 36px high.
- In the observed request-log screen, the table card starts directly below the retention note, spans the available content width, and keeps the export button far right on the same toolbar row as filters. Do not insert a separate page-section header or framework table title inside this card unless the product asks for one.
- Columns should follow the observed order exactly: `Request ID`, `创建时间`, `模型`, `请求来源`, `API Key`, `用量`, `首包延迟`, `延迟`, `状态`, `操作`. This order matters for scan speed; do not move status/action before the usage and latency columns.
- Request ID and API Key cells should show a masked/truncated monospace value plus a small neutral copy icon. Do not render full IDs in examples and do not use large copy buttons.
- The usage column is a compact vertical metric stack, not a chip group. Show token submetrics as label/value pairs: `全部 Token 12345`, `输出 Token 678`, `输入 Token 11667`, plus optional `图片 Token`, cached, reasoning, or other modality/token lines when present. This is the main request-log data-processing display.
- Status column should use compact HTTP-code tags: 22px-high 12px text, numeric code label, success `#ecfaed/#0da740`, 4xx `#fff5eb/#ff7931`, 5xx `#fff2f0/#f33939`, neutral/interrupted `#f2f4f8/#535b6b`.
- The status filter should read as a 36px capsule control and open a 300px white 24px-radius popover. The trigger border turns purple `#5b58ff` while open. Options are text rows with small checkboxes, not colored tags.
- Status filter options should use 276px x 36px rows, `0 12px` padding, 8px gap, 14px / 20px text, and neutral text. Include labels like `请求成功但用户主动中断 (0)`, `成功 (200)`, `用户行为导致的异常 (4XX)`, and `服务不可用 (5XX)`.
- Option checkboxes are 16px squares with 6px radius and an inset `#d1d7e2` outline. Selected state uses the product primary purple; avoid framework default blue checks.
- The "详情" action opens a right request-detail panel rather than a table expansion. Use a 420px white panel aligned from the 84px topbar to near the bottom, 24px radius, 28px padding, z-index about 900, and no oversized shadow.
- Request-detail panel header: title 20px / 30px / 600, muted 14px description, and a 20px close icon button. Below it, use a 40px `#f2f4f8` capsule tablist with `列表` and `Json`; selected tab is white, 32px high, 13px / 20px / 500.
- Detail list rows are 40px high with `#e6e9ef` bottom rules. Left label column is 140px, 13px / 20px, `#7f8798`; right value area is flex, 13px / 20px, `#111317`, with monospace for Request ID and compact status tags for status code.
- Detail Json tab uses a scrollable transparent code surface, not a dark editor. Use `RobotoMono`, 12px / 16px, 0.4px letter spacing, `pre-wrap`, break long words, and keep the panel width at 364px inner content. Mask or synthesize payload fields in examples.
- Avoid large colored rows, oversized badges, bold labels, or high-saturation status colors in request-log tables.
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

- Settings/configuration pages use the standard centered 1600px content rail with a single broad white panel when the content is a page-level configuration, matching the home workspace alignment. Do not use arbitrary narrow centered cards or left-aligned full-width panels for ordinary setting pages.
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
- Console shell does not show legacy breadcrumb chips or multi-page tabbar tags unless explicitly requested.
- Sidebar menu text/icons are regular weight, not overly black, and selected child labels are left aligned inside the selected capsule.
- Page title is 28px/600; subtitle is muted 14px.
- Primary surfaces are white 24px cards with 28px padding.
- Filters, tabs, selects, dates, buttons, and search are capsule-shaped.
- Data pages include real filled, loading, empty, selected, and expanded-row states.
- Tables use 13px body, 12px header, 40px header rows, compact row actions, masked sensitive values, and 22px-high 12px status tags.
- Charts use light grid lines, pale purple/blue fills, and restrained deltas.
- Primary action is black; hover/focus/links/selected states are purple; destructive text is red.
- Dialogs/popovers use 24px radius, shadow normal, and blurred page backdrops.
- Drawers are 420px wide with fixed action footers.
- Docs pages use the pale 36px reading panel, 264px sidebar, 12px code blocks, and 580px search overlay.
- No real Qianwen account data, invoice data, API keys, screenshots, or private browser content appears in generated UI.
