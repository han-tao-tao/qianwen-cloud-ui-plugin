# Qianwen Cloud UI Plugin for Codex

This repository packages Qianwen Cloud UI Codex skills as a plugin.

The skills help Codex design and implement Qianwen Cloud-style desktop console, documentation, mobile app, and WeChat Mini Program interfaces. Covered workflows include analytics dashboards, billing pages, API key management, request logs, compact tables, mobile list cards, drawers, dialogs, popovers, bottom sheets, custom navigation, tab bars, chart styling, and docs/help layouts.

## Install

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add han-tao-tao/qianwen-cloud-ui-plugin
```

Then open Codex, go to Plugins, select the `Qianwen Cloud UI` marketplace, and install `qianwen-cloud-ui`.

The installed plugin provides three skills:

- `$qianwen-cloud-ui` for desktop console and documentation pages.
- `$qianwen-cloud-mobile-ui` for phone-first mobile app, mobile web, PWA, React Native, Flutter, iOS, or Android interfaces.
- `$qianwen-cloud-miniprogram-ui` for WeChat Mini Program WXML/WXSS, custom navigation, tabBar/custom-tab-bar, WeUI-compatible flows, and mini program pages.

## Use

Invoke the bundled skill explicitly:

```text
$qianwen-cloud-ui design a Qianwen Cloud-style API key management page
$qianwen-cloud-mobile-ui design a Qianwen Cloud-style mobile usage analytics screen
$qianwen-cloud-miniprogram-ui design a Qianwen Cloud-style WeChat Mini Program API key page
```

Or ask Codex for a Qianwen Cloud / 千问云 / 千问工作台 style console, mobile app, 微信小程序, analytics, billing, API key, settings, request log, alert, or docs page and let Codex select the skill.

## Contents

```text
.agents/plugins/marketplace.json
plugins/qianwen-cloud-ui/.codex-plugin/plugin.json
plugins/qianwen-cloud-ui/skills/qianwen-cloud-ui/SKILL.md
plugins/qianwen-cloud-ui/skills/qianwen-cloud-ui/agents/openai.yaml
plugins/qianwen-cloud-ui/skills/qianwen-cloud-mobile-ui/SKILL.md
plugins/qianwen-cloud-ui/skills/qianwen-cloud-mobile-ui/agents/openai.yaml
plugins/qianwen-cloud-ui/skills/qianwen-cloud-miniprogram-ui/SKILL.md
plugins/qianwen-cloud-ui/skills/qianwen-cloud-miniprogram-ui/agents/openai.yaml
```

## Notes

- The plugin contains design instructions only. It does not include external app integrations or MCP servers.
- Do not copy real Qianwen Cloud account data, invoices, API keys, request payloads, or screenshots into generated UI.
