---
name: obsidian-heatmap
description: >
  Obsidian Heatmap Calendar plugin manager. Use for creating GitHub-style
  activity heatmaps using DataviewJS. Track goals, habits, tasks, exercise,
  finances over time.
  Triggers: heatmap, heatmap calendar, activity tracker, habit tracker, goal tracker.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: heatmap-calendar v0.7.1
  PRECEDENCE: This skill overrides obsidian-core for all heatmap features.
---

# Obsidian Heatmap Calendar Plugin

Plugin: heatmap-calendar v0.7.1
Config: `.obsidian/plugins/heatmap-calendar/data.json`

## HEATMAP RENDER BLOCK

Insert heatmap calendar via DataviewJS code block:

```javascript
```dataviewjs
const calendarData = {
  entries: [],
  year: 2026,
  intensityScaleStart: 4,
  intensityScaleEnd: 10,
  defaultEntryIntensity: 4,
  showCurrentDayBorder: true,
  color: "var(--text-accent)"
}

renderHeatmapCalendar(this.container, calendarData)
```
```

## ENTRY FORMAT

Each entry in the `entries` array:

```javascript
{
  date: "2026-04-29",
  intensity: 8,
  content: "Wrote 500 words",
  color: "green"    // optional: override color for this day
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `date` | Yes | `"YYYY-MM-DD"` format |
| `intensity` | Yes | Number within intensity scale range |
| `content` | No | Tooltip text on hover |
| `color` | No | Override color for this entry (`"green"`, `"red"`, `"blue"`, `"orange"`) |

## CALENDAR DATA OPTIONS

```javascript
const calendarData = {
  year: 2026,                         // Year to display
  entries: [],                        // Array of entry objects
  intensityScaleStart: 4,             // Min intensity to show color
  intensityScaleEnd: 10,              // Max intensity (darkest shade)
  defaultEntryIntensity: 4,           // Default if not specified
  showCurrentDayBorder: true,         // Highlight today
  defaultColor: "var(--text-accent)", // Base color
  color: "var(--text-accent)",        // Heatmap color (CSS variable or hex)
  lastUpdate: "2026-01-01",           // Optional: when data was last refreshed
  gutterValue: 5,                     // Spacing between cells
  locale: "en",                       // For day/month labels
  showMonthLabels: true,              // Show month names
  showDayLabels: true,                // Show day names
  startWeekOnMonday: true             // Monday start (false = Sunday)
}
```

---

## OPERATION PATTERNS

### Create a habit tracker
1. Create a `.md` note for the tracker
2. Add DataviewJS block with `renderHeatmapCalendar`
3. Initialize `entries` array empty
4. Set `year` to current year
5. Use appropriate intensity scale for the habit (e.g., 1-5 for days/week)

### Create a goal progress tracker
1. Define entry for each date with goal completion data
2. Use `content` field for detailed tooltip
3. Use `color: "green"` for met goals, `"red"` for missed

### Create a task completion tracker
1. Query Tasks plugin for completed tasks per day
2. Count completions per date
3. Map count to intensity (more completions = higher intensity)
4. Render as heatmap

### Update tracker data
1. Read the note containing the heatmap
2. Find the DataviewJS block
3. Add new entries to the `entries` array
4. Set `intensity` based on activity level

### Multiple trackers in one note
```javascript
```dataviewjs
// Tracker 1: Writing habit
renderHeatmapCalendar(this.container, {
  entries: [{date: "2026-04-28", intensity: 8, content: "1000 words"}],
  year: 2026,
  color: "green"
})
```

```dataviewjs
// Tracker 2: Exercise
renderHeatmapCalendar(this.container, {
  entries: [{date: "2026-04-28", intensity: 5, content: "30 min run"}],
  year: 2026,
  color: "var(--text-accent)"
})
```
```

### Empty heatmap template
```javascript
```dataviewjs
renderHeatmapCalendar(this.container, {
  entries: [],
  year: new Date().getFullYear(),
  color: "var(--text-accent)",
  showCurrentDayBorder: true
})
```
```
