<%*
if (tp.file.title.startsWith("Untitled")) {
    let templateChoices = { [""]: "Other" };

    if (tp.file.folder().endsWith("Projects")) {
        templateChoices.about = "About";
    } else {
        if (!(await tp.file.exists(`${tp.file.folder(true)}/About.md`))) {
            templateChoices.about = "About";
        }
        templateChoices.log = "Log";
    }

    const template = await tp.system.suggester(
        Object.values(templateChoices),
        Object.keys(templateChoices),
    );

    if (template) {
        return tp.file.include(`[[Project - ${template}]]`);
    }
}
%>
