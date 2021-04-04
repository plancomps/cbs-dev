---
title: Samples
math: katex
---

# Samples

The following samples illustrate how plain CBS specifications can be marked up
using the CBS-LaTeX macros, and the resulting PDFs and web pages.

## Funcon specifications

[CBS-beta/Funcons-beta/Computations/Normal/Binding](https://plancomps.github.io/CBS-beta/Funcons-beta/Computations/Normal/Binding):

> [Plain CBS](cbs/Binding.cbs.txt) \|
  [CBS-LaTeX](latex/Binding/Binding.part.tex.html) \|
  [PDF](latex/Binding/Binding.pdf) \|
  [Markdown](kramdown/Binding.md.html) \|
  [Web](katex/Binding)

## Language specifications

[CBS-beta/Languages-beta/SIMPLE/SIMPLE-cbs/SIMPLE/SIMPLE-3-Statements](https://plancomps.github.io/CBS-beta/Languages-beta/SIMPLE/SIMPLE-cbs/SIMPLE/SIMPLE-3-Statements):

> [Plain CBS](cbs/SIMPLE-3-Statements.cbs.txt) \|
  [CBS-LaTeX](latex/SIMPLE-3-Statements/SIMPLE-3-Statements.part.tex.html) \|
  [PDF](latex/SIMPLE-3-Statements/SIMPLE-3-Statements.pdf) \|
  [Markdown](kramdown/SIMPLE-3-Statements.md.html) \|
  [Web](katex/SIMPLE-3-Statements)

## ASCII tests

The ASCII tests show how various characters used in language grammars are marked up
using the CBS-LaTeX macros, and used to produce a PDF and a web page:

> [Plain CBS](cbs/TEST-Start.cbs.txt)  \|
  [CBS-LaTeX](latex/TEST-Start/TEST-Start.part.tex.html) \|
  [PDF](latex/TEST-Start/TEST-Start.pdf) \|
  [Markdown](kramdown/TEST-Start.md.html) \|
  [Web](katex/TEST-Start) 

# Browsing

PDFs
: Acrobat Reader is recommended. The Preview app on macOS does not support hyperlinks from references to declarations, which are used for navigation in multi-file CBS specifications.

Web pages
: In the browser, the LaTeX markup is rendered significantly faster by KaTeX than by MathJax. The appearance of the web pages (at least when using recent versions of Firefox and Safari) is close to that of the PDFs produced from the same CBS files using pdflatex.

# Production

A literate CBS source file is a Markdown text that includes plain CBS notation in code blocks.
Using the kramdown variant of Markdown, the CBS code blocks can be replaced by math blocks with LaTeX markup.
The kramdown package can then transform the file completely to LaTeX (to produce a PDF),
and to HTML (relying on math engines such as KaTeX or MathJax to render the embedded LaTeX in web browsers).

The current implementation of the required transformations uses `Spoofax`, `kramdown`, and `pdflatex`.
Production of a PDF and a web page from a literate CBS source file involves the following steps.

1. A CBS editor in `Spoofax` (generated from the SDF3 and NaBL2 definitions of CBS) parses all the literate CBS source files in a project,[^island] analysing and checking the names used in the plain CBS code blocks.
   
2. A menu action in the CBS editor (implemented in `Stratego`) produces kramdown files with CBS-LaTeX markup in math blocks.

3. The `kramdown` converter generates LaTeX source files from the kramdown files.

4. `pdflatex` produces PDFs by inputting the generated LaTeX source files in a document template with the `cbs-latex` package.
   The LaTeX definitions of the highlighting colours can be overridden using `\colorlet{...}{...}` (the `svgnames` colours are pre-loaded).

5. The `kramdown` converter automatically generates HTML pages from the kramdown files when building a website on GitHub Pages (or locally) with Jekyll.

6. The `KaTeX` package uses JavaScript and CSS in the browser to automatically render LaTeX code in HTML pages,
   with an option that provides the CBS-LaTeX macros.
   The CSS specifications of the highlighting colours can be overridden (the standard HTML colour names can be used).

For the CBS-beta website, the above tool chain is currently automated by running the following commands in the `CBS-beta` root directory.

For each CBS project of funcon or language specifications, Spoofax Sunshine builds the project and transforms all its CBS files to kramdown (steps 1 and 2):
```
java -Xss16M -jar sunshine2.jar build --language ../cbs-beta-tools/CBS --transform-goal "One Math" --project ...
```

Generation of all kramdown files with embedded HTML:
```
make docs 2>&1 | tee make-docs.log
```

Generation of all kramdown files with embedded LaTeX:
```
make math 2>&1 | tee make-math.log
```

Generation of stale or missing LaTeX files by `kramdown`:
```
make kramdown
```
which executes for each `FILE.md`:
```
kramdown -o latex --latex-headers "section*,subsection*,subsubsection*,paragraph*,subparagraph*,subparagraph*" FILE.md > FILE.part.tex
```

Generation of stale or missing PDF files by `pdflatex`:
```
make pdflatex
```
which executes for each `FILE.part.tex`:
```
pdflatex FILE
pdflatex FILE
```
to produce `FILE.pdf`.

----

[^island]:
    The CBS grammar resembles a so-called island grammar, where the islands are the formal notation, and the water is informal text.
    Currently, the shores of the islands are marked by comment delimiters `/*...*/` instead of the code fences used in Markdown.

{% include links.md %}
