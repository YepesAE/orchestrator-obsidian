---
name: obsidian-homepage
description: >
  Obsidian Homepage plugin manager. Use for configuring which note, canvas, or
  workspace opens when Obsidian starts.
  Triggers: homepage, startup page, default page, open on startup.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: homepage v4.4.0
  PRECEDENCE: This skill overrides obsidian-core for homepage configuration.
---

# Obsidian Homepage Plugin

Plugin: homepage v4.4.0
Config: `.obsidian/plugins/homepage/data.json`

## CONFIG STRUCTURE

```json
{
  "version": 4,
  "homepage": "Dashboard",
  "useHomepage": true,
  "openOnStartup": true,
  "alwaysKeepTabs": false,
  "autoShiftPanels": false,
  "silentLaunch": true,
  "openInNewLeaf": false
}
```

| Field | Type | Description |
|-------|------|-------------|
| `version` | number | Config version (4) |
| `homepage` | string | File path (no `.md`) or `"random"` or `"daily"` |
| `useHomepage` | boolean | Enable homepage feature |
| `openOnStartup` | boolean | Open on app launch |
| `alwaysKeepTabs` | boolean | Keep existing tabs open |
| `autoShiftPanels` | boolean | Focus to homepage |
| `silentLaunch` | boolean | Focus on homepage file |
| `openInNewLeaf` | boolean | Open in new leaf vs existing |

## HOMEPAGE TYPES

- **File**: `"homepage": "Dashboard"` — opens `Dashboard.md`
- **Subfolder**: `"homepage": "Projects/Overview"` — path from vault root
- **Daily note**: `"homepage": "daily"` — opens today's daily note
- **Random**: `"homepage": "random"` — opens a random note
- **Workspace**: `"homepage": "workspace:Default"` — opens named workspace

---

## OPERATION PATTERNS

### Set homepage to a specific note
1. Read `.obsidian/plugins/homepage/data.json`
2. Set `"homepage": "NoteName"` (without `.md`)
3. Set `"useHomepage": true`
4. Set `"openOnStartup": true`
5. Write back

### Disable homepage
1. Set `"useHomepage": false`
2. Or set `"openOnStartup": false`

### Set homepage to daily notes
1. Set `"homepage": "daily"`
2. Each startup opens current date's daily note

### Set homepage to a workspace
1. First save a workspace via Obsidian UI
2. Set `"homepage": "workspace:WorkspaceName"`
