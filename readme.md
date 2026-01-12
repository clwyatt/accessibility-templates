# Accessibility Templates

This is a repository of templates/demonstrations of generating accessible documents from markup languages like LaTeX and Markdown. The main tools used are the excellent [pandoc](https://pandoc.org) and GNU Make. Both are easy to install on most platforms. Tagged PDF generation is accomplished using ConTeXt and partially working LaTeX. A few other open source tools are used.

## Templates

* `beamer-to-html`: Basic LaTeX Beamer to html using reveal.js
* `context-to-pdf`: Basic tagged PDF generation from ConTeXt
* `latex-tagged-pdf`: An attempt to create tagged pdf directly from LaTeX
* `latex+png-to-epub`: Basic LaTeX and png figures to epub3 
* `latex+png-to-html`: Basic LaTeX and png figures to standalone (single file) html
* `latex+tikz-to-html`: Basic LaTeX and Tikz figures to standalone (single file) html
* `markdown-to-html-pdf-docx`: Markdown to three accessible outputs: single-file html, tagged pdf via ConTeXt, and docx.
* `context-exam-environment`: a ConTeXt environment similar to the LaTeX exam class. See the readme in that directory for more information.
## Documentation

* Each template contains a Makefile that documents the tools used and their invocations. 
* There is a tutorial that briefly covers what I have learned (or misunderstood as the case may be)

