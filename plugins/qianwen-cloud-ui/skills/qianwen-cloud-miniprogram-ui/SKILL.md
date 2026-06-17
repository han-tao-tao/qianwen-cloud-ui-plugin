---
name: qianwen-cloud-miniprogram-ui
description: "Use when designing or implementing a Qianwen Cloud / 千问云 / 千问工作台 WeChat Mini Program UI, WXML/WXSS screen, custom component, custom navigation bar, custom tabBar, mobile console, analytics, billing, API key, request log, settings, alert, docs/help, or account/workspace flow. Adapts the qianwen-cloud-ui and qianwen-cloud-mobile-ui visual system to 微信小程序: rpx layouts, app.json/page.json constraints, capsule menu-button avoidance, safe-area-aware custom nav, tabBar/custom-tab-bar, scroll-view lists, WeUI-compatible sheets/dialogs, compact status tags, black CTAs, purple selected/focus states, and synthetic masked cloud-console data."
---

# qianwen-cloud-miniprogram-ui

## Direction

Build WeChat Mini Program-first Qianwen Cloud product interfaces. Preserve the original calm operational style: pale gray workspace, white rounded business cards, black primary actions, purple selected states, compact status tags, masked cloud data, and restrained analytics. Redesign the shell and interactions for the WeChat host instead of copying a native mobile app one-to-one.

Use this skill for WXML/WXSS/JS, Taro, uni-app targeting 微信小程序, native Mini Program custom components, or design specs that will be implemented as a WeChat Mini Program. Do not use it for normal iOS/Android apps unless the user explicitly asks for shared tokens. Do not copy Qianwen logos, screenshots, real account names, real emails, invoice data, API keys, request payloads, or private browser content. Use masked and synthetic examples.

## Workflow

1. Reuse the local Mini Program stack first: native components, WeUI/miniprogram components, Taro/uni-app primitives, chart library, state store, request wrapper, and auth/payment/share utilities already in the project.
2. Choose the page role: tab page, secondary page, detail page, form page, sheet/dialog flow, docs/help page, or reusable component.
3. Decide navigation mode before layout: native nav, `navigationStyle: "custom"`, WeUI `mp-navigation-bar`, or a project custom nav component.
4. Build for the WeChat host chrome: status bar, right capsule menu button, bottom safe area, page stack, share affordance, pull-down refresh, and custom tabBar limitations.
5. Use `rpx` as the primary sizing unit. Treat a 750rpx-wide design as the source of truth and convert compact mobile values carefully.
6. Replace desktop tables with list cards, grouped cells, or detail pages. Avoid horizontal tables on phones.
7. Add filled, loading, skeleton, empty, network error, permission denied, refreshing, disabled, selected, keyboard-open, and overlay-open states.
8. Validate in WeChat DevTools on iPhone 5/SE width, iPhone 6/7/8 baseline, iPhone 14/15 class screens, Android tall screens, and dark/large-font risk states if the project supports them.

## Mini Program Platform Rules

- Prefer `app.json`/`page.json` configuration over JS tricks for navigation, tabBar, pull-down refresh, background color, and page registration.
- Use `navigationStyle: "custom"` only when the page needs a branded Qianwen top bar. Otherwise keep the native navigation bar for simple secondary pages.
- When using a custom nav, get status-bar and capsule metrics with `wx.getSystemInfoSync()` and `wx.getMenuButtonBoundingClientRect()`. Align the title row with the capsule and keep all right-side actions out of the capsule area.
- Never hide, overlap, or visually fight the WeChat capsule menu button. It is part of the host UI and usually only supports black/white styling through page configuration.
- Use `tabBar` for stable top-level pages. Use `custom-tab-bar` only when the visual system requires a custom selected capsule, center action, unread badge, or workspace-aware behavior.
- Keep `tabBar.list` aligned with actual tab pages. Do not put secondary pages, forms, details, or docs articles into tabBar.
- Use `scroll-view` intentionally. Avoid nested scroll regions unless a fixed custom nav/tab shell requires them.
- Prefer `button` with `open-type` for platform actions: share, contact, getPhoneNumber, chooseAvatar, and other WeChat-managed flows.
- Use `wx.showToast`, `wx.showModal`, WeUI Dialog/ActionSheet/HalfScreenDialog, or local wrappers instead of web-only overlays.
- Use `setData` sparingly for large lists. Paginate, virtualize, or use project list helpers for request logs and usage records.
- Treat `cover-view`/canvas/chart layers as special cases. Test overlays above charts and video/canvas content in DevTools and on device.

## Design Tokens

Use these tokens in `app.wxss`, theme files, component WXSS, or framework token maps. Keep the color identity shared with `qianwen-cloud-ui`; convert sizes to `rpx` for implementation.

```css
page {
  --qwx-bg: #f9fafd;
  --qwx-card: #ffffff;
  --qwx-muted-surface: #f2f4f8;
  --qwx-selected-surface: #e6e9ef;
  --qwx-line: #e6e9ef;
  --qwx-line-strong: #d1d7e2;
  --qwx-text: #0b0c0f;
  --qwx-text-soft: #111317;
  --qwx-text-muted: #535b6b;
  --qwx-text-faint: #7f8798;
  --qwx-disabled: #9fa7b7;
  --qwx-primary: #5b58ff;
  --qwx-primary-hover: #4500f3;
  --qwx-primary-soft: #f0f3ff;
  --qwx-primary-lighter: #e7eaff;
  --qwx-primary-chart: #afb9fd;
  --qwx-danger: #f33939;
  --qwx-success: #0da740;
  --qwx-warning: #ff7931;
  --qwx-blue: #277fe4;
  --qwx-status-success-bg: #ecfaed;
  --qwx-status-warning-bg: #fff5eb;
  --qwx-status-danger-bg: #fff2f0;
  --qwx-status-info-bg: #edf4fd;
  --qwx-status-neutral-bg: #f2f4f8;
}
```

Sizing:

- Use 750rpx as the design width. Common conversions: 8px -> 16rpx, 12px -> 24rpx, 16px -> 32rpx, 20px -> 40rpx, 24px -> 48rpx.
- Page horizontal padding: 32rpx on normal phones; 28rpx on very dense list pages; 40rpx on wider screens only when content needs breathing room.
- Mobile card: 32-40rpx radius, 28-40rpx padding.
- Dense list card: 28-32rpx radius, 24-32rpx padding.
- Top-level vertical rhythm: 24rpx compact gap, 32rpx normal gap, 40rpx major section gap.
- Primary buttons: 88-96rpx high, 999rpx radius.
- Icon tap target: at least 80-88rpx even when the visible icon is 40-44rpx.
- Status tag: 44-48rpx high, 4rpx 16-20rpx padding, 999rpx radius.

Typography:

- Font stack: inherit WeChat system font, with `PingFang SC`, `-apple-system`, `BlinkMacSystemFont`, `Helvetica Neue`, `Arial`, sans-serif fallback.
- Screen title: 48rpx / 64rpx, weight 600, `#0b0c0f`.
- Custom nav title: 34rpx / 48rpx, weight 600.
- Section title: 36rpx / 52rpx, weight 600.
- Card title: 30-32rpx / 44rpx, weight 600.
- Body/help text: 26-28rpx / 40rpx, muted `#535b6b` or `#7f8798`.
- Control/list text: 26rpx / 40rpx.
- Tab label: 22-24rpx / 32rpx.
- KPI number: 60-68rpx / 80rpx, weight 600 or 700.
- API keys/request IDs: monospace-like fallback is limited in Mini Programs; use `font-family: monospace` where supported and maintain masking.

## App Shell

### Native Or Custom Navigation

- Prefer native navigation for simple detail pages. Set `navigationBarBackgroundColor` to `#f9fafd` or `#ffffff`, `navigationBarTextStyle` to `black`, and title text concise.
- Use custom navigation for tab pages, dashboard pages, and pages where Qianwen Cloud branding or workspace switching matters.
- Custom nav layout:
  - Top spacer: status bar height from system info.
  - Nav content height: align to the capsule button height and vertical center.
  - Right safe gutter: reserve the capsule `width + right gap + 16-24rpx`; never place search, bell, or profile icons under it.
  - Left action: back/home/workspace avatar with 80-88rpx tap target.
  - Title: one line, 34rpx/600, truncate before capsule.
  - Optional subtitle/workspace chip belongs below the nav, not inside a crowded title row.
- For WeUI, use `mp-navigation-bar` when the local stack already has `weui-miniprogram`; override `background`, `color`, and slots to match Qianwen style.

### TabBar

- Default top tabs: 首页, 用量, API Key, 账单, 我的. Use 4-5 tabs only.
- Native tabBar should stay simple: white background, `#535b6b` default, `#5b58ff` selected, top border `#e6e9ef`.
- Custom tabBar can add a soft selected capsule, compact badges, and a center create action, but it must preserve WeChat page stack behavior.
- Keep the visual tab height around 104-112rpx plus safe-area bottom. Add `padding-bottom: env(safe-area-inset-bottom)` when supported by the target stack.
- Do not use hover-only states. Use tap pressed states and clear selected state.

### Page Layout

- Set `page { background: #f9fafd; }` for console pages.
- Use a root `.page` with `min-height: 100vh`, `box-sizing: border-box`, and bottom padding that accounts for tabBar or fixed action bars.
- On tab pages, keep main content scrollable under the custom nav only when the nav has a solid/blurred background and the first content block has enough top padding.
- Avoid full-screen outer white cards. White cards represent data surfaces, not the page itself.

## Components

### Cards And Cells

- Summary card: white, 40rpx radius, 40rpx padding, no heavy border.
- Data/list card: white, 32rpx radius, 28-32rpx padding, subtle row separators.
- Cell group: white surface, 32rpx radius, rows 96-128rpx high with icon, title, metadata, chevron.
- Resource/action tiles: 2-column grid or horizontal scroll; 32rpx radius; icon badge 64-72rpx.
- Avoid nested cards unless the inner element is a code block, chart panel, or selectable item.

### Buttons

- Primary action: black `#0b0c0f`, white text, 88-96rpx high, 999rpx radius, 28rpx/600, 36-40rpx horizontal padding.
- Primary pressed state: purple `#5b58ff` or opacity feedback.
- Disabled primary: `#9fa7b7`, white text.
- Secondary: white/transparent, `2rpx #d1d7e2`, black text, 88rpx high, 999rpx radius.
- Link/text action: purple `#5b58ff`, no border, 26-28rpx.
- Use Mini Program `button` reset styles carefully: remove default border only when providing a replacement focus/pressed state.

### Inputs, Search, And Filters

- Search capsule: 88-96rpx high, full width unless paired with one icon action, radius 999rpx, `#f2f4f8` fill or `#e6e9ef` border.
- Form input: 88-96rpx high, radius 24-32rpx or 999rpx, focus border/ring purple.
- Use `confirm-type`, `maxlength`, placeholder color, and keyboard types (`number`, `digit`, `idcard` only when appropriate).
- Filter chips: horizontal `scroll-view`, 72-80rpx high touch target, 999rpx capsule, active count visible.
- Complex filters use ActionSheet/HalfScreenDialog with reset and apply buttons fixed at the bottom.
- Date ranges should be quick chips plus a project date picker; do not port desktop popovers.

### Status Tags

- Use compact status tags everywhere status appears. Keep them subtle:
  - Success / HTTP 2xx: `#ecfaed` background, `#0da740` text.
  - Neutral / interrupted: `#f2f4f8` background, `#535b6b` text.
  - Informational / HTTP 3xx: `#edf4fd` background, `#277fe4` text.
  - User exception / HTTP 4xx: `#fff5eb` background, `#ff7931` text.
  - Service error / HTTP 5xx: `#fff2f0` background, `#f33939` text.
- Keep labels short: `200`, `4xx`, `失败`, `待开票`, `已启用`.
- Do not use loud WeChat green as the main brand color; reserve green for success state only.

### Lists Instead Of Tables

- Convert desktop table rows into list cards or cell groups.
- Each row should have: primary title, masked ID or metadata, one status tag, one key metric, and a chevron/action.
- Request log row height: 176-224rpx.
- API key row height: 176-220rpx with switch/action menu.
- Billing transaction row height: 144-176rpx.
- Use `scroll-view` or page scrolling with pagination. For large request logs, add skeleton, "加载更多", and empty/error states.
- Use `movable-view` or WeUI `slideview` only for familiar row actions; destructive actions still need confirmation.

### Charts

- Prefer the project's Mini Program chart library or canvas wrapper. Test real rendering in WeChat DevTools because canvas layering affects overlays.
- Use one primary chart per screen. Put dense legends and secondary metrics behind tabs or detail pages.
- Keep line/area chart colors pale: line `#afb9fd`, fill `#f0f3ff`, grid `#e6e9ef`, axis `#535b6b`.
- Chart card height: 360-460rpx for phone dashboards.
- Provide loading, no-data, and tap tooltip states. Do not rely on hover.

## Overlays And Feedback

### ActionSheet And Half-Screen Dialog

- Use WeUI ActionSheet for row actions, filter choices, workspace switcher, status selection, and non-destructive menus.
- Use HalfScreenDialog or a project bottom sheet for richer filters, API key reveal, recharge selection, and model picker.
- Sheet top radius: 40-48rpx; handle optional but useful; max height about 80-88vh.
- Footer buttons stay sticky above the safe area. Include reset/apply for filters.
- Backdrop should dim the page without fully hiding context.

### Dialogs And Toasts

- Use `wx.showModal` or WeUI Dialog for short confirmations and destructive actions.
- Use `wx.showToast` for copy, save, refresh, and lightweight success/error feedback.
- Use page-level error cards for network failures or permission issues; do not rely only on toast.
- Dialog buttons should fit Chinese labels; stack vertically if two labels become cramped.

### Forms

- Use full page forms for API key creation, alert rules, invoice title, and workspace settings.
- Keep one column. Split long forms into cards or sections.
- Fixed bottom submit bars must account for safe-area bottom and keyboard open state.
- Validate inline, disable submit until valid, and show concise help text.

## Page Patterns

### Home

- Custom nav with workspace chip or account avatar, leaving space for the capsule.
- First card: account status, balance/spend, or service health.
- Quick actions: 2x2 grid for 创建 API Key, 用量分析, 充值, 文档.
- Recent cards: request health, model usage, unread alerts. Use synthetic metrics.

### Usage Analytics

- Header: title, date chip, model chip.
- KPI summary card first; compact chart below.
- Secondary metrics: 2-column grid or horizontal scroll.
- Model breakdown: list cards with usage, cost, and trend indicator.
- Include pull-down refresh and partial-data state.

### Request Logs

- Search request ID as a capsule, then horizontal filter chips.
- Row content: time, model, masked request ID, HTTP status tag, latency, tokens/cost.
- Detail page or half-screen dialog shows timing, token breakdown, masked metadata, retry/copy actions.
- Never show raw prompts, private payloads, real customer identifiers, or unmasked keys.

### API Key Management

- Base URL card with copy buttons and masked URLs where appropriate.
- Key list rows: masked key, description, created date, enabled switch, cost summary, action menu.
- Create API Key: full page form with description, scope/model limits if relevant, advice box, disabled generate until valid.
- Generated key reveal: half-screen dialog; show once, copy feedback, and clear warning.

### Billing And Invoices

- Overview: balance, month spend, recharge CTA, plan status.
- Transactions: list rows with amount, type, date, status tag, detail chevron.
- Recharge: ActionSheet/half-screen quick amount selection; payment details use WeChat payment flow or backend handoff.
- Invoice: tabs/chips for 申请, 历史, 抬头; form page for invoice title.
- All amounts and invoice examples must be synthetic.

### Alerts And Settings

- Alerts: segment chips for 规则, 模板, 历史; list rows; create action.
- Alert rule form: full page, sections for model, metric, threshold, notification channel, fixed footer.
- Settings: cell groups for account, workspace, security, notifications, billing profile, docs/support.
- Account values must be masked or synthetic.

### Docs And Help

- Search capsule at top, category chips, article list.
- Article pages use readable 30-32rpx body text, compact code blocks, and copy buttons.
- Code blocks scroll horizontally and do not overflow the viewport.
- External docs links should use `web-view` only if the Mini Program policy and domain whitelist allow it; otherwise route to an in-app article or copy link.

## Implementation Notes

- Use WXML/WXSS component classes rather than inline styles for static styling. Use inline styles only for dynamic nav/capsule/safe-area values.
- Avoid unsupported or unreliable web CSS patterns. Test `position: sticky`, backdrop blur, fixed footers, and `env(safe-area-inset-bottom)` in the target base library.
- Store shared tokens in `app.wxss`, a theme WXSS file, or framework variables. Keep component styles locally scoped when possible.
- Use `page-meta` or page config where the project already does so for background and scroll behavior.
- Use `wx.canIUse` or framework feature checks before adopting newer Mini Program APIs.
- Use WeUI components when the project has `weui-miniprogram`; restyle lightly through `ext-class` instead of forking component internals.
- If using Taro or uni-app, keep WeChat-specific nav/capsule and tabBar logic behind platform conditionals.
- For copy actions, use `wx.setClipboardData`; for sharing, use `onShareAppMessage`; for login/user data/payment, follow the project's approved backend flow.
- Keep mock data dense enough to prove layout, but mask API keys, request IDs, account IDs, phone numbers, emails, and billing values.

## Quality Checklist

- `app.json`/`page.json` page registration, nav style, tabBar, and pull-down refresh choices match the intended page type.
- Custom navigation avoids the capsule button and uses real system/capsule metrics.
- `rpx` values are used consistently; no desktop px layout has been pasted into WXSS unchanged.
- Tab pages use native/custom tabBar correctly; secondary pages are not forced into tabBar.
- The page canvas is `#f9fafd`; primary cards are white and rounded.
- Buttons and icon actions have practical 80-96rpx tap targets.
- Desktop tables are converted to list cards, cells, or detail pages.
- Filters use horizontal chips plus ActionSheet/HalfScreenDialog for complex selection.
- Status tags are compact and use the qianwen color mapping.
- Charts are legible on narrow phones and tested with overlays/sheets.
- Fixed nav, tabBar, action bars, keyboard, and safe areas do not cover content.
- Loading, skeleton, empty, network error, permission denied, disabled, refreshing, and copied/saved states are present.
- Sensitive values are masked; no real Qianwen account data, invoices, API keys, request payloads, screenshots, or private browser content appears.
