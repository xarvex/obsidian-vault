---
tags:
  - note/meta
---

```dataviewjs
const folder = dv.current().file.folder;

dv.table(
    ["Project", "Info", "Tags", "Tasks"],
    dv
        .pages(`"${folder}" and #project/about`)
        .file.groupBy((file) => file.folder)
        .sort((group) => group.rows.mtime.ts.max(), "desc")
        .map((group) => {
            const project =
                group.key == folder
                    ? group.rows[0].name
                    : group.key.slice(folder.length + 1);
            const files = group.rows.map((file) => file.link);
            const tags = group.rows.etags.filter(
                (tag) => tag != "#project/about",
            );
            const tasks = dv.markdownTaskList(group.rows.tasks);

            return [project, files, tags, tasks];
        }),
);
```
