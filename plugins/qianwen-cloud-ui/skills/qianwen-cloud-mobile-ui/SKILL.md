---
name: qianwen-cloud-mobile-ui
description: "Use when designing or implementing a Qianwen Cloud / 千问云 / 千问工作台 mobile app, mobile web, PWA, iOS, Android, React Native, Flutter, or phone-sized console experience. Adapts the qianwen-cloud-ui visual system to phones: pale gray app workspace, white rounded cards, bottom tab navigation, safe-area-aware top bars, compact data lists, mobile API key and billing flows, bottom sheets, full-screen forms, capsule filters, compact status tags, black CTAs, purple selected/focus/link states, restrained charts, and mobile documentation/help surfaces."
---

# qianwen-cloud-mobile-ui

## Direction

Build phone-first Qianwen Cloud style product interfaces. Preserve the calm operational feel of `qianwen-cloud-ui`, but redesign the interaction model for a handheld app instead of shrinking the desktop console.

Use this skill for mobile app screens, mobile web screens, React Native/Flutter/iOS/Android implementations, PWA prototypes, or responsive phone breakpoints for Qianwen Cloud console workflows. Do not use it for marketing landing pages. Do not copy Qianwen logos, screenshots, real account names, real emails, invoice data, API keys, request IDs, or private browser content. Use masked and synthetic examples.

## Workflow

1. Reuse the project's native primitives first: navigation, safe-area helpers, bottom sheets, lists, forms, tabs, icons, charts, haptics, and accessibility utilities.
2. Choose the mobile workflow before drawing components: overview, usage analytics, request logs, API keys, billing, alerts, settings, docs/help, or account/workspace switcher.
3. Build the shell first: safe-area-aware top app bar, scroll container, bottom navigation or bottom action bar, then content.
4. Replace desktop tables with scan-friendly list cards, grouped rows, or drill-in details. Use a dense table only on tablet or landscape widths.
5. Replace desktop right drawers with bottom sheets, full-screen modals, or pushed detail routes.
6. Add filled, loading, empty, error, offline, refreshing, selected, disabled, keyboard-open, and sheet-open states.
7. Validate at 360x780, 390x844, 430x932, and a small Android viewport. Check safe areas, keyboard avoidance, scroll reachability, and no bottom navigation overlap.

## Mobile Adaptation Rules

- Treat 360-430 logical px as the primary design range. Wider tablets can reuse the desktop skill with a navigation rail or split view.
- Use `#f9fafd` as the app canvas and white cards as content surfaces. Never wrap the entire screen in a giant card.
- Keep the desktop identity: black primary action, purple selected/focus/link states, soft gray structure, compact status tags, restrained charts.
- Increase touch targets even when visual controls are compact. Interactive areas should be at least 44px on iOS-style surfaces and 48dp on Android-style surfaces; never go below WCAG's 24 CSS px minimum.
- Honor safe areas and system bars. Pad top bars, bottom navigation, sheets, sticky footers, and keyboard-aware forms with platform insets.
- Keep primary actions reachable near the bottom or in the top-right only when the action is light and reversible.
- Prefer one primary task per screen. Put secondary actions in menus, sheets, or row-level actions.
- Keep text operational and short. Do not add visible instructions for obvious controls.
- Use real data density, but constrain each mobile screen to what can be scanned with one thumb: 1 primary metric block, 1 chart, 3-6 key list rows, or a single form section at a time.

## Design Tokens

Map these values to local tokens or CSS variables. Keep the original qianwen-cloud-ui colors, but reduce radii and spacing for phone density.

```css
:root {
  --qwm-bg: #f9fafd;
  --qwm-card: #ffffff;
  --qwm-muted-surface: #f2f4f8;
  --qwm-selected-surface: #e6e9ef;
  --qwm-line: #e6e9ef;
  --qwm-line-strong: #d1d7e2;
  --qwm-text: #0b0c0f;
  --qwm-text-soft: #111317;
  --qwm-text-muted: #535b6b;
  --qwm-text-faint: #7f8798;
  --qwm-disabled: #9fa7b7;
  --qwm-primary: #5b58ff;
  --qwm-primary-hover: #4500f3;
  --qwm-primary-soft: #f0f3ff;
  --qwm-primary-lighter: #e7eaff;
  --qwm-primary-chart: #afb9fd;
  --qwm-danger: #f33939;
  --qwm-success: #0da740;
  --qwm-warning: #ff7931;
  --qwm-blue: #277fe4;
  --qwm-status-success-bg: #ecfaed;
  --qwm-status-warning-bg: #fff5eb;
  --qwm-status-danger-bg: #fff2f0;
  --qwm-status-info-bg: #edf4fd;
  --qwm-status-neutral-bg: #f2f4f8;
  --qwm-shadow-light: 0 8px 24px rgba(83, 91, 107, 0.06);
  --qwm-shadow-normal: 0 16px 40px rgba(83, 91, 107, 0.10);
}
```

Typography:

- Font family: `Inter`, `PingFang SC`, `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, `Roboto`, `Helvetica Neue`, `Arial`, `Noto Sans`, sans-serif.
- Code/API values: `RobotoMono`, `SFMono-Regular`, `Consolas`, `Monaco`, monospace.
- Screen title: 24px / 32px, weight 600, color `#0b0c0f`.
- Top app bar title: 17px / 24px, weight 600.
- Section title: 18px / 26px, weight 600.
- Card title: 15-16px / 22px, weight 600.
- Body/help text: 13-14px / 20px, muted `#535b6b` or `#7f8798`.
- Controls and list rows: 13px / 20px.
- KPI number: 30-34px / 40px, weight 600 or 700.
- Tab label: 11-12px / 16px when paired with an icon.

Spacing and radius:

- Screen horizontal padding: 16px on 360-390px phones, 20px on 430px phones.
- Vertical screen rhythm: 12px between compact sections, 16px between cards, 20px before major groups.
- Mobile card: 16-20px radius, 16px padding for dense content, 20px for summary cards.
- Bottom sheet: 24px top radius, 16-20px side padding, safe-area bottom padding.
- List row radius: 14-16px when rows are grouped in white cards.
- Capsule controls: 999px radius.

## App Shell

### Top App Bar

- Height: 52-56px plus top safe-area inset.
- Background: usually `#f9fafd` or white with slight blur when content scrolls underneath.
- Left side: workspace avatar, back chevron, or menu. Use one clear affordance, not a desktop sidebar toggle.
- Center/left title: 17px/600, truncated after one line.
- Right side: one or two 40-44px icon buttons such as search, notifications, help, profile, or create.
- Use monochrome line icons, 20-22px, `stroke: currentColor`. Selected or active icons use purple.

### Bottom Navigation

- Use bottom tabs for the core app sections. Default tabs: 首页, 用量, API Key, 账单, 我的.
- Height: 64-72px plus bottom safe-area inset.
- Background: white, top border `#e6e9ef`, optional blur on native/web platforms.
- Use 4-5 tabs. Each tab has a 22-24px line icon, 11-12px label, and 48px minimum touch area.
- Selected tab uses purple icon/text and a soft `#f0f3ff` capsule or small indicator. Unselected tabs use `#535b6b`.
- Do not put every desktop sidebar item into bottom navigation. Put secondary sections inside "我的", a workspace sheet, or page-level segmented controls.

### Secondary Navigation

- Route-level sub-tabs become horizontally scrollable capsule tabs below the title or inside a card.
- Tab container can be white or `#f2f4f8`, 36-40px high, with selected tab as white or `#f2f4f8`.
- Keep labels short: 用量, 日志, 趋势, 明细, 发票, 规则.
- Preserve scroll position and selected state when returning from detail screens.

## Core Components

### Cards

- Summary card: white, 20px radius, 20px padding, no heavy border, optional soft shadow only when floating above mixed content.
- Dense data card: white, 16px radius, 14-16px padding, subtle separators.
- Hero/banner card: pale blue/purple tint, 20px radius, compact text, one reachable action. Avoid large marketing hero composition.
- Tile card: 16px radius, `#ffffff`, optional `1px #e6e9ef`, icon badge 32-36px.
- Avoid cards inside cards unless the inner surface is a real code block, list group, or selectable resource tile.

### Buttons

- Primary action: black `#0b0c0f`, white text, 44-48px high, radius 999px, 14px/600, horizontal padding 18-20px.
- Primary hover/pressed: purple `#5b58ff`; use native pressed opacity or ripple where appropriate.
- Disabled primary: `#9fa7b7`, white text, no hover.
- Secondary: white or transparent, `1px #d1d7e2`, black text, 44px high, radius 999px.
- Link/text action: purple `#5b58ff`, 13-14px, no border.
- Icon-only: visible icon can be 20-22px, but hit target must be 44-48px.
- Floating action button is acceptable for create or support actions only when it does not compete with bottom tabs.

### Inputs And Filters

- Search input: 44-48px high, full width, radius 999px, `#e6e9ef` border or `#f2f4f8` fill, search icon left.
- Form input: 48px high, radius 16px or 999px depending local component style; focus border/ring purple.
- Select/filter trigger: 36-40px high capsule, `1px #e6e9ef`, 13px text.
- Filter chips scroll horizontally. Always include a visible active-count chip when multiple filters are applied.
- Complex filters open a bottom sheet with search, checkbox rows, reset, and apply actions.
- Date ranges use a bottom sheet: quick range chips first, then calendar/range fields. Do not use a desktop 488px popover on phone.

### Status Tags

- Keep the original compact status language. Tags are `inline-flex`, 22-24px high, `2px 8-10px` padding, radius 999px, 12px / 16px text, no shadow.
- Success or HTTP 2xx: background `#ecfaed`, text `#0da740`.
- Neutral or interrupted: background `#f2f4f8`, text `#535b6b`.
- Informational or HTTP 3xx: background `#edf4fd`, text `#277fe4`.
- User exception or HTTP 4xx: background `#fff5eb`, text `#ff7931`.
- Service error or HTTP 5xx: background `#fff2f0`, text `#f33939`.
- Never use large saturated banners for row statuses unless a whole screen is in error state.

### Lists Instead Of Tables

- Convert desktop table rows into grouped list cards.
- Each list item should expose: primary label, secondary metadata, one compact status tag, one key metric, and a chevron or action menu.
- Use 56-72px row height for simple rows; 88-112px for request log/API key/billing rows with multiple metadata lines.
- Put IDs/API keys in monospace and mask them, e.g. `sk-a****1234`, `req_****8f2a`.
- Use swipe actions sparingly. Destructive actions still need confirmation.
- For long lists, include pull-to-refresh, skeleton rows, empty state, error retry, and infinite loading or pagination.

### Charts And Metrics

- Use one primary chart per screen section. Put secondary breakdowns behind tabs or drill-in routes.
- Chart cards are white with light grid lines. Avoid saturated multi-series visuals on small screens.
- Line/area chart: line `#afb9fd`, pale primary fill, axis labels `#535b6b`, grid `#e6e9ef`.
- Bar chart: normal bars `#e7eaff` or `#d1d7ff`; active bar `#5b58ff`.
- KPI deltas: green for improvement, red for bad movement, small arrow or compact text.
- For dense analytics, show a summary strip of 2-4 horizontally scrollable KPI tiles and a detail screen for the full chart.

## Mobile Overlays

### Bottom Sheets

- Use bottom sheets for filters, workspace switcher, row actions, compact forms, model picker, date picker, and API key reveal confirmations.
- Sheet width: full viewport; max height 88-92vh; top radius 24px; drag handle centered, 36px x 4px, `#d1d7e2`.
- Header: title 17-18px/600, optional muted description, close icon with 44px target.
- Content scrolls inside the sheet. Footer actions stay sticky above the bottom safe area.
- Backdrop: translucent wash with blur when supported; keep underlying page recognizable but inactive.

### Full-Screen Forms

- Use a pushed route or full-screen modal for complex create/edit flows: API key creation, alert rules, workspace settings, invoice title management.
- Header has back/close, title, and optional save. Footer can hold a full-width black primary button.
- Split long forms into sections. Validate inline and keep disabled submit until valid.
- Avoid multi-column forms. Every field is one column and keyboard-aware.

### Dialogs And Alerts

- Use centered dialogs only for short confirmations, destructive actions, or critical notices.
- Width: viewport minus 32px; radius 24px; 20px padding; concise title and body.
- Button layout: stacked full-width on very narrow phones, horizontal only when labels fit comfortably.

## Page Patterns

### Home

- Top: greeting and workspace/account chip, then a quick status card.
- Quick actions: 2x2 or horizontal tiles for 创建 API Key, 查看用量, 充值, 文档.
- Overview cards: balance/spend, usage, recent model, request health. Use synthetic values.
- Learning/resource cards should be compact and actionable, not marketing-heavy.

### Usage Analytics

- Header: title, time range chip, optional model chip.
- First card: main KPI and trend chart.
- Secondary KPI tiles: horizontal scroll or 2x2 grid.
- Details: model usage list with expandable detail route or bottom sheet.
- Include loading skeleton, no-data state, partial-data state, and pull-to-refresh.

### Request Logs

- Toolbar: search request ID, date chip, model chip, status chip.
- List item: time, model, masked request ID, HTTP status tag, latency, tokens/cost, chevron.
- Detail sheet/route: request summary, model, timing, token breakdown, masked payload metadata, retry/copy actions.
- Do not show raw prompts, private payloads, real customer identifiers, or unmasked keys.

### API Key Management

- Top card: base URL capsules and copy buttons.
- Key list: masked key, description, creation date, cost/use summary, enabled switch, action menu.
- Create flow: full-screen or bottom sheet with description input, scope/model limits if relevant, advice box, disabled generate button until valid.
- Reveal/copy key: use a confirmation sheet; show the generated key once; include copy feedback and a warning that it cannot be viewed again.

### Billing

- Overview: balance, spend this month, recharge button, plan status.
- Trend: compact chart with date range.
- Transactions/invoices: list cards with amount, type, date, status tag, chevron.
- Recharge or subscription: bottom sheet for quick amount selection; full route for payment details.
- All money examples must be synthetic.

### Alerts And Settings

- Alerts: segmented tabs for rules/templates/history, list rows, create action, empty state.
- Alert rule form: full-screen route or tall sheet with threshold, model, channel, and fixed footer.
- Settings: grouped list rows for account, workspace, security, notifications, billing profile, docs/support.
- Account and workspace values must be masked or synthetic.

### Docs And Help

- Use a mobile docs shell: search capsule at top, category chips, article list, and reading route.
- Article body: white or pale panel, 16px side padding, readable 15-16px text, 12px code blocks.
- Code blocks scroll horizontally and include a 44px copy target.
- Search overlay is a full-screen modal or bottom sheet, not a 580px desktop panel.

## Implementation Notes

- For React/Next/mobile web, use CSS environment variables for safe areas: `env(safe-area-inset-top)` and `env(safe-area-inset-bottom)`.
- For React Native, use `SafeAreaView`, platform navigation primitives, and bottom-sheet libraries already present in the project.
- For Flutter, use `SafeArea`, `NavigationBar`, `BottomSheet`, and existing theme extensions.
- For iOS native, respect safe areas, Dynamic Type, VoiceOver labels, and large content sizes.
- For Android native, respect window insets, edge-to-edge behavior, TalkBack labels, and 48dp touch targets.
- Use the existing icon library. If none exists, use lucide for web prototypes and platform icons for native implementations.
- Prefer native scrolling, pull-to-refresh, haptics, and keyboard avoidance over desktop hover patterns.
- Do not depend on hover. Every action must have tap, focus, and accessibility states.
- Keep screenshots and mock data synthetic.

## Quality Checklist

- Phone shell has safe-area-aware top bar and bottom navigation or bottom action bar.
- No content is hidden behind the status bar, home indicator, bottom nav, sticky footer, or keyboard.
- Main navigation uses 4-5 bottom tabs; secondary navigation uses scrollable capsule tabs.
- Cards use 16-20px radius and 16-20px padding, not desktop 24px/28px defaults everywhere.
- Buttons, icon buttons, tabs, list actions, and chips have at least 44-48px practical hit areas when important.
- Search and form fields are 44-48px high and keyboard-aware.
- Desktop tables have been redesigned as list cards or grouped rows.
- Status tags remain compact and use the original qianwen color mapping.
- Charts are legible at 360px width and avoid dense legends.
- Bottom sheets have drag handle, close target, sticky footer, max height, and safe-area padding.
- Create/edit flows validate input, include disabled states, and do not rely on hidden desktop drawers.
- Loading, empty, offline/error, refreshing, and permission-denied states are present where data is remote.
- Sensitive values are masked; no real Qianwen account data, invoices, API keys, request payloads, or screenshots appear.
