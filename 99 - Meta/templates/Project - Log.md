<%*
if (tp.file.title.startsWith("Untitled")) {
    await tp.file.rename(`Log - ${tp.date.now()}`);
}
-%>
---
created:
  - <% tp.file.creation_date() %>
tags:
  - project/log
---
