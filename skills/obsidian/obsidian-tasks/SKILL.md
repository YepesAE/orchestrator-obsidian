---
name: obsidian-tasks
description: >
  Obsidian Tasks plugin manager. Use for creating, querying, completing, and
  modifying task items with dates, priorities, recurrence, and dependencies.
  Triggers: task, tasks, todo, due date, priority, recurring, task query,
  checklist, complete task.
  Vault path: /home/yepes/Documents/Vaults/Orchestrator/
  Plugin ID: obsidian-tasks-plugin v7.23.1
  PRECEDENCE: This skill overrides obsidian-core for all task-related features.
---

# Obsidian Tasks Plugin

Plugin: obsidian-tasks-plugin v7.23.1
Config: `.obsidian/plugins/obsidian-tasks-plugin/data.json`

## TASK FORMAT

```markdown
- [ ] #task Simple task
- [ ] #task Task with due date 📅 2026-05-15
- [ ] #task Scheduled task ⏳ 2026-04-20
- [ ] #task Started 🛫 2026-04-25
- [ ] #task Recurring 🔁 every day
- [x] #task Completed ✅ 2026-04-29
```

### Priority Markers

| Marker | Priority |
|--------|----------|
| `🔺` | Highest |
| `⏫` | High |
| `🔼` | Medium |
| `🔽` | Low |
| (none) | Normal |

### Recurrence Syntax

```markdown
- [ ] #task Standup 🔁 every weekday ⏳ 2026-04-28
- [ ] #task Report 🔁 every month on the 1st ⏳ 2026-05-01
- [ ] #task Sprint 🔁 every 2 weeks on Friday ⏳ 2026-04-24
- [ ] #task Review 🔁 every year on January 1st
```

### Dependencies

```markdown
- [ ] #task Blocker task 🆔 abc123
- [ ] #task Depends on blocker ⛔ abc123
```

### Full Metadata Task

```markdown
- [ ] #task Write report 📅 2026-05-01 ⏫ 🔁 every month ⏳ 2026-04-01 🛫 2026-04-25 ➕ 2026-04-20 🆔 rpt-001
```

---

## TASK QUERY BLOCKS

````markdown
```tasks
not done
due before tomorrow
priority is high
group by filename
sort by due reverse
limit 50
```
````

### Status Filters

```tasks
not done
done
```

### Date Filters

```tasks
due today
due before tomorrow
due after 2026-01-01
due on or before 2026-05-15
due 2026-04-01 2026-04-30
starts before today
scheduled this week
happens today
no due date
has due date
done date is invalid
```

Date keywords: `last week/month/quarter/year`, `this week/month/quarter/year`, `next week/month/quarter/year`, `YYYY-Www`, `YYYY-MM`, `YYYY-QQ`

### Priority Filters

```tasks
priority is high
priority is above medium
priority is not none
```

### Text Filters

```tasks
description includes search term
description does not include text
heading includes section name
heading regex matches /pattern/
```

### Tag Filters

```tasks
tags include #home
tags do not include #work
tag regex matches /#book$/i
no tags
has tags
```

### Recurrence Filters

```tasks
is recurring
is not recurring
recurrence includes every week
```

### Dependency Filters

```tasks
is blocking
is not blocking
is blocked
has id
id includes abc

### Combining Filters

```tasks
(no due date) OR (due after 2026-04-30)
(has start date) AND (starts before tomorrow)
NOT (tags include #done)
```

### Custom Filter by Function

```tasks
filter by function task.due.format('dddd') === 'Tuesday'
filter by function task.urgency > 7.9999
filter by function !task.isRecurring
filter by function task.tags.length > 1
```

### Display Controls

```tasks
group by filename
group by due
group by heading
group by priority
group by tags
sort by due
sort by due reverse
sort by priority
sort by description
limit 50
limit groups 10
show tree
hide backlinks
hide edit button
hide task count
hide urgency
```

---

## OPERATION PATTERNS

### Add a task
1. Insert `- [ ] #task DESCRIPTION 📅 YYYY-MM-DD` under a heading in any `.md` file
2. Include priority marker if specified: `⏫`/`🔼`/`🔽`
3. Include recurrence if repeating: `🔁 every [period] [on DAY]`
4. For scheduled tasks add `⏳ YYYY-MM-DD`
5. For started tasks add `🛫 YYYY-MM-DD`

### Complete a task
1. Change `- [ ]` to `- [x]`
2. Add `✅ YYYY-MM-DD` (current date)
3. Keep all other emoji fields intact
4. If task is recurring, the plugin will auto-create next instance

### Query tasks
1. Use fenced code block ` ```tasks ` with filters
2. Always close with ` ``` `
3. Filter by status, date, priority, tags, heading, path as needed

### Move a task between headings
1. Cut the entire task line (with all emoji fields)
2. Paste under the target heading
3. Task queries using `heading includes` will auto-reflect the new location

### Change task date
1. Update the `📅 YYYY-MM-DD` value in the task line
2. Update `⏳` or `🛫` if those change too
3. Keep all other fields intact
