# pandoc

Pandoc is used for converting between markup language file types.

## macOS

### Install

- Installed with homebrew. Command:
`brew install pandoc`
`brew install librsvg homebrew/cask/basictex`
- This also installs [BasicTex](https://tug.org/mactex/morepackages.html), a trimmed down version of [LaTeX](LaTeX.md). Pandoc uses LaTeX to make pdfs.
- After installing, add the path of pandoc to the `$PATH` environment variable.

### Add `$PATH`

- Necessary for apps to find where pandoc is
- Find [where pandoc is installed](homebrew.md#Location%20of%20Packages)
- Write down the path: `/opt/homebrew/Cellar/pandoc/3.1.9/bin/pandoc` or `/opt/homebrew/bin/pandoc`
- Add the path to `/etc/paths`

## markdown to pdf

``` shell
pandoc -f markdown-implicit_figures -t html assignment\ report.md | pandoc -f html --pdf-engine=xelatex -o report.pdf
```

convert to html first to use the html img tag to control image width and location.