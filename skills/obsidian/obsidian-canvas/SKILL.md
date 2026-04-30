---
name: obsidian-canvas
description: >
  Obsidian Canvas + Advanced Canvas plugin manager. Use for creating and
  modifying .canvas files with nodes, edges, groups, presentations, and
  flowcharts.
  Triggers: canvas, mind map, flowchart, presentation, canvas node, canvas edge.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugins: canvas (core), advanced-canvas v6.0.1
  PRECEDENCE: This skill overrides obsidian-core for all canvas features.
---

# Obsidian Canvas + Advanced Canvas

Core canvas + Advanced Canvas plugin v6.0.1

## CANVAS FILE FORMAT (.canvas)

Canvas files are JSON with `.canvas` extension:

```json
{
  "nodes": [
    {
      "id": "abc123",
      "type": "file",
      "file": "My Note.md",
      "subpath": "#heading",
      "x": 0, "y": 0,
      "width": 400, "height": 300,
      "color": "1"
    },
    {
      "id": "def456",
      "type": "text",
      "text": "**Bold** text card\n\n- bullet\n- list",
      "x": 500, "y": 0,
      "width": 300, "height": 200,
      "color": "4"
    },
    {
      "id": "ghi789",
      "type": "link",
      "url": "https://example.com",
      "x": 1000, "y": 100,
      "width": 400, "height": 300
    },
    {
      "id": "grp1",
      "type": "group",
      "label": "My Section",
      "background": "Assets/bg.png",
      "backgroundStyle": "cover",
      "x": -300, "y": -150,
      "width": 900, "height": 600,
      "color": "5"
    }
  ],
  "edges": [
    {
      "id": "e1",
      "fromNode": "abc123",
      "fromSide": "right",
      "fromEnd": "none",
      "toNode": "def456",
      "toSide": "left",
      "toEnd": "arrow",
      "color": "1",
      "label": "relates to"
    }
  ]
}
```

## NODE TYPES

| Type | Key Fields | Purpose |
|------|-----------|---------|
| `"file"` | `file` (path), `subpath?` (#heading or #^blockid) | Vault file reference |
| `"text"` | `text` (markdown string) | Free-form text card |
| `"link"` | `url` (string) | External URL |
| `"group"` | `label?`, `background?`, `backgroundStyle?` | Visual container |

## NODE COMMON FIELDS

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `id` | string | Yes | Unique within canvas |
| `type` | string | Yes | `file`, `text`, `link`, `group` |
| `x` | number | Yes | Pixels from left |
| `y` | number | Yes | Pixels from top |
| `width` | number | Yes | Card width |
| `height` | number | Yes | Card height |
| `color` | string | No | `"1"`-`"6"` or hex `"#FF5733"` |

## COLOR PRESETS

| Value | Color |
|-------|-------|
| `"1"` | Red |
| `"2"` | Orange |
| `"3"` | Yellow |
| `"4"` | Green |
| `"5"` | Cyan/Blue |
| `"6"` | Purple |

## EDGE FIELDS

| Field | Type | Required | Values |
|-------|------|----------|--------|
| `id` | string | Yes | Unique ID |
| `fromNode` | string | Yes | Source node ID |
| `fromSide` | string | No | `"top"`, `"right"`, `"bottom"`, `"left"` |
| `fromEnd` | string | No | `"none"`, `"arrow"` |
| `toNode` | string | Yes | Target node ID |
| `toSide` | string | No | `"top"`, `"right"`, `"bottom"`, `"left"` |
| `toEnd` | string | No | `"none"`, `"arrow"` |
| `color` | string | No | Same as node colors |
| `label` | string | No | Edge label text |

## GROUP BACKGROUND STYLES

| Style | Behavior |
|-------|----------|
| `"cover"` | Image covers area (may crop) |
| `"ratio"` | Maintains aspect ratio |
| `"repeat"` | Tiles/repeats |

---

## ADVANCED CANVAS FEATURES

### Presentation Mode
Nodes become slides. Use Advanced Canvas to present.

### Flowchart Mode
Auto-layout for flowchart node graphs.

### Canvas Portals
Embed one canvas inside another.

### Collapsible Groups
Groups can collapse/expand.

---

## OPERATION PATTERNS

### Create a new canvas
1. Create `.canvas` file as JSON
2. Include `nodes` array: each with `id`, `type`, `x`, `y`, `width`, `height`
3. Include `edges` array for connections
4. Generate unique IDs for nodes and edges (random 6-char hex)

### Create a flowchart canvas
1. Use `"text"` type nodes for steps (supports markdown)
2. Use color `"4"` (green) for start, `"2"` (orange) for processes, `"1"` (red) for endpoints
3. Connect with edges: `fromEnd: "none"`, `toEnd: "arrow"`
4. Space nodes 400-500px apart, staggered vertically by 200-300px

### Create a mindmap canvas
1. Central node at (0, 0) or canvas center
2. First ring of children at ~400px radius
3. Connect central node to all children with edges
4. Second ring at ~800px, connected to first ring

### Add a file node
1. Node type `"file"` with `"file": "path/to/Note.md"`
2. For heading reference: `"subpath": "#heading-name"`
3. For block reference: `"subpath": "#^blockid"`

### Create a presentation
1. Group nodes into logical slides using `"type": "group"` nodes
2. Set each group with appropriate label
3. Arrange groups in linear order for presentation flow

### Layout guidelines
- Default node sizes: text 300x200, file 400x300, link 400x300
- Minimum spacing between unrelated nodes: 100px
- Edge default: `fromEnd: "none"`, `toEnd: "arrow"`
- Use color coding consistently across nodes of same type
