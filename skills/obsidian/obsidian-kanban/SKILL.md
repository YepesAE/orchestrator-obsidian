---
name: obsidian-kanban
description: >
  Obsidian Kanban plugin manager. Use for creating, reading, and modifying
  kanban boards with columns and cards. Boards are markdown files with special
  frontmatter and column syntax.
  Triggers: kanban, board, column, card, kanban board, create board.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: obsidian-kanban v2.0.51
  PRECEDENCE: This skill overrides obsidian-core for all kanban-related features.
---

# Obsidian Kanban Plugin

Plugin: obsidian-kanban v2.0.51
Config: `.obsidian/plugins/obsidian-kanban/data.json`

## BOARD FILE STRUCTURE

Kanban boards are markdown files with mandatory frontmatter:

```markdown
---

kanban-plugin: board

---

## Column Name

- [ ] Card in this column
- [ ] Another card with [[link to note]]
- [ ] Task with date 📅 2026-05-15
- [x] Completed card ✅ 2026-04-28

## Another Column

- [ ] Card in second column

%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[false,false]}
```
%%
```

### Critical Rules

1. **Frontmatter MUST contain**: `kanban-plugin: board`
2. **Columns are `## Heading` lines** — each becomes a lane
3. **Cards are checklist items** (`- [ ]`) under column headings
4. **Settings block** (`%% kanban:settings %%`) stores lane collapse state as JSON — optional, plugin auto-creates it
5. Cards can use **full Tasks plugin syntax** (emojis, dates, priorities, recurrence)

### Column Max Items

```markdown
## Column Name (5)
```

The `(5)` limits the column to 5 visible cards.

### Archive Support

```yaml
---

kanban-plugin: board
archive: false

---
```

Or with timestamp: `archive: 1680134400000`

### Settings Block JSON

```json
{"kanban-plugin":"board","list-collapse":[false,false,false,false]}
```

- `list-collapse` array: one boolean per column (true = collapsed)
- Must match column count
- Fenced with ` ``` ` inside `%% kanban:settings %%` comment

---

## CARD FORMAT REFERENCE

Cards support all standard Obsidian markdown:

```markdown
- [ ] Basic card
- [ ] Card with **bold** and *italic*
- [ ] Card linking to [[Other Note]]
- [ ] Card with nested content
    - Sub-item
    - Another sub-item
- [ ] #task Tagged task card 📅 2026-05-01 ⏫
- [ ] Card with date metadata {2026-05-15}
```

Cards can have indented sub-content (nested bullets, text, code blocks).

---

## OPERATION PATTERNS

### Create a new board
1. Create `.md` file with frontmatter `kanban-plugin: board`
2. Add `## Column Name` headings for each column
3. Add `- [ ]` checklist items as cards under columns
4. Include `%% kanban:settings %%` block (optional, plugin auto-creates)

### Add a card to a column
1. Read the board file
2. Find the target `## Column Name` heading
3. Insert `- [ ] card description` on a new line under that heading
4. Add any task syntax (dates, priorities, tags) as needed
5. Write the file

### Move a card between columns
1. Read the board file
2. Find the card line under its current column
3. Cut the entire line (all content on that line and any indented sub-content)
4. Paste under the target `## Column` heading
5. Write the file

### Complete a card
1. Change `- [ ]` to `- [x]`
2. Add `✅ YYYY-MM-DD` timestamp
3. Optionally move to a "Done" column

### Remove a card
1. Delete the card line and any indented sub-content
2. Leave a blank line if needed for spacing

### Change column order
1. Reorder the `## Heading` sections in the file
2. Columns render in source order

### Rename a column
1. Change the `## Old Name` heading to `## New Name`
2. Cards stay under the renamed column
3. Update `list-collapse` array position if needed (settings block)

### Archive a board
1. Change frontmatter: `archive: 1680134400000` (epoch ms)
2. Or `archive: true`
3. Board still exists but shows as archived in UI
