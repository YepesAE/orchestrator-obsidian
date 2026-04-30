---
name: obsidian-ui
description: >
  Bundled UI/config skill for: Hider, Omnisearch, Commander, Code Styler,
  File Explorer++, File Explorer Note Count, Ninja Cursor, File Color,
  Colored Tags, Crafty. Use for managing UI customization and config files
  for these plugins.
  Triggers: hider, omnisearch, commander, code styler, file explorer,
  note count, ninja cursor, file color, colored tags, crafty.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  PRECEDENCE: This skill overrides obsidian-core for the covered plugins.
---

# Obsidian UI Plugins (Bundled)

Covers 10 UI/config plugins in the Orchestrator vault.

---

## 1. Hider (`obsidian-hider` v1.6.1)

Hides Obsidian UI elements. Config: `.obsidian/plugins/obsidian-hider/data.json`

```json
{
  "hideStatus": false,
  "hideVault": false,
  "hideTitle": false,
  "hideSearchSuggestions": false,
  "hideSidebars": false,
  "hideTooltips": false,
  "hideScrollbars": false,
  "hideTabBar": false
}
```

All boolean toggles. Set `true` to hide the element.

---

## 2. Omnisearch (`omnisearch` v1.28.2)

Vault-wide search engine. Config: `.obsidian/plugins/omnisearch/data.json`

### Embed search in notes
````markdown
```omnisearch
query: your search terms
```
````

Configurable settings include: indexed file types, excluded folders, cache behavior,
weighting for filename vs content matches, result count.

---

## 3. Commander (`cmdr` v0.5.5)

Customize workspace by adding commands to UI elements. Config:
`.obsidian/plugins/cmdr/data.json`

Creates macro commands and custom toolbar buttons. Complex JSON config mapping
command IDs to UI locations (ribbon, status bar, title bar, mobile toolbar).

---

## 4. Code Styler (`code-styler` v1.1.7)

Style code blocks and inline code. Config: `.obsidian/plugins/code-styler/data.json`

Features: custom themes per language, line numbers, line highlighting,
header/footer decorations, code block titles.

---

## 5. File Explorer++ (`file-explorer-plus` v1.3.1)

Hide and pin files/folders in the file explorer. Config:
`.obsidian/plugins/file-explorer-plus/data.json`

```json
{
  "filters": {
    "hidden": ["_private/*", ".git/*"],
    "pinned": ["Readme.md", "Dashboard.md"]
  }
}
```

- `hidden`: array of glob/regex patterns to hide
- `pinned`: array of file/folder paths to pin to top

---

## 6. File Explorer Note Count (`file-explorer-note-count` v1.2.4)

Shows note counts under folders. Config:
`.obsidian/plugins/file-explorer-note-count/data.json`

```json
{
  "showAllNumbers": true,
  "filterList": ["*.md", "*.canvas"],
  "excludeFileExtensions": [".excalidraw"],
  "showFilesInSubfolders": true,
  "countAddBlankLine": false
}
```

- `showAllNumbers`: show counts for all folders
- `filterList`: file types to count
- `showFilesInSubfolders`: recursive counting

---

## 7. Ninja Cursor (`ninja-cursor` v0.0.13)

Enhances cursor visibility. Config: `.obsidian/plugins/ninja-cursor/data.json`

Controls cursor animation effects (glow, trail, pulse) and visibility settings.
Minimal config — primarily enabled/disabled toggle.

---

## 8. File Color (`obsidian-file-color` v1.1.0)

Sets colors on folders/files in the file tree. Config:
`.obsidian/plugins/obsidian-file-color/data.json`

```json
{
  "fileColors": [
    {
      "path": "Projects/Active",
      "color": "#3b82f6"
    },
    {
      "path": "References",
      "color": "#f59e0b"
    }
  ]
}
```

Assign colors via `fileColors` array. Each entry has `path` (vault-relative) and `color` (hex).

---

## 9. Colored Tags (`colored-tags` v6.1.2)

Colorizes tags. Config: `.obsidian/plugins/colored-tags/data.json`

```json
{
  "palette": {
    "luminance": 5,
    "chroma": 2,
    "hueShift": 0
  },
  "tagColors": [
    {
      "tag": "#project",
      "color": { "r": 59, "g": 130, "b": 246 }
    },
    {
      "tag": "#todo",
      "color": { "r": 245, "g": 158, "b": 11 }
    }
  ]
}
```

Tag colors stored with RGB values. Nested tags inherit mixed colors.

---

## 10. Crafty (`crafty` v1.3.2)

Adds tooltips to canvas nodes and enables navigation between connected nodes.
Config: `.obsidian/plugins/crafty/data.json`

Works with Canvas files. Primarily a UI enhancement with minimal filesystem config.

---

## OPERATION PATTERNS

### Hide a UI element (Hider)
1. Read `.obsidian/plugins/obsidian-hider/data.json`
2. Set the relevant toggle to `true`
3. Write back

### Add a file/folder color (File Color)
1. Read `.obsidian/plugins/obsidian-file-color/data.json`
2. Add `{ "path": "path/to/folder", "color": "#hex" }` to `fileColors` array
3. Remove any existing entry for the same path first

### Color a tag (Colored Tags)
1. Read `.obsidian/plugins/colored-tags/data.json`
2. Add `{ "tag": "#tagname", "color": { "r": R, "g": G, "b": B } }` to `tagColors` array
3. Write back

### Hide a file in explorer (File Explorer++)
1. Read `file-explorer-plus/data.json`
2. Add glob pattern to `filters.hidden` array
3. Write back
