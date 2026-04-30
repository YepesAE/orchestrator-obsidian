---
name: obsidian-iconize
description: >
  Obsidian Iconize (Icon Folder) plugin manager. Use for assigning icons to
  files and folders via frontmatter or data.json rules. Supports Lucide icons,
  Remixicon, Font Awesome, and custom SVGs.
  Triggers: icon, iconize, folder icon, file icon, lucide icon, set icon.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: obsidian-icon-folder v2.14.7
  PRECEDENCE: This skill overrides obsidian-core for all icon-related features.
---

# Obsidian Iconize (Icon Folder) Plugin

Plugin: obsidian-icon-folder v2.14.7
Config: `.obsidian/plugins/obsidian-icon-folder/data.json`

## ICON ASSIGNMENT METHODS

### Method 1: Frontmatter (per note)

```yaml
---
icon: LiBook
---
```

Adds an icon to that note's tab and title.

### Method 2: data.json (file/folder mapping)

```json
{
  "settings": { ... },
  "path/to/folder": {
    "iconName": "LiFolderIcon",
    "iconColor": "#hexcolor"
  },
  "path/to/file.md": "LiIconName"
}
```

Two syntaxes:
- **Simple**: `"path/to/file.md": "LiIconName"` (no color)
- **Rich**: `"path/to/folder": { "iconName": "LiFolderIcon", "iconColor": "#hexhex" }`

### Method 3: Rules (pattern-based auto-assignment)

```json
{
  "rules": [
    {
      "rule": "folder",
      "iconName": "LiFolderKanban",
      "for": "everything",
      "order": 0
    },
    {
      "rule": "file",
      "iconName": "LiCode2",
      "for": "*.ts",
      "order": 1
    }
  ]
}
```

### Inline Icons

```markdown
:LiIconName:
```

## LUCIDE ICONS REFERENCE (Li* prefix)

**Folders:** `LiFolder`, `LiFolderOpen`, `LiFolderClosed`, `LiFolderKanban`,
`LiFolderGit`, `LiFolderCode`, `LiFolderHeart`, `LiFolderLock`,
`LiFolderArchive`, `LiFolderCheck`, `LiFolderClock`, `LiFolderCog`

**Files:** `LiFile`, `LiFileText`, `LiFileCode`, `LiFileJson`, `LiFileSpreadsheet`,
`LiFileImage`, `LiFileVideo`, `LiFileAudio`, `LiFileArchive`, `LiFilePlus`

**Actions:** `LiKanban`, `LiLayoutDashboard`, `LiCalendar`, `LiPenTool`, `LiBookImage`,
`LiBookOpen`, `LiListTodo`, `LiCheckCircle`, `LiClock`, `LiAlertCircle`,
`LiZap`, `LiStar`, `LiHeart`, `LiPin`, `LiFlag`

**Tech:** `LiCode2`, `LiTerminal`, `LiGlobe`, `LiDatabase`, `LiGitBranch`,
`LiCloud`, `LiServer`, `LiMonitor`, `LiCpu`, `LiHardDrive`

**People:** `LiUser`, `LiUserCircle`, `LiUsers`, `LiUserCheck`, `LiUserPlus`

**UI:** `LiSearch`, `LiSettings`, `LiHome`, `LiMail`, `LiMessageSquare`,
`LiBell`, `LiFilter`, `LiPlus`, `LiMinus`, `LiX`, `LiCheck`, `LiTrash2`

**Creative:** `LiPalette`, `LiImage`, `LiCamera`, `LiMusic`, `LiVideo`,
`LiPen`, `LiPencil`, `LiPaintbrush`

**Status:** `LiCheckCircle`, `LiAlertCircle`, `LiAlertTriangle`, `LiInfo`,
`LiHelpCircle`, `LiThumbsUp`, `LiThumbsDown`, `LiTrendingUp`, `LiTrendingDown`

---

## CONFIG STRUCTURE

```json
{
  "settings": {
    "iconPacksPath": ".obsidian/icons",
    "fontSize": 16,
    "emojiStyle": "native",
    "iconColor": null,
    "recentlyUsedIcons": ["LiFolder", "LiCode2"],
    "recentlyUsedIconsSize": 5,
    "rules": [],
    "iconInTabsEnabled": false,
    "iconInTitleEnabled": true,
    "iconInFrontmatterEnabled": true,
    "iconInFrontmatterFieldName": "icon",
    "iconColorInFrontmatterFieldName": "iconColor",
    "iconsBackgroundCheckEnabled": false,
    "iconsInNotesEnabled": true,
    "iconsInLinksEnabled": true,
    "iconIdentifier": ":",
    "lucideIconPackType": "native",
    "debugMode": false
  },
  "path/to/folder": { "iconName": "LiIconName", "iconColor": "#hex" }
}
```

---

## OPERATION PATTERNS

### Assign an icon to a file via frontmatter
1. Open the `.md` file
2. Add `icon: LiIconName` to YAML frontmatter
3. Optionally add `iconColor: "#hexhex"` for color

### Assign an icon to a folder via data.json
1. Read `.obsidian/plugins/obsidian-icon-folder/data.json`
2. Add entry in top-level object (not `settings`):
   - `"path/to/folder": { "iconName": "LiIconName", "iconColor": "#hex" }`
3. Write back the complete JSON

### Remove an icon assignment
1. Read data.json
2. Delete the key from top-level object
3. Write back

### Add auto-assignment rules
1. Read data.json
2. Edit the `settings.rules` array
3. Each rule: `{ "rule": "folder"|"file", "iconName": "LiX", "for": "pattern", "order": N }`
4. Lower `order` = higher priority
5. `"for": "everything"` matches all

### Use inline icons in notes
1. Write `:LiIconName:` anywhere in body text
2. Renders the icon inline at text size
