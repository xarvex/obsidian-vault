<%*
if (tp.file.title.startsWith("Untitled")) {
    await tp.file.rename(`Meeting - ${tp.date.now()}`);
}
-%>
---
created:
  - <% tp.file.creation_date() %>
tags:
  - personal/meeting
---

## Plan

## Expectations

- [ ]
