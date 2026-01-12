---
title: A Tutorial on Rendering Markup Languages to Accessible Formats
author: Chris Wyatt
date: 2025-08-20
---

### The goals for this quick tutorial:

* Case 1: Demonstrate making LaTeX pdfs more accessible
* Case 2: Demonstrate how to leverage existing LaTeX source documents and experience using Pandoc to create accessible html
* Case 3: Introduce Markdown for simple accessible authoring targeting html, docx/pptx, and epub
* Case 4: Introduce ConTeXt for producing accessible PDFs
* Case 5: Introduce Quarto for more complex accessible authoring

It assumes you are already using a Markup language to author your documents (or want to learn how).

See this [GitHub repository](https://github.com/clwyatt/accessibility-templates) for templates, more details, and the source for this presentation.

### Initial Remarks

While you can make PDFs accessible, screen readers (currently) handle html much better.

:::::: columns
::: column
**PDF Pros:**

- layout is preserved exactly
- single file that is easy to distribute
- it is possible to tag PDFs containing images and math

**PDF Cons:**

- many tools for creating PDFs still generate untagged or poorly tagged files

:::

:::: column

**HTML Pros:**

- it is relatively simple to create files that meet level AA compliance

**HTML Cons:**

- layout is not preserved
- typically has multiple external resources, complicating distribution

::::
::::::

### Case 1: Make LaTeX more accessible

* You need a bleeding-edge Tex distribution, e.g. TexLive-2025
* You add some meta-data before the documentclass declaration
* You add alt-tags to ``\includegraphics``
```{.latex}
\DocumentMetadata{
  lang        = en,
  pdfstandard = ua-2,
  pdfstandard = a-4f, %or a-4
  tagging=on,
  tagging-setup={math/setup=mathml-SE}
\documentclass{article}
\usepackage{unicode-math}
\begin{document}
\includegraphics[alt={Description Here}]{myimage.png}
\end{document}
```

In my testing this **does** tag section headers and figures/images, but **does not** tag equations such that Ally will accept them.

### Case 2: Basic LaTeX to Accessible HTML + MathML

Given ``mydoc.tex``:

```{.latex}
\documentclass{article}
\title{My Title}
\author{Some One}
\date{2025-09-01}
\begin{document}
\maketitle

\section{Introduction}

A \textbf{famous} \textit{equation} is $V = IR$.

\end{document}
```


### Case 2: Basic LaTeX to Accessible HTML + MathML

We can use [pandoc](https://pandoc.org) to convert this to a single accessible html file.

```{.sh}
> pandoc -s -t html -V lang=en --embed-resources --mathml \
         mydoc.tex -o mydoc.html
```

* ``-s`` (optional) create a standalone html file (header etc)
* ``-t html`` produce html
* ``-V lang=en`` add the language to the html header (for screen readers)
* ``--embed-resources`` (optional) embeds any resource files (e.g. images) into the file itself. This makes it easier to distribute and upload to Canvas but the increases file size and pasting into the Canvas Rich Content Editor breaks.
* ``--mathml`` means to use mathml for math. This results in equations a screen reader can **automatically** navigate.

### Case 2: Basic LaTeX to Accessible HTML + MathML

The [result](output/mydoc.html) gets 100% in Ally and Firefox Accessibility Issue tool.

It does have some minor issues found by the Axe DevTools Chrome Extension that can be solved by modifying the pandoc html template or adding a header and footer.

### Case 2: Adding Images with Alt Text

Suppose we add to ``mydoc.tex``:

```{.latex}
\includegraphics[alt={As long a description as you like}]
                {myfig.png}
```

The [html output](output/mydoc-v2.html) now includes the image with accessible alt text.

### Case 2: Adding Captions

Suppose we modify ``mydoc.tex``:

```{.latex}
\begin{figure}
  \centering
  \includegraphics[alt={illustration of concept X, 
                        see figure caption for details
						}]{myfig.png}
  \caption{My longer caption text with details.}
\end{figure}
```

The [html output](output/mydoc-v3.html) includes the image with accessible alt text with a visible caption. This is the recommended practice for complex images.

### Case 2: More complex math

Pandoc conversion supports the amsmath and amssymb LaTeX packages.

Example preamble:

```{.latex}
\usepackage{amsmath,amssymb}
```

Example usage:
```{.latex}
\begin{align*}
  a_k &= \frac{1}{T_0} \int\limits_{T_0} x_p(t) e^{-jk\omega_0 t}\; dt\\
  &= \frac{1}{T_0} \int\limits_{-\infty}^{\infty} x(t) e^{-jk\omega_0 t}\; dt \mbox{ since } x(t) = 0 \mbox{ outside the interval } (A,B)\\
\end{align*}
```

Again, the [result](output/mydoc-v4.html) gets 100% in Ally and Firefox Accessibility Issue tool.

### Case 2: Tikz figures

If you use ``tikz`` or ``circuitikz`` for figures, render them to svg and include them.

[Here is an example](https://github.com/clwyatt/ece3704-notes) showing how to combine all these options.

### Case 2: Getting it into Canvas Pages

If you want to get this content into canvas you can:

1. Create the page in the Canvas Rich Text Editor, and hit the ``</>`` icon to put it into raw html mode.
2. Remove the standalone and embed switches in pandoc.
3. Copy/paste the output file into the Canvas editor.
4. Upload any images and reinsert them with alt-text.

Note: you can skip the file and just pipe the output into your clipboard for easy pasting. e.g. in macOS

```{.sh}
> pandoc -t html -V lang=en --mathml mydoc.tex | pbcopy
```

### Case 2: EPUB output

* One of the problems with html is creating portable, standalone documents due to external resource files like images.
* The `--embed-resources` option to pandoc mitigates this, but generates large files in many cases.
* Another option is to use zip files, one per document, or a mhtml/maff/webarchive/warc/... file.
* A better option is to use the epub3 format, which is a zip file of html, images, and metadata.

```{.sh}
pandoc -s -t epub --mathml input.tex -o output.epub
```

There are many epub3 readers available including Apple Books, Calibre and Adobe Digital Editions. I am still confirming if this meets accessibility requirements.

### Case 2: LateX Beamer

If you use beamer for your slides. You can convert to one of the html slide frameworks, e.g. reveal.js using pandoc.

See [this example](https://github.com/clwyatt/accessibility-templates/tree/main/beamer-to-html).

### Case 3: Using Alternative Markup Languages

If you do not currently use LaTeX, consider Markdown ( or Asciidoc, or reStructuredText).

* simple markup, but supports sections, math, and figures
* pandoc can generate accessible html, epub, or docx/pptx (with the proper structure)
* pandoc can also generate accessible PDF (with some effort via ConTeXt)

[Here is an example](https://github.com/clwyatt/accessibility-templates/tree/main/markdown-to-html-pdf-docx)

### Case 4: Using ConTeXt

* The html+mathml format should be preferred, but sometimes we need to preserve layout and prevent tampering (e.g. for assignments).
* LaTeX does not currently support tagged PDF well (at least that I can get to work)
* A very similar macro system for TeX, called ConTeXt, does support tagging.
* Can be used in conjunction with Markdown if you do not want to learn ConTeXt. 
* You can also use pandoc to convert LaTeX to ConTeXt (about 90% effective)
* It can be a little [tedious to install](https://wiki.contextgarden.net/Introduction/Installation) but seems robust.
* The previous example has an accessible template. The mp3 alternative download does a good job reading these files.

### Case 5: Using Quarto

A final example, if you need to generate more complex documents with multiple pages, cross-references, etc. consider using the Quarto publishing system.

* Uses a markdown syntax
* supports multiple document types including html and epub
* integrates computation (python scripts, etc) that produce output embedded in the document

I am using this to [convert the ECE 2714 Notes](https://github.com/clwyatt/notes-2714).

### Some Takeaways

* Consider moving away from PDF, html+mathml is considered more accessible.
* Tag every image and caption figures.
* Start small, converting one document at a time, focus on major issues.
* Pandoc is your new best friend!

**Resources:**

* LaTeX Tagging: <https://www.latex-project.org/news/2024/07/08/tagging/>
* Pandoc: <https://pandoc.org>
* Quarto: <https://quarto.org>
* Context: <https://wiki.contextgarden.net>
* Accessibility Templates: <https://github.com/clwyatt/accessibility-templates>



