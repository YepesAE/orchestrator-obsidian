---
name: obsidian-pixel-banner
description: >
  Obsidian Pixel Banner plugin manager. Use for adding customizable banner
  images to notes via frontmatter. Supports AI-generated banners, local images,
  and a curated banner store.
  Triggers: banner, pixel banner, header image, note banner, banner image.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: pexels-banner v3.6.18
  PRECEDENCE: This skill overrides obsidian-core for all banner-related features.
---

# Obsidian Pixel Banner Plugin

Plugin: pexels-banner v3.6.18
Config: `.obsidian/plugins/pexels-banner/data.json`

## BANNER FRONTMATTER

Add banner images to notes via YAML frontmatter:

```yaml
---
banner: "Assets/banners/project-bg.jpg"
banner-y: 50
banner-icon: LiFolderKanban
---
```

| Field | Description |
|-------|-------------|
| `banner` | Path to local image or URL |
| `banner-x` | Horizontal position (0-100, default 50) |
| `banner-y` | Vertical position (0-100, default 50) |
| `banner-icon` | Lucide icon name (e.g., `LiFolderKanban`) |
| `banner-hue` | CSS hue-rotate filter (degrees) |
| `banner-particles` | `true`/`false` for particle effects |

## IMAGE SOURCES

- **Local vault images**: `"banner": "Assets/banners/image.jpg"`
- **External URLs**: `"banner": "https://example.com/image.jpg"`
- **AI-generated**: Via plugin's built-in AI generation feature
- **Curated store**: Plugin includes a downloadable banner collection

---

## OPERATION PATTERNS

### Add a banner to a note
1. Open the `.md` file
2. Add `banner: "path/to/image.jpg"` to YAML frontmatter
3. Optionally set `banner-y` for vertical alignment (0 = top, 50 = center, 100 = bottom)
4. Optionally set `banner-icon` for an overlay icon

### Remove a banner
1. Delete `banner` field from frontmatter
2. Optionally remove `banner-x`, `banner-y`, `banner-icon` fields

### Adjust banner position
1. Modify `banner-x` (horizontal) and `banner-y` (vertical) values
2. Values 0-100, default 50 for center
3. `banner-y: 20` = show top portion; `banner-y: 80` = show bottom

### Add a banner icon overlay
1. Add `banner-icon: LiIconName` to frontmatter
2. Uses Lucide icons (same as Iconize)

### Use a themed banner (hue rotation)
1. Add `banner-hue: 180` to frontmatter
2. Rotates the image hue to match theme
3. Value in degrees (0-360), 0 = no change
