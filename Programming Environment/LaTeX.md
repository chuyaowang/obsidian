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



| Replicate | Sample | Group |
| --------- | ------ | ----- |
| 1         | 1      | 1     |
| 2         | 2      | 1     |
| 3         | 3      | 1     |
| 1         | 4      | 2     |
| 2         | 5      | 2     |
| 3         | 6      | 2     |


Breast cancer is the most frequently diagnosed cancer in women worldwide. Discerning between cancer subtypes is critical for selecting the optimal treatment plan for the patient. In particular, HER2+ cancer is the deadliest breast cancer subtype, and therapies targeting HER2+ biomarkers can improve the prognosis drastically. In this study, array CGH data were used to train cancer subtype classifiers based on ANOVA feature selection + logistic regression and SPLSDA feature selection + XGBoost accompanied by feature importance analysis to identify HER2+ cancer biomarkers. The XGBoost model identified HER2+ with 100\% accuracy in nested cross validations. Subsequent feature importance analyses identified a single chromosome range and genes related to HER2+ cancer. Interpretations of the significant feature, limitations of the study, and potential improvements are discussed at the end of the paper.