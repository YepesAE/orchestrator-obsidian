# Orchestrator

An Obsidian vault configured as a project management and workflow
orchestration system. Switch between workspaces with a single click,
manage tasks on a kanban board, sketch diagrams on canvas, and keep
everything organized across 10 top-level domains.

**Obsidian v1.12.7** · **Gruvbox theme** · **17 community plugins**

---

## Vault Structure

```
Orchestrator/
├── Assets/
│   └── pixel-banner-images/     Animated GIF banners for project dashboards
├── Creative/
│   └── Pexá Studio/             Active project — design & creative work
├── Cybersec/                    Empty — cybersecurity resources
├── Desktop Dev/                 Empty — desktop applications
├── DIY/                         Empty — do-it-yourself projects
├── Game Dev/                    Empty — game development
├── Health/                      Empty — fitness & wellness
├── Home/                        Dashboard — navigator, kanban, welcome page
│   ├── Navigator.base           Bases card grid — shows all projects
│   ├── Kanban.md                Global task board
│   └── Welcome to Orchestrator.md  Landing page
├── References/                  Empty — reference materials
└── Web Dev/
    └── Hola Cafre/              Active project — web development
```

**10 top-level folders**, each representing a domain. **2 active projects**
(Hola Cafre, Pexá Studio) with identical file templates.

---

## Home Workspace

The dashboard opens at startup and gives you three views in one layout:

| Pane | What it does |
|------|-------------|
| **Navigator** | A card grid of all projects. Cards show color-coded folder icons. **Click a card → workspace switches to that project.** |
| **Kanban** | Global task board with standard columns: Backlog, In Progress, Review, Done. |
| **Welcome** | Landing page with a rotating pixel banner. |

The left sidebar is collapsed by default. The right sidebar shows backlinks,
tags, properties, outline, and a calendar.

---

## Project Blueprint

Every project follows the same 5-file template:

```
Project Name/
├── Link.md           Navigator card — tag, color, image, workspace command
├── Dashboard.md      Pixel banner header with random GIF
├── Wiki.md           Project knowledge base
├── Roadmap.canvas    Visual roadmap / mind map
└── Draw.md           Excalidraw sketch for diagrams & wireframes
```

### Color Coding

| Domain | Color | Hex |
|--------|-------|-----|
| Web Dev, Cybersec, Desktop Dev, Game Dev | Blue | `#458588` |
| Creative | Green | `#98971a` |
| References, DIY | Red | `#cc241d` |
| Health, Home, Assets, and others | Yellow | `#d79921` |

Colors are applied to both the **Navigator card image** (colored folder SVG)
and the **file tree** (via the File Color plugin).

### How Link.md works

```yaml
---
title: Project Name
color: "#458588"
tags: [Project]
image: "[[folder-gruvbox-original-blue.svg]]"
---
```

A `dataviewjs` block at the bottom runs
`app.commands.executeCommandById('workspaces-plus:Project Name')`
when the note opens. Combined with the Navigator's Bases card view, this
means **click the card → note opens → workspace switches** — one click.

---

## Workspace System

Three workspaces are currently saved:

| Workspace | Main panes | Purpose |
|-----------|-----------|---------|
| **Home** | Navigator · Kanban · Welcome | Dashboard |
| **Hola Cafre** | Dashboard · Wiki · Roadmap · Draw | Project workspace |
| **Pexá Studio** | Dashboard · Wiki · Roadmap · Draw | Project workspace |

The Home workspace loads on startup. Clicking a project card in the Navigator
switches to that project's workspace, which opens all 4 project files in
stacked tabs with the left sidebar collapsed for a focused, full-width view.

Workspace switching is powered by **Workspaces Plus** (`workspaces-plus` v0.3.3)
with commands triggered from `dataviewjs` blocks in each project's Link.md.

---

## Plugins

### Enabled (17)

| Plugin | Role |
|--------|------|
| **Iconize** (`obsidian-icon-folder`) | Folder and file icons |
| **File Color** | Color-coded folders in the file tree |
| **Colored Tags** | Tag colorization |
| **Kanban** | Global task board |
| **Excalidraw** | Diagrams and sketches per project |
| **Calendar** | Sidebar calendar for daily notes |
| **Pixel Banner** | Animated GIF banners on dashboards |
| **Dataview** | Dynamic queries and `dataviewjs` workspace triggers |
| **Bases** (core) | Card-based project navigator |
| **Workspaces Plus** | Save and switch between named workspace layouts |
| **Homepage** | Open Welcome page on startup |
| **Commander** | Custom command palette entries |
| **Hider** | Hide UI elements for clean workspace |
| **Omnisearch** | Fast vault-wide search |
| **Style Settings** | Theme customization |
| **Code Styler** | Code block styling |
| **File Explorer++** | Filter and pin files in explorer |
| **Ninja Cursor** | Enhanced cursor visibility |

### Disabled (9 — available but off)

`obsidian-advanced-uri`, `quickadd`, `buttons`, `data-cards`, `crafty`,
`obsidian-tasks-plugin`, `advanced-canvas`, `heatmap-calendar`,
`file-explorer-note-count`

---

## Theme & Appearance

- **Theme**: Obsidian Gruvbox (`insanum/obsidian-gruvbox`)
- **CSS snippet**: `left-start-notes` — forces left-aligned text
- **Inline titles**: hidden
- **Readable line length**: enabled
- **Fold heading/indent**: enabled

---

## Creating a New Project

Projects follow the Hola Cafre blueprint. To create one:

1. Create a folder under the appropriate domain (e.g., `Web Dev/NewProject/`)
2. Create 5 template files: `Link.md`, `Dashboard.md`, `Wiki.md`, `Roadmap.canvas`, `Draw.md`
3. Duplicate the Hola Cafre workspace in `workspaces.json` and update file paths
4. Pick the color SVG and GIF based on the domain

This is automated by the **project-creator AI skill**, which can create a
fully wired project with a single prompt.

The Navigator picks up new projects automatically — any note tagged `Project`
appears as a card.

---

## Requirements

- [Obsidian](https://obsidian.md/) ≥ 1.12.7
- Community plugins listed above (installed and enabled)
- Core plugin **Bases** must be enabled
- Core plugin **Workspaces** must be enabled

---

## Acknowledgements

- Folder SVGs from the [Gruvbox Folder Icons](https://github.com/Snailedlt/obsidian-gruvbox-folders) collection
- Pixel banner GIFs for dashboard headers
- All plugin authors credited in their respective repositories
