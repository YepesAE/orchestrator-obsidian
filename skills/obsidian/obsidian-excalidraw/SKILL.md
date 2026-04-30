---
name: obsidian-excalidraw
description: >
  Obsidian Excalidraw plugin manager. Use for creating, reading, and modifying
  Excalidraw drawing files (.excalidraw.md). Supports programmatic diagram
  generation with elements, appState, and scripting.
  Triggers: excalidraw, drawing, diagram, sketch, flowchart, mindmap, excalidraw script.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: obsidian-excalidraw-plugin v2.22.1
  PRECEDENCE: This skill overrides obsidian-core for all Excalidraw features.
---

# Obsidian Excalidraw Plugin

Plugin: obsidian-excalidraw-plugin v2.22.1
Config: `.obsidian/plugins/obsidian-excalidraw-plugin/data.json`

## FILE FORMAT (.excalidraw.md)

Excalidraw files use `.excalidraw.md` extension and contain three sections:

```markdown
---
excalidraw-plugin: parsed
excalidraw-autoexport: png
excalidraw-link-prefix: "📍"
tags: [diagram]
---

# Optional free-text area
This text is preserved by the plugin and not rendered on canvas.

# Text Elements
Visible text on the canvas
[[Linked Page]]

# Drawing
```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "https://marketplace.obsidian.md/plugins/obsidian-excalidraw-plugin",
  "elements": [],
  "appState": { "gridSize": null, "viewBackgroundColor": "#ffffff" },
  "files": {}
}
```
```

### Frontmatter Options

| Key | Values | Description |
|-----|--------|-------------|
| `excalidraw-plugin` | `parsed` | Required for plugin processing |
| `excalidraw-autoexport` | `none`, `both`, `png`, `svg` | Auto-export on save |
| `excalidraw-link-prefix` | String | Prefix for link icons |
| `excalidraw-default-mode` | `view`, `zen` | Default view mode |
| `excalidraw-export-transparent` | `true`/`false` | Transparent background |
| `excalidraw-export-dark` | `true`/`false` | Dark mode export |
| `excalidraw-export-padding` | Number | Export padding in px |
| `excalidraw-export-pngscale` | Number | PNG scale factor |
| `excalidraw-font` | `Virgil`, `Cascadia`, or custom | Font family |
| `excalidraw-font-color` | Hex color | Font color |
| `excalidraw-border-color` | Color name/hex | Border color |

---

## DRAWING JSON STRUCTURE

```json
{
  "type": "excalidraw",
  "version": 2,
  "elements": [
    {
      "id": "element-1",
      "type": "rectangle",
      "x": 100, "y": 100,
      "width": 200, "height": 100,
      "strokeColor": "#1e1e1e",
      "backgroundColor": "#a5d8ff",
      "fillStyle": "solid",
      "strokeWidth": 2,
      "roughness": 1,
      "opacity": 100,
      "roundness": null,
      "angle": 0,
      "strokeStyle": "solid",
      "groupIds": [],
      "frameId": null,
      "boundElements": [],
      "updated": 1,
      "link": null,
      "locked": false
    }
  ],
  "appState": {
    "gridSize": null,
    "viewBackgroundColor": "#ffffff",
    "zoom": { "value": 1 },
    "offsetTop": 0,
    "offsetLeft": 0,
    "theme": "light"
  },
  "files": {}
}
```

### Element Types

| Type | Key Fields | Description |
|------|-----------|-------------|
| `rectangle` | `x`, `y`, `width`, `height` | Box shape |
| `ellipse` | `x`, `y`, `width`, `height` | Oval/circle |
| `diamond` | `x`, `y`, `width`, `height` | Diamond shape |
| `text` | `x`, `y`, `width`, `height`, `text`, `fontSize`, `fontFamily` | Text element |
| `arrow` | `x`, `y`, `width`, `height`, `points` | Line/arrow |
| `line` | `x`, `y`, `width`, `height`, `points` | Multi-point line |
| `freedraw` | `x`, `y`, `width`, `height`, `points` | Free-hand drawing |
| `image` | `x`, `y`, `width`, `height`, `fileId` | Embedded image |
| `frame` | `x`, `y`, `width`, `height`, `name` | Named frame/group |

### Element Common Properties

| Field | Type | Required | Default |
|-------|------|----------|---------|
| `id` | string | Yes | — |
| `type` | string | Yes | — |
| `x` | number | Yes | — |
| `y` | number | Yes | — |
| `width` | number | Yes | — |
| `height` | number | Yes | — |
| `strokeColor` | hex string | No | `"#1e1e1e"` |
| `backgroundColor` | hex string | No | `"transparent"` |
| `fillStyle` | `"solid"`, `"hachure"`, `"cross-hatch"` | No | `"solid"` |
| `strokeWidth` | number | No | 2 |
| `roughness` | number (0-2) | No | 1 |
| `opacity` | number (0-100) | No | 100 |
| `angle` | number (radians) | No | 0 |
| `groupIds` | string[] | No | `[]` |
| `link` | string or null | No | null |
| `locked` | boolean | No | false |

### Arrow / Line Points

```json
{
  "type": "arrow",
  "points": [[0, 0], [200, 50]],
  "startArrowhead": "arrow",
  "endArrowhead": "arrow"
}
```

Arrowhead options: `"arrow"`, `"bar"`, `"dot"`, `"triangle"`, `null`

### Text Properties

```json
{
  "type": "text",
  "text": "Hello World",
  "fontSize": 20,
  "fontFamily": 1,
  "textAlign": "left",
  "verticalAlign": "top"
}
```

Font families: `1` (Virgil), `2` (Helvetica), `3` (Cascadia), `4` (Assistant, local font)

---

## EMBEDDING DRAWINGS

```markdown
![[drawing.excalidraw|300]]              # Width
![[drawing.excalidraw|300x200]]          # Width x height
![[drawing.excalidraw|100|left]]         # Width | alignment
![[drawing.excalidraw|right-wrap]]       # Wrap alignment

# Block references
[[drawing#^elementID]]                   # Reference element
[[drawing#^group=elementID]]             # Select group
[[drawing#area=Section heading]]          # Area cutout
```

---

## SCRIPTING (ExcalidrawAutomate)

Scripts stored in vault, run via Script Engine:

```javascript
const ea = ExcalidrawAutomate;
ea.reset();
ea.style.strokeColor = "#1e1e1e";
ea.style.backgroundColor = "#a5d8ff";
ea.style.fillStyle = "solid";

ea.addText(100, 100, "Hello World");
ea.addRect(50, 50, 200, 100);
ea.connectObjects("rect1", "text1");

await ea.create({ filename: "output" });
```

---

## OPERATION PATTERNS

### Create a new drawing
1. Create `.excalidraw.md` file
2. Include frontmatter with `excalidraw-plugin: parsed`
3. Add `# Text Elements` section with visible text
4. Add `# Drawing` section with ` ```json ... ``` ` drawing data
5. Initialize with empty elements array and default appState

### Add elements to a drawing
1. Read existing `.excalidraw.md` file
2. Parse the `# Drawing` JSON
3. Add new element objects to `elements` array with unique IDs
4. Write back the full file

### Create a flowchart diagram
1. Use `rectangle` elements for process steps
2. Use `diamond` elements for decisions
3. Use `arrow` elements for connections
4. Use `text` elements for labels
5. Space elements 200px apart horizontally, 150px vertically
6. Use `fillStyle: "solid"` with light background colors

### Create a mindmap
1. Use `ellipse` for the central node
2. Use `ellipse` or `rectangle` for child nodes radiating outward
3. Use `arrow` or `line` for connections
4. Position children in concentric rings around center

### Embed a drawing
1. Use `![[filename.excalidraw|width]]` syntax
2. Optionally specify dimensions: `|300x200` or just `|300`
3. For block refs: `[[filename#^elementID]]`
