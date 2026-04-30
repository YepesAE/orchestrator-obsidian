---
name: obsidian-project-creator
description: >
  Creates new projects in the Orchestrator vault following the Hola Cafre
  blueprint. Use when the user says "create a project" or "new project".
  Triggers: create project, new project, make project.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  PRECEDENCE: Overrides obsidian-core for project creation workflow.
---

# Project Creator — Orchestrator Vault

Vault: `/home/yepes/Documents/Vaults/Orchestrator/`

## WHEN TRIGGERED

When user says "create a project called [Name] in [Folder]" or "new project [Name] under [ParentFolder]".

**CRITICAL: Ensure Obsidian is CLOSED before executing.**
Obsidian overwrites `workspaces.json` on shutdown/save and will undo the
workspace creation. Close Obsidian, create the project, then reopen.

## WHAT TO CREATE

```
ParentFolder/ProjectName/
├── Link.md           → Navigator card (tags, image, dataviewjs)
├── Dashboard.md      → Banner GIF header
├── Wiki.md           → Empty
├── Draw.md           → Excalidraw (empty)
└── Roadmap.canvas    → Canvas (empty)
```

Plus: duplicate the "Hola Cafre" workspace in workspaces.json, rename to ProjectName, update paths.

---

## STEP-BY-STEP

### Step 1: Determine color

| Parent folder contains | Color | Hex | SVG |
|------------------------|-------|-----|-----|
| Web Dev, Cybersec, Desktop Dev, Game Dev | Blue | `#458588` | `folder-gruvbox-original-blue.svg` |
| References, DIY | Red | `#cc241d` | `folder-gruvbox-original-red.svg` |
| Creative | Green | `#98971a` | `folder-gruvbox-original-green.svg` |
| Anything else | Yellow | `#d79921` | `folder-gruvbox-original-yellow.svg` |

### Step 2: Create project folder and files

**Link.md:**
```markdown
---
title: PROJECT_NAME
color: "#HEXHEX"
tags:
  - Project
image: "[[folder-gruvbox-original-COLOR.svg]]"
uri: "obsidian://adv-uri?vault=Orchestrator&commandid=workspace%3Aload&uid=PROJECT_NAME&filepath=PARENT_FOLDER%2FPROJECT_NAME%2FDashboard&filepath=PARENT_FOLDER%2FPROJECT_NAME%2FDraw&filepath=PARENT_FOLDER%2FPROJECT_NAME%2FLink&filepath=PARENT_FOLDER%2FPROJECT_NAME%2FRoadmap&filepath=PARENT_FOLDER%2FPROJECT_NAME%2FWiki"
---

```dataviewjs
app.commands.executeCommandById('workspaces-plus:PROJECT_NAME');
```
```

Replace PROJECT_NAME, HEXHEX, COLOR, PARENT_FOLDER with actual values.
URI-encode spaces in paths: spaces → `%20`, `/` → `%2F`.

**Dashboard.md:**
```markdown
---
banner: Assets/pixel-banner-images/RANDOM.gif
banner-height: 250
content-start: 0
---
```

Pick RANDOM.gif from the 17 GIFs (listed below). The `content-start` field is REQUIRED — it forces Pixel Banner to render the banner even when the note has no body content, preventing the missing-banner issue on workspace switch.
```
DashboardBanner.gif, FridayBanner.gif, MondayBanner.gif, MonthlyBanner1.gif,
MonthlyBanner2.gif, MonthlyBanner3.gif, MonthlyBanner4.gif, QAIdeaBanner.gif,
SaturdayBanner.gif, SundayBanner.gif, ThursdayBanner.gif, TuesdayBanner.gif,
WednesdayBanner.gif, WeeklyBanner1.gif, WeeklyBanner2.gif, WeeklyBanner3.gif,
WeeklyBanner4.gif
```

**Wiki.md:** Empty file (0 bytes).

**Roadmap.canvas:**
```json
{"nodes":[],"edges":[],"metadata":{"version":"1.0-1.0","frontmatter":{}}}
```

**Draw.md:**
```markdown
---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'


# Excalidraw Data

## Text Elements
%%
## Drawing
```compressed-json
N4KAkARALgngDgUwgLgAQQQDwMYEMA2AlgCYBOuA7hADTgQBuCpAzoQPYB2KqATLZMzYBXUtiRoIACyhQ4zZAHoFAc0JRJQgEYA6bGwC2CgF7N6hbEcK4OCtptbErHALRY8RMpWdx8Q1TdIEfARcZgRmBShcZQUebR44gEYaOiCEfQQOKGZuAG1wMFAwYugsKG4IQE4ANgBWAE4ASgCGAMwFALq4KYBFAsAAQntWBIqAHngA/Gp0BuWqGJbWAMIJ
xU6mFiaG1QC6C4VAADNum4PjKYqmDiCRADF1zq4bNs43ggDiAuw5RABBIto
Z7nV6/HhA7Rg8FsMHbCDUZg7EEjdjbbIgjGQ7Q4o4faqkRAcVjnQwkeCECYk
Z7YtIQDEhYK6ba9fp5aLcgDq2A5sVoDB0UQKfGquBEVAExEMdgcxG0mAE2gA
cgIHAhRJI2HBcLJHPJJIAKDRzISwOwODaYYQ6HTaQzGHSmcw8VzsTjc7Ym
KwhgCGvLWNCiOQ0OCwBL4Uj2NIZUmYCFQmGlcFI7BIjBo2SYhF4gmkikymk
kvkABkdstQip0IDGsiN3nVIkNiELguZcsUyAUKgUGp0qEw+G1+uN9HN1IIIs
IIt2IFqNTQOwoDDYLQESAEONM+P4cGkRA21B0QjeBAUDpCklPvIABSRSEG
ICB1gBBDEsQxCBWj4ekwCgJAlgQAAHPJ9zwT12BsXAKEUOBtlkQg+F2CBFGW
B1YkWCAlBmNtGFYVpOA4bppJADYAGWPB2AIXMz0WYDcLMAQVnVTZBV5WoGA
kKRNFwqARBkAR5iWep2GEHBuJsLxOIgHQC2AzBnHoVgYCYsgWDYZhIOs2JGO
wxYjDYAA1HhgnESRsP0pjWPY/wACtO1zFZ3SxCB2HiYwtg6AxPB4RidE0OI
UBAmKAgCjRNF0fQuwAE3o/J2G0bQFAAcywwLoFwxZ8IIoijgASguU4lOI2F
aMyZLsIIMgMhyXwAGF8lzMqCggTkAEU2GUABRABZKQZGmT8PxAECwDyfBtgm
cRoLgUh/AoBFuRSBBdko7YrjNIhxAoALtE4JA0CAEd9EYChYnY9KgsWZCyl
QtT0PmHYUGOZQACt+XQwRAT0RC6K0bZbSSBRcgkbB4PSGLsF0LsdGYGQUGK
dRhVu55Gg5XMJgyGzgvyAwMhCt0IrwwjiOIrt7tgyDNBfPYwhsORUc2F1sF
WVtbgsO6Mva0d4l0U41KYyhZDsOxxJ4ljBPa4jiM1MA2A+nC7u2XY0Y2QQu
2mKyXNrTYIF2JoYFeZ0TgQWJ4lSsiK2ITD9BzUk6a0aTvJdKhPio3I2Pp5N
ljAeIBDxY5c2IVVdX0rVkq1MiyAANV0Qp5WcBRuQEaIrm1YEZj2OkxZhbZn
VjPUHTTTMuQATnPPELxPVrLpuq6brehkIF7RAcFwAwBFgu6bOerY2H6Jx7F
DKbwh0SUCQRWY/lBVdDZoIT1xIDY3Oxd7IDQ4jNV6AJwkiVJMn8oojPyUZV
FZqoGAaFoy3qJFMAMTAWC0OUxRQkImozQ45ty6xEuyh8qor1Sqxn0TURAdg
hAdYpzT7hzE6dWWFbaAOY2whBnx4MFcIpEWIQQCJYLWAQUh+FYLqUWCd9BR
1sGBMo1lIR2lUrXA0TlKJnnElAeyxl4DOQKHJFhvgtKGGFG5MYXYgjeVdAE
AKCoAghW7po6IrhoAoIYqVaKDsogdCCJYWsDZEXaBibWLtLkGwz0KLHBiC
A/Lh0Fo9S4bAzC/UYg7YWpFci6gjj0XcAhiDVnVhYn+CdNSVx2CDYWgg8RQ
CoNibQACyUxbEAAFuCYSkbw/iQAgA
```
%%
```

### Step 3: Duplicate workspace in workspaces.json

**CRITICAL: Obsidian MUST NOT be running when modifying workspaces.json.**
Obsidian overwrites this file on every save/shutdown. If Obsidian is running,
your workspace will be lost immediately.

**Workspace duplication script** (Python — copy exactly):

```python
import json, hashlib, random

VAULT = "/home/yepes/Documents/Vaults/Orchestrator"
PROJECT = "Project Name"
PARENT = "Parent Folder"
OLD = "Web Dev/Hola Cafre"
NEW_PATH = f"Parent Folder/Project Name"

with open(f"{VAULT}/.obsidian/workspaces.json") as f:
    wsp = json.load(f)

# Deep copy Hola Cafre workspace
template = json.loads(json.dumps(wsp['workspaces']['Hola Cafre']))

def replace(obj):
    if isinstance(obj, str):
        return obj.replace(OLD, NEW_PATH)
    elif isinstance(obj, dict):
        new = {}
        for k, v in obj.items():
            if k == "id" and isinstance(v, str) and len(v) >= 6:
                # Generate fresh ID of same length as original
                new[k] = hashlib.md5(f"{PROJECT}{k}{random.random()}".encode()).hexdigest()[:len(v)]
            else:
                new[k] = replace(v)
        return new
    elif isinstance(obj, list):
        return [replace(i) for i in obj]
    return obj

new_ws = replace(template)

# FIX: Update active leaf to point to first leaf in NEW workspace
def first_leaf_id(node):
    if isinstance(node, dict):
        if node.get('type') == 'leaf':
            return node['id']
        for v in node.values():
            fid = first_leaf_id(v)
            if fid: return fid
    elif isinstance(node, list):
        for item in node:
            fid = first_leaf_id(item)
            if fid: return fid
    return None

new_ws['active'] = first_leaf_id(new_ws['main'])

# Add workspace
wsp['workspaces'][PROJECT] = new_ws

# Write and verify IMMEDIATELY
with open(f"{VAULT}/.obsidian/workspaces.json", 'w') as f:
    json.dump(wsp, f, indent='\t')

# Verify
with open(f"{VAULT}/.obsidian/workspaces.json") as f:
    verify = json.load(f)
assert PROJECT in verify.get('workspaces', {}), f"FAILED: {PROJECT} not saved!"
print(f"Workspace '{PROJECT}' saved. Total: {len(verify['workspaces'])}")
```

**What this does:**
1. Deep-copies the Hola Cafre workspace
2. Replaces all file paths from `Web Dev/Hola Cafre/` to `Parent Folder/New Project/`
3. Generates fresh random IDs for every node (main, split, tabs, leaf)
4. Fixes the `active` field to point to a valid leaf in the new workspace
5. Writes and immediately verifies the save succeeded

---

## RANDOM GIF HELPER

When picking a random GIF for Dashboard.md:
```python
import random
gifs = os.listdir(f'{VAULT}/Assets/pixel-banner-images/')
gif = random.choice([g for g in gifs if g.endswith('.gif')])
```

Use the `random` module (or just pick from the 17 listed GIFs).

---

## URI ENCODING

For the `uri` field in Link.md frontmatter, encode paths:
- Spaces → `%20`
- `/` → `%2F`
- The vault name is always `Orchestrator`

Example: `filepath=Web%20Dev%2FNew%20Project%2FDashboard`

---

## VERIFICATION

After creating the project, verify ALL of these:
1. **5 files exist**: `Link.md`, `Dashboard.md`, `Wiki.md`, `Draw.md`, `Roadmap.canvas` in `PARENT_FOLDER/PROJECT_NAME/`
2. **Workspace saved**: `PROJECT_NAME` exists in `workspaces.json['workspaces']` — read and verify immediately after writing
3. **Active field valid**: `workspace['active']` points to a leaf ID that exists in the new workspace (NOT a stale Hola Cafre ID)
4. **File paths correct**: All leaf nodes in the workspace point to `PARENT_FOLDER/PROJECT_NAME/` (not `Web Dev/Hola Cafre/`)
5. **Link.md fields correct**: `color` hex matches the color rule, `image` SVG matches the color, `tags` includes `Project`
6. **Dashboard.md**: `banner` points to a valid GIF in `Assets/pixel-banner-images/`
7. **NON-NEGOTIABLE**: Read `workspaces.json` AFTER writing and assert the workspace key exists. If it doesn't, DO NOT proceed — Obsidian may be running.
