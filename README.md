# Orchestrator

An Obsidian vault configured as a project management and workflow
orchestration system. Switch between workspaces with a single click,
manage tasks on a kanban board, sketch diagrams on canvas, and keep
everything organized across 10 top-level domains.

**Obsidian v1.12.7** · **Gruvbox theme** · **20 community plugins** · **6 workspaces**

<img width="1893" height="1029" alt="orchestrator-home-layout" src="https://github.com/user-attachments/assets/35ccca23-c8cf-4ace-a332-2865ddd6e7aa" />
Orchestrator home layout.

<img width="1918" height="1075" alt="orchestrator-project-layout" src="https://github.com/user-attachments/assets/90825e15-d59c-4294-85cf-75268f5f72c8" />
Orchestrator project layout.


---

## Vault Structure

```
Orchestrator/
├── Assets/
│   └── pixel-banner-images/            Animated GIF banners for project dashboards
├── Creative/
│   └── Pexá Studio/                    Project — design and creative studio work
├── Cybersec/                           Empty — cybersecurity resources
├── Desktop Dev/                        Empty — desktop applications
├── DIY/                                Empty — do-it-yourself projects
├── Game Dev/                           Empty — game development
├── Health/
│   └── Escalada/                       Project — climbing fitness tracking
├── Home/                               Dashboard — navigator, kanban, welcome page
│   ├── Navigator.base                  Navigator card grid — all projects
│   ├── Kanban.md                       Global user-story board
│   └── Welcome to Orchestrator.md      Landing page
├── References/                         Empty — reference materials
└── Web Dev/
    ├── Hola Cafre/                     Project — Angular web for an artist
    └── Babylon/                        Project — web development
```

**10 top-level domains**, each representing an area of focus.
**4 active projects** (Hola Cafre, Babylon, Pexá Studio, Escalada)
with identical file templates and workspace layouts.

---

## Home Workspace

The dashboard opens at startup and gives you three views in one layout:

| Pane | What it does |
|------|-------------|
| **Navigator** | A card grid of all projects. Cards show color-coded folder icons. **Click a card → workspace switches to that project.** |
| **Kanban** | Global task board with user stories (columns: Backlog, Analyzing, In Progress, For Review, Done). Each user story links to a project's task file. |
| **Welcome** | Landing page with a rotating pixel banner. |

The left sidebar is collapsed by default. The right sidebar shows backlinks,
outgoing links, tags, properties, outline, and a calendar.

---

## Project Blueprint

Every project follows the same template:

```
Project Name/
├── Link.md              Navigator card — workspace launcher
├── Tasks.md             Task index — progress bars, dynamic task table, open-task queries
├── Wiki.md              Project knowledge base (landing page)
├── Wiki/                Wiki sub-pages
│   ├── Architecture.md  Tech stack, module structure, routing, services
│   ├── Setup.md         Prerequisites, dev commands, environment config
│   ├── Components.md    Component catalog by section
│   └── API.md           API surface, endpoints, models
├── Roadmap.canvas       Visual roadmap / mind map (Canvas)
├── Draw.md              Excalidraw sketch for diagrams & wireframes
└── Tasks/               Granular task lists — one file per user story
    └── Story Name.md    Checklist of #task items with priorities and dates
```

### How Link.md works

```yaml
---
title: Project Name
color: "#458588"
tags: [Project]
image: "[[folder-gruvbox-original-blue.svg]]"
uri: "obsidian://adv-uri?vault=Orchestrator&commandid=workspace%3Aload&uid=Project&filepath=..."
---
```

A `dataviewjs` block runs `app.commands.executeCommandById('workspaces-plus:Project Name')`
when the note opens. Combined with the Navigator card view, this means
**click the card → note opens → workspace switches** — one click.

### How Tasks.md works

The task index is a live dashboard for each project:

- **DataviewJS progress bar** — reads all `.file.tasks` from files in `Tasks/` and shows completion percentage
- **Dynamic task file table** — lists every file in `Tasks/` with open/done counts and progress
- **Tasks query block** — renders all open tasks grouped by filename (requires Tasks plugin)

When the `Tasks/` folder is empty, the page shows a friendly message instead of stale links.
Everything updates automatically as you add or remove task files.

---

## Task Architecture

The vault uses a **two-level task system** to keep the home kanban manageable
while projects contain granular detail.

```
Home Kanban (user stories)                   Project Tasks/ (granular)
  ├── "Web Design" ────────────────→ Tasks/Web Design.md
  │                                      └── [ ] Prepare Web Sketch
  │                                      └── [ ] Choose color palette
  │
  ├── "Wireframe all views" ──────→ Tasks/Wireframes.md
  │                                      └── [ ] Wireframe homepage
  │                                      └── [ ] Wireframe gallery
  ...
```

### Tag Convention

| Tag | Where | Purpose |
|-----|-------|---------|
| `#user-story` | Home Kanban cards | High-level epics / features |
| `#task` | Project task files | Granular work items |
| `#hola-cafre`, etc. | Both | Project-specific filtering |

### User Story Card Format

```markdown
- [ ] #user-story #hola-cafre [[Hola Cafre/Tasks/Web Design|Web Design]] 📅 2026-05-01 ⏫
```

### Granular Task Format

```markdown
- [ ] #task #hola-cafre Prepare Web Sketch 🛫 2026-05-01 ⏫
```

Tasks use emoji markers for priority (`⏫` high, `🔼` medium, `🔽` low),
dates (`📅` due, `🛫` start, `⏳` scheduled), and completion (`✅ YYYY-MM-DD`).
These follow the Tasks plugin syntax and are parsed by both the Dataview and
Tasks plugins.

---

## Color Coding

| Domain | Color | Hex |
|--------|-------|-----|
| Web Dev, Cybersec, Desktop Dev, Game Dev | Blue | `#458588` |
| Creative | Green | `#98971a` |
| References, DIY | Red | `#cc241d` |
| Health, Home, Assets, and others | Yellow | `#d79921` |

Colors are applied to the **Navigator card image** (colored folder SVG),
the **Link.md frontmatter**, and the **file tree** (via the File Color plugin).

---

## Workspace System

Six workspaces are currently saved:

| Workspace | Main panes | Purpose |
|-----------|-----------|---------|
| **Home** | Navigator · Kanban · Welcome | Dashboard |
| **Hola Cafre** | Wiki · Tasks+Draw+Roadmap · Timer | Project workspace |
| **Babylon** | Wiki · Tasks+Draw+Roadmap · Timer | Project workspace |
| **Pexá Studio** | Wiki · Tasks+Draw+Roadmap · Timer | Project workspace |
| **Escalada** | Wiki · Tasks+Draw+Roadmap · Timer | Project workspace |

All project workspaces share the same layout:

```
┌───────────────────────────┐
│ Wiki.md                   │  Top: project wiki (source mode)
├─────────────────┬─────────┤
│ Tasks.md        │         │
│ Draw.md         │ Timer   │  Bottom-left: task index, drawing, roadmap
│ Roadmap.canvas  │         │  Bottom-right: pomodoro timer
└─────────────────┴─────────┘
```

The Home workspace loads on startup. Clicking a project card in the Navigator
switches to that project's workspace, which opens all 4 project files with the
right sidebar collapsed for a focused, full-width view.

Workspace switching is powered by **Workspaces Plus** (`workspaces-plus` v0.3.3)
with commands triggered from `dataviewjs` blocks in each project's Link.md.

---

## Plugins

### Enabled (20)

| Plugin | Role |
|--------|------|
| **Iconize** (`obsidian-icon-folder`) | Folder and file icons |
| **File Color** (`obsidian-file-color`) | Color-coded folders in the file tree |
| **Colored Tags** | Tag colorization |
| **Kanban** (`obsidian-kanban`) | Global user-story board |
| **Excalidraw** (`obsidian-excalidraw-plugin`) | Diagrams and sketches per project |
| **Calendar** | Sidebar calendar for daily notes |
| **Pixel Banner** (`pexels-banner`) | Animated GIF banners on dashboards |
| **Dataview** | Dynamic queries, `dataviewjs` workspace triggers, progress bars |
| **Bases** (core) | Card-based project navigator |
| **Workspaces Plus** (`workspaces-plus`) | Save and switch between named workspace layouts |
| **Homepage** | Open Welcome page on startup |
| **Commander** (`cmdr`) | Custom command palette entries |
| **Hider** (`obsidian-hider`) | Hide UI elements for clean workspace |
| **Omnisearch** | Fast vault-wide search |
| **Style Settings** (`obsidian-style-settings`) | Theme customization |
| **Code Styler** | Code block styling |
| **File Explorer++** (`file-explorer-plus`) | Filter and pin files in explorer |
| **Ninja Cursor** | Enhanced cursor visibility |
| **Heatmap Calendar** (`heatmap-calendar`) | Activity heatmaps |
| **Widgets** | Embedded widgets (clock, etc.) |
| **Pomodoro Timer** (`pomodoro-timer`) | Focus timer per workspace |

### Available but Disabled

`obsidian-tasks-plugin`, `obsidian-advanced-uri`, `quickadd`, `buttons`,
`data-cards`, `crafty`, `advanced-canvas`, `file-explorer-note-count`

> **Note:** The vault uses Tasks plugin syntax (`#task`, emoji markers) throughout
> task files, and `tasks` query blocks in `Tasks.md`. These require the
> `obsidian-tasks-plugin` to be enabled for full query functionality.
> DataviewJS progress bars and tables in `Tasks.md` work independently.

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
2. Create 7 template files and directories:
   - `Link.md` — navigator card with workspace URI
   - `Tasks.md` — dynamic task index with DataviewJS
   - `Tasks/` — folder for per-story task files (at least one `.md`)
   - `Wiki.md` — project knowledge base
   - `Wiki/` — sub-pages (Architecture, Setup, Components, API)
   - `Roadmap.canvas` — empty canvas
   - `Draw.md` — empty Excalidraw sketch
3. Duplicate the Hola Cafre workspace in `workspaces.json` and update file paths
4. Pick the color SVG and hex based on the domain
5. Add a `#user-story` card to the Home Kanban linking to a task file

This is automated by the **project-creator AI skill**, which can create a
fully wired project with a single prompt.

The Navigator picks up new projects automatically — any note tagged `Project`
appears as a card.

---

## Requirements

- [Obsidian](https://obsidian.md/) v1.12.7 or later
- Community plugins listed above (installed and enabled)
- Core plugin **Bases** must be enabled
- Core plugin **Workspaces** must be enabled
- Core plugin **Canvas** must be enabled
- Enable `obsidian-tasks-plugin` for task query blocks (optional but recommended)

---

## Acknowledgements

- Folder SVGs from the [Gruvbox Folder Icons](https://github.com/Snailedlt/obsidian-gruvbox-folders) collection
- Pixel banner GIFs for dashboard headers
- All plugin authors credited in their respective repositories
