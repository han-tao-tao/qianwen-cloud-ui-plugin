# Qianwen Cloud UI Plugin for Codex

This repository packages the `qianwen-cloud-ui` Codex skill as a plugin.

The skill helps Codex design and implement Qianwen Cloud-style console and documentation pages, including analytics dashboards, billing pages, API key management, compact tables, drawers, dialogs, popovers, chart styling, and docs search/reading layouts.

## Install

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add han-tao-tao/qianwen-cloud-ui-plugin
```

Then open Codex, go to Plugins, select the `Qianwen Cloud UI` marketplace, and install `qianwen-cloud-ui`.

## Use

Invoke the bundled skill explicitly:

```text
$qianwen-cloud-ui design a Qianwen Cloud-style API key management page
```

Or ask Codex for a Qianwen Cloud / 千问云 / 千问工作台 style console, analytics, billing, API key, settings, or docs page and let Codex select the skill.

## Contents

```text
.agents/plugins/marketplace.json
plugins/qianwen-cloud-ui/.codex-plugin/plugin.json
plugins/qianwen-cloud-ui/skills/qianwen-cloud-ui/SKILL.md
plugins/qianwen-cloud-ui/skills/qianwen-cloud-ui/agents/openai.yaml
```

## Notes

- The plugin contains design instructions only. It does not include external app integrations or MCP servers.
- Do not copy real Qianwen Cloud account data, invoices, API keys, or screenshots into generated UI.
