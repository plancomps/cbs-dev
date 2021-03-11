---
title: Samples
math: katex
has_children: true
---

# Samples

Two CBS specifications from the [CBS-beta] repository illustrate the use of the `cbs-latex` package to produce PDFs and web pages:

| Literate CBS | $$\LATEX$$ |     PDF    |  kramdown  |   $$\KaTeX$$    |
| :-------: | :--------: | :--------: | :--------: | :--------: |
| [Binding](cbs/Binding.cbs.txt) | [CBS-LaTeX](latex/Binding/Binding.part.tex.txt) | [PDF](latex/Binding/Binding.pdf) | [Markdown](kramdown/Binding.md.txt) | [HTML](katex/Binding) |
| [SIMPLE-3-Statements](cbs/SIMPLE-3-Statements.cbs.txt) | [CBS-LaTeX](latex/SIMPLE-3-Statements/SIMPLE-3-Statements.part.tex.txt) | [PDF](latex/SIMPLE-3-Statements/SIMPLE-3-Statements.pdf) | [Markdown](kramdown/Binding.md.txt) | [HTML](katex/SIMPLE-3-Statements) |
| [Tests](cbs/Tests.cbs.txt)  | [CBS-LaTeX](latex/Tests/Tests.part.tex.txt) | [PDF](latex/Tests/Tests.pdf) | [Markdown](kramdown/Tests.md.txt) | [HTML](katex/Tests) |

## Browsing

PDFs
: Acrobat Reader is recommended. The Preview app on macOS does not support hyperlinks from references to declarations, which are used for navigation in multi-file CBS specifications.

Web pages
: In the browser, the LaTeX markup is rendered significantly faster by KaTeX than by MathJax. The appearance of the web pages (at least when using recent versions of Firefox and Safari) is close to that of the PDFs produced from the same CBS files using pdflatex.

## Production

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
   The LaTeX definitions of the highlighting colours can be overridden by editing the template (the `dvipsnames` colours are pre-loaded).

5. The `kramdown` converter automatically generates HTML pages from the kramdown files when building a website on GitHub Pages (or locally) with Jekyll.

6. The `KaTeX` package uses JavaScript and CSS in the browser to automatically render LaTeX code in HTML pages,
   with an option that provides the CBS-LaTeX macros.
   The CSS specifications of the highlighting colours can be overridden (the standard HTML colour names can be used).

----

[^island]:
    The CBS grammar resembles a so-called island grammar, where the islands are the formal notation, and the water is informal text.
    Currently, the shores of the islands are marked by comment delimiters `/*...*/` instead of the code fences used in Markdown.

[CBS-beta]: https://plancomps.github.io/CBS-beta/
