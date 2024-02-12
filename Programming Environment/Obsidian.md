# Obsidian Use Notes

## Internal Link

> Example

> [!note] Link with block identifier
> 
> This is my note. Link to it with an internal link.
> 
> - First, create an identifier following this block.
> - Then link to it using a markdown link in the following form:
> 
> > [!code] Markdown Link
> > \[display name](Note#^identifier)
> > \[display name](#^identifier) for linking blocks within the same note
> > 	
> > > [!tip]
> > > This also shows how to make nested admonitions.
> > 
> 
^internal-link

Here I link to the previous note using its block identifier: [Link to Note](Obsidian.md#^internal-link)

> [!info] Enter special characters
> 
> To enter space in links, type %20;
> To escape a special symbol like \[, type a \ before the symbol.
## External Link

> [!note]
> There are two formats to link to another note. One is the wikinote format, another is the markdown format. Use the markdown format because it is more specific.
> > [!code] Markdown Link
> > \[Displayed name](Note.md)
> > >[!warning]
> > >Do not create notes with the same name!

> [!note] Link with headings
> 
> Alternatively, links can be created using headings. For linking headings within the same note, just type \[display name](#heading name). For linking outside headings, type \[display name](note.md#heading).

> [!note] Enter links fast
> 
> Type \[\[ to open an interface that can be used to visually select and create links.

## Admonitions

A way to insert highlighted blocks of text.

> [!summary]
> With a book icon. Use this to give definitions.

> [!note]
> With a pen icon. Use this to write a note in your own words.

> [!info]
> With a ! icon. Use this to document additional noteworthy information about something.

> [!info] Using Native Callouts
> Links in the original admonitions within codeblocks are not recognized, but they can be recognized in native callouts in Obsidian. 
> 
> To change the appearance of the native callouts, add custom styles in admonitions settings pane, export them as css, and add the css files into the css snippets folder in the vault.
> 
> Also note that admonitions are easier to use. So only use native callouts when there is a link in it.

## Vault Settings

The appearances and add-ins are distinct for each vault. To easily port settings for one vault to another, just copy the `.obsidian` folder or create a [symlink (macos)](File%20Links.md#^macoslink) or [junction (windows)](File%20Links.md#^windowslink).

## Tags

- Label note topics, or use it to group notes.
- Type #, not followed by a space.
- Or add it using the [tag property](https://help.obsidian.md/Editing+and+formatting/Tags)

````ad-code
title: Using the Tag Property

```
---
tags:
 - Tag1
 - Tag2
---
```

````

## Code Block Syntax Highlighting

Add different highlighting to code languages in code blocks by add the language name to the code block. See supported languages [here](https://prismjs.com/#supported-languages).

Common ones I use:
- r
- python, py
- shell, sh, bash

## Footnote

- Use `[^number]` or `[^name]` to add a footnote. 
- Add 2 spaces before the the second and further lines to write a multi-line footnote.
- Write the footnote in-line.^[An in-line footnote.]
- Footnotes can only be viewed in reading mode.
- Numbered automatically.

Add a footnote[^demo]

[^demo]: Add 2 spaces at the start of each new line. 
  This lets you write footnotes that span multiple lines.

Another note[^3]

[^3]: This is another footnote
  Yes, the same one even though this line is larger.