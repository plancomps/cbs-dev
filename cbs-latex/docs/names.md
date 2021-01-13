---
title: Names
# parent: Macros
nav_exclude: true
mathjax: true
---

# Names

The arguments of the macros for names are in text mode, to support formatting of hyphenated words.

Names may be variables, funcons, syntax sorts, or semantic functions.

## Variables

`\VAR{Variable}`

: Single uppercase letters or multi-character words, possibly with hyphens, used as variables in (syntax or funcon) terms, not including primes, subscripts, or superscripts:
  
  $$\VAR{VarsDecl}$$, $$\VAR{X}$$, ...
  
  Note: Also single-character variables such as `X` need markup with `\VAR`, to ensure uniformity of fonts.
  A variable consisting of a single Greek letter has to be enclosed in `$...$` to ensure math mode, e.g.: `\VAR{$\rho$}`.

`\SUB{digits}`

: Using `\VAR{Variable}\SUB{digits}` (optionally followed by one or more apostrophes `'`) ensures that the same font is used for the `Variable` and the `digits`.

  `\VAR{X}\SUB{1}, \VAR{X}\SUB{23}''` (written `X1, X23''` in plain CBS) produces $$\VAR{X}\SUB{1}, \VAR{X}\SUB{23}''$$

`\PLUS`

: `\VAR{X}\PLUS` (written `X+` in plain CBS) produces $$\VAR{X}\PLUS$$

`\QUERY`

: `\VAR{X}\QUERY` (written `X?` in plain CBS) produces $$\VAR{X}\QUERY$$

`\STAR`

: `\VAR{X}\STAR` (written `X*` in plain CBS) produces $$\VAR{X}\STAR$$

## Other kinds of names

`\NAME{funcon-name}`

: Funcon name:
  
  $$\NAME{sequential}$$, $$\NAME{map-interleave}$$, ...

`\SYN{syntax-name}`

: Name of a syntax sort (non-terminal):
  
  $$\SYN{exp}$$, $$\SYN{imp-stmt}$$, ...

`\SEM{semantic-name}`

: Name of a semantic function (translation):
  
  $$\SEM{exp}$$, $$\SEM{imp-stmt}$$, ...

`\SECT{sect-num}`

: Number of a section (in a language specification):

  $$\SECT{2}$$, $$\SECT{2.1.4}$$, $$\SECT{A.1}$$, ...

## Hyperlinks

Name markup can take an optional argument to indicate that it is a declaration or a reference.
In both PDFs and web pages, each name reference becomes a hyperlink to a declaration of that name.
Each name can be declared only once in each file.

`\NAME[\DECL]{name}`

: a declaration.

  `\VAR[\DECL]{name}` is only for use on declarations of meta-variables in grammars.[^var]

`\NAME[\REF]{name}`

: a reference to the unique declaration in the current file.

`\NAME[\HYPER{URL}{FILE}]{name}`

: <br>

  a reference to the unique declaration in the PDF at `URL/FILE/FILE.pdf` or in the web page at `URL/FILE/`.

The usage of the optional argument is the same for all kinds of names.
The default for the optional argument in `\NAME{name}` is the macro `\PLAIN`.

Redefinition of `\HYPER{URL}{FILE}` to `\REF` makes all links produced by name markup local to the current PDF or web page.

----
[^var]:
    CBS-LaTeX does not support links within rules.
    Name analysis for CBS-beta in Spoofax links variable references in terms to their introductions in patterns,
    but that is to support checks for source-dependency, rather than navigation.
