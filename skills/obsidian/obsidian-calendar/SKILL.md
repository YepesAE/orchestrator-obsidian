---
name: obsidian-calendar
description: >
  Obsidian Calendar plugin manager. Use for creating daily notes, navigating
  calendar views, and configuring the Calendar plugin.
  Triggers: calendar, daily note, calendar view, week view, calendar config.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: calendar v1.5.10
  PRECEDENCE: This skill overrides obsidian-core for calendar/daily-note features.
---

# Obsidian Calendar Plugin

Plugin: calendar v1.5.10
Config: `.obsidian/plugins/calendar/data.json`

## PLUGIN OVERVIEW

The Calendar plugin provides a sidebar calendar view for navigating and creating
daily notes. It does NOT manage events — it focuses on daily/weekly note navigation.

## DAILY NOTE FORMAT

Daily notes are standard `.md` files named by date:

```
YYYY-MM-DD.md          →  2026-04-29.md
yyyy-MM-dd.md          →  2026-04-29.md
YYYY/MM/DD.md          →  2026/04/29.md (folder structure)
```

The Calendar plugin highlights dates that have corresponding daily notes.

## WEEKLY NOTES

If enabled, weekly notes follow a configurable format:
```
YYYY-[W]ww.md          →  2026-W18.md
gggg-[W]ww.md          →  ISO week format
```

## CONFIGURATION

Config file: `.obsidian/plugins/calendar/data.json`

Common settings:
```json
{
  "wordsPerDot": 250,
  "shouldConfirmBeforeCreate": true,
  "weekStart": "locale"
}
```

- `wordsPerDot` — dots under calendar dates indicate note content volume
- `shouldConfirmBeforeCreate` — prompt before creating new daily notes
- `weekStart` — `"locale"`, `"sunday"`, or `"monday"`

---

## OPERATION PATTERNS

### Create a daily note
1. Determine filename from date format (default: `YYYY-MM-DD.md`)
2. Apply daily note template variables if configured:
   - `{{title}}` — filename without `.md`
   - `{{date}}` — current date
   - `{{date:FORMAT}}` — custom format
   - `{{time}}` — current time
   - `{{yesterday}}`, `{{tomorrow}}`
3. Write to the configured daily notes folder
4. Include YAML frontmatter with `tags: [daily-note]` and date

### Navigate calendar
- Calendar sidebar shows current month with dots indicating note density
- Click a date to open/create that day's note
- Use week view for weekly overview

### Create a weekly note
1. Calculate current ISO week: `YYYY-Www`
2. Create file at the configured weekly notes location
3. Include week-specific frontmatter: `week: YYYY-Www`

### Daily note template example
```markdown
---
tags: [daily-note]
date: {{date:YYYY-MM-DD}}
---

# {{date:dddd, MMMM D, YYYY}}

## Agenda
- [ ] 

## Notes

## Tasks
- [ ] 

## Reflection
```
