---
title: Samples
mathjax: true
# has_children: true
---

# Samples

Two CBS specifications from the [CBS-beta] repository illustrate the use of the `cbs-latex` package to produce PDFs and web pages:

| Plain CBS | $$\LATEX$$ |     PDF    |   MathJax  |     Web    |
| :-------: | :--------: | :--------: | :--------: | :--------: |
| [Binding]  | [.tex](latex/Binding/Binding.txt) | [.pdf](latex/Binding/Binding.pdf) | [.md](mathjax/Binding.txt) | [.html](mathjax/Binding.html) |
| [SIMPLE-3-Statements]  | [.tex](latex/SIMPLE-3-Statements/SIMPLE-3-Statements.txt) | [.pdf](latex/SIMPLE-3-Statements/SIMPLE-3-Statements.pdf) | [.md](mathjax/SIMPLE-3-Statements.txt) | [.html](mathjax/SIMPLE-3-Statements.html) |

`pdflatex` produced the PDFs from source documents that include the [`cbs-latex`] package and the marked-up CBS specifications in $$\LATEX$$.

MathJax produced the web pages from source documents that include the marked-up CBS specifications in the kramdown variant of Markdown,
which supports embedding of $$\LATEX$$ code in math blocks `$$...$$`.
Jekyll uses kramdown to convert Markdown to HTML, 
then MathJax converts the $$\LATEX$$ embedded in it to HTML.
The [MathJax configuration] is included in the `<head>` element of the HTML pages.

Names in the formatted CBS specifications are linked to the relative URLs of their declarations,[^scroll]
but the targets of non-local links are not included here.

----

[^scroll]:
    Local links scroll correctly in Firefox, but not in Safari;
    a future release of MathJax should be able to work around the Safari issue.

[CBS-beta]:  https://plancomps.github.io/CBS-beta/

[Binding]:  https://plancomps.github.io/CBS-beta/Funcons-beta/Computations/Normal/Binding/
[Binding.tex]:  latex/Binding/Binding.txt
[Binding.pdf]:  latex/Binding/Binding.pdf
[Binding.md]:   mathjax/Binding.txt
[Binding.html]: mathjax/Binding.html

[SIMPLE-3-Statements]:  https://plancomps.github.io/CBS-beta/Languages-beta/SIMPLE/SIMPLE-cbs/SIMPLE/SIMPLE-3-Statements/
[SIMPLE-3-Statements.tex]:  latex/SIMPLE-3-Statements/SIMPLE-3-Statements.txt
[SIMPLE-3-Statements.pdf]:  latex/SIMPLE-3-Statements/SIMPLE-3-Statements.pdf
[SIMPLE-3-Statements.md]:   mathjax/SIMPLE-3-Statements.txt
[SIMPLE-3-Statements.html]: mathjax/SIMPLE-3-Statements.html

[`cbs-latex`]: latex/cbs-latex.txt
[MathJax configuration]: mathjax/config.txt
