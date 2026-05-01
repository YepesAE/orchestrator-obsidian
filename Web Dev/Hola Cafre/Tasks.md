---
title: Hola Cafre Tasks
color: "#458588"
tags:
  - Project
  - hola-cafre
image: "[[folder-gruvbox-original-blue.svg]]"
uri: "obsidian://adv-uri?vault=Orchestrator&commandid=workspace%3Aload&uid=Project%20Layout&filepath=Web%20Dev%2FHola%20Cafre%2FTasks&filepath=Web%20Dev%2FHola%20Cafre%2FDraw&filepath=Web%20Dev%2FHola%20Cafre%2FRoadmap&filepath=Web%20Dev%2FHola%20Cafre%2FWiki"
---

# Task Index

```dataviewjs
const pages = dv.pages('"Web Dev/Hola Cafre/Tasks"');
const tasks = pages.file.tasks;
const total = tasks.length;
const done = tasks.where(t => t.completed).length;
const pct = total > 0 ? Math.round(done / total * 100) : 0;

dv.span(`**Progress:** ${done}/${total} (${pct}%)`);
dv.span(`  \`${"▓".repeat(Math.round(pct/5))}${"░".repeat(20-Math.round(pct/5))}\``);

if (pages.length === 0) {
  dv.paragraph("*No task files yet. Create one in `Tasks/` to see it here.*");
}
```

---

## Task Files

```dataviewjs
const pages = dv.pages('"Web Dev/Hola Cafre/Tasks"');
if (pages.length === 0) {
  dv.paragraph("*No task files found in the `Tasks/` folder.*");
} else {
  dv.table(
    ["File", "Open", "Done", "Progress"],
    pages.map(p => {
      const total = p.file.tasks.length;
      const done = p.file.tasks.where(t => t.completed).length;
      const pct = total > 0 ? Math.round(done / total * 100) : 0;
      return [
        dv.fileLink(p.file.path),
        total,
        done,
        `${pct}%`
      ];
    })
  );
}
```

---

## All Open Tasks

```tasks
path includes Hola Cafre/Tasks
not done
sort by priority reverse
group by filename
```
