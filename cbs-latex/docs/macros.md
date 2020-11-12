---
title: Macros
mathjax: true
---

# Macros
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

The $$\LaTeX$$ markup for CBS is to be generated from plain CBS specifications.
It is quite low level, and would be tedious to write manually.
When included in manuscript sources, however, it should be much easier to tweak than higher-level AST-based markup.

In general, line breaks in plain CBS are to be respected in the $$\LaTeX$$ markup.
Most of the alignment between related lines should be automatic, but CBS may need enhancing to allow hints to be inserted at various places, to avoid the need for manual adjustment in generated markup.

## Macro usage

The macros format their arguments as follows.

### Symbols

`\KEY{Keyword}`

: CBS keyword: 

  `\KEY{Rule}`, `\KEY{Built-in Funcon}`, ...

  SVG Bug: `\KEY{...} ~ \KEY{...}` overlays the keywords

`\VAR{Variable}`

: Multi-character words used as variables in (syntax or funcon) patterns, not including primes, subscripts, or superscripts:
  
  `\VAR{VarsDecl}`, `\VAR{Block}_2`, ...
  
  Note: Single-character variables such as `X` do not need markup with `\VAR`, since that macro uses the standard math font.
  
  Currently, variables are not linked to their places of introduction.
  
  A `variable` either starts with an uppercase Latin letter, or it is single Greek letter ($$\rho$$, $$\Sigma$$, ...).

`\LEX{Lexeme}`

: Language keyword or separator, written `'...'` in plain CBS:
  
  `\LEX{if}`, `\LEX{;}`, `\LEX{\LBRACE}`, `\LEX{\RBRACE}`, ...
  
  `\LBRACE` and `\RBRACE` match the fixed-width font used for lexemes. 
  Elsewhere, use `\{` and `\}`.
  
  Note: The quotes used in plain CBS would make grammars and semantic rules look messy, so they are omitted.

`\STRING{Characters}`

: Literal CBS string, written `"..."` in plain CBS:
  
  `\STRING{Hello world!}`
  
  The macro encloses the argument in double quotes.

`\ATOM{Characters}`

: Literal CBS atom, written `'...'` in plain CBS:
  
  `\ATOM{location-42}`
  
  The macro encloses the argument in single quotes.

### Names

`\NAME{Funcon-name}`

: Funcon name:
  
  `\NAME{sequential}`, `\NAME{map-interleave}`

  `\NAME[\DECL]{Funcon-name}` makes  `Funcon-name` a declaration.
  
  `\NAME[\REF]{Funcon-name}` makes  `Funcon-name` a hyperlink to its declaration on the same page.
  
  `\NAME[\HYPER{URL}]{Funcon-name}` makes  `Funcon-name` a hyperlink to its declaration on the page at the `URL`.

`\SYN{Syntax-name}`

: Name of a syntax sort (non-terminal):
  
  `\SYN{exp}`, `\SYN{imp-stmt}`

  `\SYN[\DECL]{Syntax-name}` makes  `Syntax-name` a declaration.
  
  `\SYN[\REF]{Syntax-name}` makes  `Syntax-name` a hyperlink to its declaration on the same page.
  
  `\SYN[\HYPER{URL}]{Syntax-name}` makes  `Syntax-name` a hyperlink to its declaration on the page at the `URL`.

`\SEM{Semantic-name}`

: Name of a semantic function (translation):
  
  `\SEM{exp}`, `\SEM{imp-stmt}`

  `\SEM[\DECL]{Semantic-name}` makes  `Semantic-name` a declaration.
  
  `\SEM[\REF]{Semantic-name}` makes  `Semantic-name` a hyperlink to its declaration on the same page.
  
  `\SEM[\HYPER{URL}]{Semantic-name}` makes  `Semantic-name` a hyperlink to its declaration on the page at the `URL`.

### Languages

`\GROUP{Phrase-type}`

: Grouping in a regular expression, written `(...)` in plain CBS:
  
  `\GROUP{ \LEX{else} ~ \SYN[\REF]{block} }`

  Elsewhere, use `(` and `)`.

`\MID`

: Alternatives, written `...|...` in plain CBS:
  
  `\SYN{imp-stmt} \MID \SYN{vars-decl}`

`\PLUS`, `\STAR`, `\QUERY`

: Iterations, written `+`, `*`, `?` in plain CBS:
  
  `\SYN{stmts}\QUERY`, ...

`\PHRASE{Syntax-pattern}`

: Sequences of lexemes and variables, written `[[...]]` in plain CBS:
  
  `\PHRASE{ \LEX{if} ~ \LEX{(} ~ \VAR{Exp} ~ \LEX{)} ~ \VAR{Block} }`

### Signatures and rules

`\RULE{Premises}{Conclusion}`

: Inference rule, written `... ---- ...` in plain CBS.

  Separate multiple premises by `\quad`, or align them using `\begin{aligned}...\\...\end{aligned}`.
  
`\AXIOM{Conclusion}`

: Rule with no premises.

`\TO`

: Computation type, written `=> ...` in plain CBS:
  
  `\KEY{Funcon} ~ \NAME{initialise-binding}(X:\TO T) : \TO T`

`\TRANS`

: Transition, written `...--->...` in plain CBS:
  
  `\NAME{environment}(\NAME{map}(~)) \vdash X \TRANS X'`
  
  TBA: Macros for input/output/signal transitions.

### Spacing, line breaks, and alignment

`~`, `\quad`, `\qquad`

: Space between symbols.

`$$\begin{align*} ...&... \\ ...&... \end{align*}$$`

: Break a displayed specification into lines, aligning on `&`.

`\begin{aligned}[t] ...&... \\ ...&... \end{aligned}`

: Break part of a displayed specification into lines, aligning on `&`.

## MathJax macro definitions

The macro definitions used for MathJax are listed below.
Corresponding definitions for use in $$\LaTeX$$ are to be added.

> MathJax 3.1.1 does not yet support `\begingroup...\endgroup`.
> To use the same macro definitions on different pages, it appears that they currently need to be specified (less perspicuously) in the MathJax configuration.

```latex
\newcommand{\KEY}[1]{\text{\color{Gray}\mit{#1}\;\;}}
\newcommand{\VAR}[1]{\mathit{\small#1}\mspace2mu}
\newcommand{\LEX}[1]{\mathtt{#1}}
\newcommand{\LBRACE}{\unicode{x007b}}
\newcommand{\RBRACE}{\unicode{x007d}}
\newcommand{\STRING}[1]{\mathtt{\unicode{x201c}#1\unicode{x201d}}}
\newcommand{\ATOM}[1]{\mathtt{\unicode{x2018}#1\unicode{x2019}}}

\newcommand{\NAME}[2][\PLAIN]{#1{Name_#2}{\text{\color{Mahogany}#2}}}
\newcommand{\SYN}[2][\PLAIN]{#1{SyntaxName_#2}{\text{\color{ForestGreen}#2}}}
\newcommand{\SEM}[2][\PLAIN]{#1{SemanticsName_#2}{\text{\color{Blue}#2}}}

\newcommand{\PLAIN}[1]{}
\newcommand{\DECL}[1]{\cssId{#1}}
\newcommand{\REF}[1]{\href{samples.html\##1}}
\newcommand{\HYPER}[2]{#1{#2}}

\newcommand{\GROUP}[1]{ {\color{Gray}(} #1 {\color{Gray})} }
\newcommand{\MID}{\mathbin{|}}
\newcommand{\PLUS}{^{\text{\bf+}}}
\newcommand{\STAR}{^{\boldsymbol{\ast}}}
\newcommand{\QUERY}{^{\text{\bf?}}}
\newcommand{\PHRASE}[1]{[\![\, #1 \,]\!]}

\newcommand{\RULE}[2]{\frac{#1}{#2}}
\newcommand{\AXIOM}[1]{\begin{aligned}#1\end{aligned}}
\newcommand{\TO}{\mathop{\Rightarrow}}
\newcommand{\TRANS}{\longrightarrow}

\newcommand{\LanguagesSIMPLE}[2]{\href{https://plancomps.github.io/CBS-beta/Languages-beta/SIMPLE/SIMPLE-cbs/SIMPLE/SIMPLE-#1\##2}}
\newcommand{\FunconsFlowing}[1]{\href{https://plancomps.github.io/CBS-beta/Funcons-beta/Computations/Normal/Flowing\##1}}
\newcommand{\FunconsBinding}[1]{\href{samples.html\##1}}
```

## $$\LaTeX$$ macro definitions

The macro definitions used for $$\LaTeX$$ are listed below.

```latex
\documentclass[fleqn]{article}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage[dvipsnames]{xcolor}
\usepackage{parskip}
\usepackage[hidelinks]{hyperref}

\newcommand{\KEY}[1]{\textsf{\textit{\color{Gray}#1}}}
\newcommand{\VAR}[1]{\mathit{\small#1}}
\newcommand{\LEX}[1]{\text{\texttt{#1}}}
\newcommand{\LBRACE}{\char`\{}
\newcommand{\RBRACE}{\char`\}}
\newcommand{\STRING}[1]{\text{``\texttt{#1}''}}
\newcommand{\ATOM}[1]{\text{`\texttt{#1}'}}

\newcommand{\NAME}[2][\PLAIN]{#1{Name_#2}{\textsf{\color{Mahogany}#2}}}
\newcommand{\SYN}[2][\PLAIN]{#1{SyntaxName_#2}{\textsf{\color{ForestGreen}#2}}}
\newcommand{\SEM}[2][\PLAIN]{#1{SemanticsName_#2}{\textsf{\color{Blue}#2}}}

\newcommand{\PLAIN}[1]{}
\newcommand{\DECL}[1]{\hypertarget{#1}}
\newcommand{\REF}[1]{\hyperlink{#1}}
\newcommand{\HYPER}[2]{#1{#2}}

\newcommand{\GROUP}[1]{ {\color{Gray}(} #1 {\color{Gray})} }
\newcommand{\PLUS}{^{\text{\bf+}}}
\newcommand{\STAR}{^{\boldsymbol{\ast}}}
\newcommand{\QUERY}{^{\text{\bf?}}}
\newcommand{\PHRASE}[1]{[\![\, #1 \,]\!]}

\newcommand{\RULE}[2]{\frac{#1}{#2}}
\newcommand{\AXIOM}[1]{\begin{aligned}#1\end{aligned}}
\newcommand{\TO}{\mathop{\Rightarrow}}
\newcommand{\TRANS}{\longrightarrow}

\newcommand{\LanguagesSIMPLE}[2]{\href{https://plancomps.github.io/CBS-beta/Languages-beta/SIMPLE/SIMPLE-cbs/SIMPLE/SIMPLE-#1\##2}}
\newcommand{\FunconsFlowing}[1]{\href{https://plancomps.github.io/CBS-beta/Funcons-beta/Computations/Normal/Flowing\##1}}
\newcommand{\FunconsBinding}[1]{\REF{#1}}
```
