# LaTeX

A typesetting language

## Installation

Choose a distribution: BasicTeX, MikTeX, TeX Live (MacTex).
I chose BasicTex. MacTeX is the complete version and very large. MikTeX does not come with perl.

Install via [homebrew](homebrew.md): 
> [!code] bash
> brew install homebrew/cask/basictex
^912efa

## Update tlmgr

`sudo tlmgr update --self --all`

## Package manager

`tlmgr`

Install fonts:  `sudo tlmgr install collection-fontsrecommended`
Install latexmk: `sudo tlmgr install latexmk`

> [!warning] Perl
> 
> latexmk requires Perl, and MacOS already has Perl installed.
> Enter `Perl -v` in the terminal to find out.

Install framed `sudo tlmgr install framed`

## LaTeX Workshop

- Write and build LaTeX in VS Code
- [Install](https://github.com/James-Yu/LaTeX-Workshop/wiki/Install)
- [Video Instructions](https://www.youtube.com/watch?v=CmagZthwhaY)
- `latexmk` is required for the default recipe for building LaTeX projects to work.

## OCR service to generate LaTeX math formulas

[Link](https://simpletex.cn/ai/latex_ocr)

## Code snippets

$$\operatorname*{argmin}_\boldsymbol{\phi}$$
