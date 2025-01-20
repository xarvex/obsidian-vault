<%*
if (tp.file.title.startsWith("Untitled")) {
    await tp.file.rename(
        tp.file.folder().endsWith("Projects")
            ? await tp.system.prompt("Project name:")
            : "About",
    );
}

const languageChoices = {
    assembly: "Assembly",
    c: "C",
    cpp: "C++",
    go: "Go",
    java: "Java",
    javascript: "JavaScript",
    kotlin: "Kotlin",
    lua: "Lua",
    nix: "Nix",
    python: "Python",
    rust: "Rust",
    shell: "shellscript",
    typescript: "TypeScript",
    vala: "Vala",
    zig: "Zig",
};

const languages = [];
const languageSelection = { ...languageChoices };
while (true) {
    const language = await tp.system.suggester(
        Object.values(languageSelection),
        Object.keys(languageSelection),
    );

    if (language == null) {
        break;
    } else {
        languages.push(language);
        delete languageSelection[language];
    }
}
delete languageSelection;
-%>
---
created:
  - <% tp.file.creation_date() %>
tags:
<% languages.toSorted().map((language) => `  - programming/language/${language}`).join("\n") %>
  - project/about
---

> **`$= const lastFolder = dv.current().file.folder.substring(dv.current().file.folder.lastIndexOf("/") + 1); lastFolder.endsWith("Projects") ? dv.current().file.name : lastFolder`** is <% tp.system.prompt(`What is the project?`, "a") %> written in <% (new Intl.ListFormat("en")).format(languages.map((language) => languageChoices[language])) %>.<% tp.file.cursor() %>

```dataviewjs
const folder = dv.current().file.folder;

if (!folder.substring(folder.lastIndexOf("/") + 1).endsWith("Projects")) {
    dv.span(
        `**${dv.fileLink(`${folder}/Log - ${dv.luxon.DateTime.now().toFormat(dv.settings.defaultDateFormat)}`, false, "Today's Log")}**`,
    );
    dv.el("br");
    dv.el("br");
}
```

## Design

1.

### Current Tasks

- [ ]

#### Expectations

-

---

## Resources

-

### Libraries

-

### Inspiration

-
