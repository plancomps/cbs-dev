---
title: Macros
# has_children: true
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

----

Markup using `cbs-latex` is quite low-level.
This makes it easy to adjust the layout to fit the intended page width, but tedious to write.
Generation of marked-up CBS from CBS source text is currently being implemented in Spoofax.

The macros provided by `cbs-latex` are defined separately for producing PDFs and web pages:

- [`cbs-latex.sty`]
- [MathJax configuration]

The `cbs-latex` package provides macros that mostly have different definitions for PDFs and web pages.
It also provides a few macros for complicated or uncommon $$\LATEX$$ commands.
All macro names are in uppercase, to reduce the risk of clashes with macros defined by other packages.
They are for use only in math mode.

## Required packages

When used with $$\LATEX$$, the `cbs-latex` package requires the following packages (all included in TeXLive):

`amsmath`
: Provides various environments and commands for math alignment, including `align*` and `aligned`.

`amssymb`
: Provides an extended math symbol collection, including $$\leadsto$$.

`stmaryrd`
: Provides symbols for TCS, including `\llbracket` and `\rrbracket` ($$\LEFTPHRASE$$ and $$\RIGHTPHRASE$$).

`textcomp`[^implicit]
: Provides commands for various characters in text mode, including `\textsinglequote` ($$\APOSTROPHE$$).

`xcolor`
: The `dvipsnames` option provides the same names for colors as MathJax.

`hyperref`
: Needed for creating hyperlinks. The `hidelinks` option avoids the appearance of coloured boxes around references to names in CBS specifications.

The following packages are not required, but using them may make the formatting of running text in $$\LATEX$$ closer to that produced from Markdown on web pages:

`parskip`
: Uses blank lines to separate paragraphs.

`markdown`
: Provides the `markdown` environment, which allows the use of Markdown markup in $$\LATEX$$ text mode.
  For text that also contains $$\LATEX$$ math mode markup, add the package option `[hybrid]`.
  
  Warning: Use of `*`-environments inside the `markdown` environment may cause `pdflatex` to fail.

## Colors

The following four color macros are used internally by other macros.
The tones of these colors differ between PDFs and web pages,
and between light and dark color schemes on web pages.
The default color of text and math symbols is black for PDFs, and either a dark gray or white for web pages.
(Ideally, the colors should be distinguishable also to readers with color-impaired vision; this has not yet been checked.)

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Gray` | `{\GRAYCOLOR Gray}` | $${\GRAYCOLOR \textsf{Gray}}$$ |
| `Red` | `{REDYCOLOR Red}` | $${\REDCOLOR \textsf{Red}}$$ |
| `Green` | `{\GREENCOLOR Green}` | $${\GREENCOLOR \textsf{Green}}$$ |
| `Blue` | `{\BLUECOLOR Blue}` | $${\BLUECOLOR \textsf{Blue}}$$ |

Apart from the standard $$\LATEX$$ color names, the names defined by the `dvipsnames` option of the `xcolor` package (along with the `RGB`, `rgb`, and `grey-scale` color spaces) can be used for both PDFs and web pages.

## Names

CBS specifications involve declaration and reference of names for funcons, entities, syntax sorts, and semantic functions.
The macro used for a name depends on the namespace.
Names in different namespaces have different highlighting colors.

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `funcon-name` | `\NAME{funcon-name}` | $$\NAME{funcon-name}$$ |
| `entity-name` | `\NAME{entity-name}` | $$\NAME{entity-name}$$ |
| `syntax-name` | `\SYN{syntax-name}` | $$\SYN{syntax-name}$$ |
| `semantics-name` | `\SEM{semantics-name}` | $$\SEM{semantics-name}$$ |
| `§2.1` | `\S\SECT{2.1}` | $$\S\SECT{2.1}$$ |

### Hyperlinks

The optional argument of a name markup macro indicates that the occurrence of the name is a declaration or a reference.
In both PDFs and web pages, each name reference becomes a hyperlink to a declaration of that name.
A name should not be declared (in the same namespace) more than once per file.

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `name` | `\NAME[\DECL]{name}` | $$\NAME{name}$$ |
| `name` | `\NAME[\REF]{name}` | $$\NAME{name}$$ |
| `name` | `\NAME[\HYPER{url}{file}]{name}` | $$\NAME{name}$$ |

Similarly for `\SYN`, `\SEM`, `\SECT`.

### Variables

The macro for variables formats its argument in text mode.
A Greek letter used as a variable has to be in math mode.
Any primes, subscripts, and multiplicity come after the macro argument.

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `X'` | `\VAR{X}'` | $$\VAR{X}'$$ |
| `X12''` | `\VAR{X}\SUB{12}''` | $$\VAR{X}\SUB{12}''$$ |
| `X+` | `\VAR{X}\PLUS` | $$\VAR{X}\PLUS$$ |
| `X?` | `\VAR{X}\QUERY` | $$\VAR{X}\QUERY$$ |
| `X*` | `\VAR{X}\STAR` | $$\VAR{X}\STAR$$ |
| `Rho` | `\rho` or `\VAR{$\rho$}` | $$\VAR{$\rho$}$$ |

## Language specifications

### Grammars

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Lexis ...` | `\KEY{Lexis} ~ ...` | $$\KEY{Lexis} ~ \ldots$$ |
| `Syntax ...` | `\KEY{Syntax} ~ ...` | $$\KEY{Syntax} ~ \ldots$$ |
| `...:... ::= ...` | `...:... ::= ...` | $$\ldots:\ldots ::= \ldots$$ |

### Syntactic phrase types

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `syntax-name` | `\SYN{syntax-name}` | $$\SYN{syntax-name}$$ |
| `'lexeme'` | `\LEX{lexeme}` | $$\LEX{lexeme}$$ |
| `P_1 P_2` | `P_1 ~ P_2` | $$P_1 ~ P_2$$ |
| `P_1 | P_2` | `P_1 \mid P_2` | $$P_1 \mid P_2$$ |
| `P+` | `P\PLUS` | $$P\PLUS$$ |
| `P?` | `P\QUERY` | $$P\QUERY$$ |
| `P*` | `P\STAR` | $$P\STAR$$ |
| `(P)` | `\LEFTGROUP P \RIGHTGROUP` | $$\LEFTGROUP P \RIGHTGROUP$$ |

### Lexemes

Characters in lexemes are marked up as follows.
Those that require macros include all the special characters of $$\LATEX$$,
and characters that look different in text and math mode.

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `'0...9A...Za...z'` | `\LEX{0...9A...Za...z}` | $$\LEX{0...9A...Za...z}$$ |
| `'!()*,./:;=?@[]'` | `\LEX{!()*,./:;=?@[]}` | $$\LEX{!()*,./:;=?@[]}$$ |
| `'#'` | `\LEX{\HASH}` | $$\LEX{\HASH}$$ |
| `'#'` | `\LEX{\DOLLAR}` | $$\LEX{\DOLLAR}$$ |
| `'#'` | `\LEX{\PERCENT}` | $$\LEX{\PERCENT}$$ |
| `'#'` | `\LEX{\AMPERSAND}` | $$\LEX{\AMPERSAND}$$ |
| `'#'` | `\LEX{\APOSTROPHE}` | $$\LEX{\APOSTROPHE}$$ |
| `'+'` | `\LEX{\PLUSCHAR}` | $$\LEX{\PLUSCHAR}$$ |
| `'-'` | `\LEX{\HYPHEN}` | $$\LEX{\HYPHEN}$$ |
| `'<'` | `\LEX{\LESS}` | $$\LEX{\LESS}$$ |
| `'>'` | `\LEX{\GREATER}` | $$\LEX{\GREATER}$$ |
| `'\\'` | `\LEX{\BACKSLASH}` | $$\LEX{\BACKSLASH}$$ |
| `'^'` | `\LEX{\CARET}` | $$\LEX{\CARET}$$ |
| `'_'` | `\LEX{\UNDERSCORE}` | $$\LEX{\UNDERSCORE}$$ |
| ``'`'`` | `\LEX{\GRAVE}` | $$\LEX{\GRAVE}$$ |
| `'{'` | `\LEX{\LEFTBRACE}` | $$\LEX{\LEFTBRACE}$$ |
| `'|'` | `\LEX{\BAR}` | $$\LEX{\BAR}$$ |
| `'}'` | `\LEX{\RIGHTBRACE}` | $$\LEX{\RIGHTBRACE}$$ |
| `'~'` | `\LEX{\TILDE}` | $$\LEX{\TILDE}$$ |

### Semantic functions

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
|  `Semantics s-n[[_:...]] : ...` | `\KEY{Semantics} ~ \SEM[\DECL]{s-n} \LEFTPHRASE\_:...\RIGHTPHRASE : ...` | $$\KEY{Semantics} ~ \SEM{s-n} \LEFTPHRASE \_ : \ldots \RIGHTPHRASE : \ldots$$ |
| `Rule ... = ...` | `\KEY{Rule} ~ ... = ...` | $$\KEY{Rule} ~ \ldots = \ldots$$ |
| `[[...]]` | `\LEFTPHRASE ... \RIGHTPHRASE` | $$\LEFTPHRASE \ldots \RIGHTPHRASE$$ |
| `s-n[[...]]` | `\SEM[\REF]{s-n}\LEFTPHRASE ... \RIGHTPHRASE` | $$\SEM{s-n}\LEFTPHRASE \ldots \RIGHTPHRASE$$ |

## Funcon specifications

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Funcon f-n ... : ...` | `\KEY{Funcon} ~ \NAME[\DECL]{f-n} ... : ...` | $$\KEY{Funcon} ~ \NAME{f-n} \ldots : \ldots$$ |
| `Alias f-n1 = f-n2` | `\KEY{Alias} ~ \NAME[\DECL]{f-n1} = \NAME[\REF]{f-n2}` | $$\KEY{Alias} ~ \NAME{f-n1} = \NAME{f-n2}$$ |
| `Type f-n ...` | `\KEY{Type} ~ \NAME[\DECL]{f-n} ...` | $$\KEY{Type} ~ \NAME{f-n} \ldots$$ |

### Datatype specifications

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Datatype f-n ::= ...` | `\KEY{Datatype} ~ \NAME[\DECL]{f-n} ::= ...` | $$\KEY{Datatype} ~ \NAME{f-n} ::= \ldots$$ |
| `... | ...` | `... \mid ...` | $$\ldots \mid \ldots$$ |
| `f-n` | `\NAME[\DECL]{f-n}` | $$\NAME{f-n}$$ |
| `f-n(...)` | `\NAME[\DECL]{f-n}(...)` | $$\NAME{f-n}(\ldots)$$ |
| `{ _ : ... }` | `\{ ~ _ : ... ~ \}` | $$\{ ~ \_ : \ldots ~ \}$$ |

### Entity declarations

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Entity ...` | `\KEY{Entity} ~ ...` | $$\KEY{Entity} ~ \ldots$$ |
| `e-n(_:...)|- _ ---> _` | `\NAME[\DECL]{e-n}(\_:...) \vdash \_\TRANS\_` | $$\NAME{e-n}(\_ : \ldots) \vdash \_ \TRANS \_$$ |
| `<_,e-n(_:...)> ---> <_,e-n(_:...)>` | `\langle\_,\NAME[\DECL]{e-n}(\_:...)\rangle \TRANS \langle\_,\NAME{e-n}(\_:...)\rangle` | $$\langle\_,\NAME{e-n}(\_:\ldots)\rangle \TRANS \langle\_,\NAME{e-n}(\_:\ldots)\rangle$$ |
| `_ -- e-n.(_:...) -> _` | `\_\TRANS[{\NAME[\DECL]{e-n}.(\_:...)}]\_` | $$\_\TRANS[{\NAME{e-n}.(\_:\ldots)}]\_$$ |

The `.` in the last line above can be `!`, `?`, or omitted.

### Rules

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Rule ...` | `\KEY{Rule} ~ ...` | $$\KEY{Rule} ~ \ldots$$ |
| `Rule ... ⏎ ...` | `\KEY{Rule} ~ \AXIOM{& ... \\ & ...}` | $$\KEY{Rule} ~ \AXIOM{& \ldots \\ & \ldots}$$ |
| `Rule ... ⏎ ---- ⏎ ...` | `\KEY{Rule} ~ \RULE{...}{...}` | $$\begin{align*} \KEY{Rule} ~ \RULE{\ldots}{\ldots} \end{align*}$$ |
| `Otherwise ...` | `\KEY{Otherwise} ~ ...` | $$\KEY{Otherwise} ~ \ldots$$ |
| `Assert ...` | `\KEY{Assert} ~ ...` | $$\KEY{Assert} ~ \ldots$$ |

### Formulae

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `... ~> ...` | `... \leadsto ...` | $$\ldots \leadsto \ldots$$ |
| `... == ...` | `... == ...` | $$\ldots == \ldots$$ |
| `... =/= ...` | `... \neq ...` | $$\ldots \neq \ldots$$ |
| `... <: ...` | `... <: ...` | $$\ldots <: \ldots$$ |
| `... ---> ...` | `... \TRANS ...` | $$\ldots \TRANS \ldots$$ |
| `e-n(...)|- ...--->...` | `\NAME[\REF]{e-n}(...) \vdash ...\TRANS...` | $$\NAME{e-n}(\ldots) \vdash \ldots \TRANS \ldots$$ |
| `<...,e-n(...)> ---> <...,e-n(...)>` | `\langle...,\NAME[\REF]{e-n}(...)\rangle \TRANS \langle...,\NAME{e-n}(...)\rangle` | $$\langle\ldots,\NAME{e-n}(\ldots)\rangle \TRANS \langle\ldots,\NAME{e-n}(\ldots)\rangle$$ |
| `... -- e-n.(...) -> ...` | `...\TRANS[{\NAME[\DECL]{e-n}.(...)}]...` | $$\ldots\TRANS[{\NAME{e-n}.(\ldots)}]\ldots$$ |

The `.` in the last line above can be `!`, `?`, or omitted.

### Terms

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `( )` | `( ~ )` | $$( ~ )$$ |
| `'...'` | `\ATOM{...}` | $$\ATOM{...}$$ |
| `42` | `42` | $$42$$ |
| `2.14` | `2.14` | $$2.14$$ |
| `"..."` | `\STRING{...}` | $$\STRING{...}$$ |
| `... : ...` | `... : ...` | $$\ldots : \ldots$$ |
| `... => ...` | `... \TO ...` | $$\ldots \TO \ldots$$ |
| `...+` | `...\PLUS` | $$\ldots\PLUS$$ |
| `...?` | `...\QUERY` | $$\ldots\QUERY$$ |
| `...*` | `...\STAR` | $$\ldots\STAR$$ |
| `... | ...` | `... \mid ...` | $$\ldots \mid \ldots$$ |
| `... & ...` | `... \& ...` | $$\ldots \& \ldots$$ |
| `...^N` | `...^{N}` | $$\ldots^{N}$$ |
| `(..., ...)` | `(..., ...)` | $$(\ldots, \ldots)$$ |
| `[..., ...]` | `[..., ...]` | $$[\ldots, \ldots]$$ |
| `{..., ...}` | `\{..., ...\}` | $$\{\ldots, \ldots\}$$ |
| `{...|->..., ...}` | `\{... \mapsto ..., \cdots\}` | $$\{\ldots \mapsto \ldots, \cdots\}$$ |

### Other specifications

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `Auxiliary K ...` | `\KEY{Auxiliary K} ~ ...` | $$\KEY{Auxiliary K} ~ \ldots$$ |
| `Built-in K ...` | `\KEY{Built-in K} ~ ...` | $$\KEY{Built-in K} ~ \ldots$$ |
| `Meta-variables ...` | `\KEY{Meta-variables} ~ ...` | $$\KEY{Meta-variables} ~ \ldots$$ |

## Alignment

| Plain CBS | $$\LATEX$$ | Formatted CBS |
| - | - | - | 
| `. .` | `.~.` | $$.~.$$ |
| `. . .` | `.\quad.` | $$.\quad.$$ |
| `. . . . .` | `.\qquad.` | $$.\qquad.$$ |
| `... ... ⏎    ...` | `\begin{align*} ... ~ & ... \\ ~ & ... \end{align*}` | $$\begin{align*} \ldots ~ & \ldots \\ ~ & \ldots \end{align*}$$ |
| `... ... ⏎    ...` | `... ~ \begin{aligned}[t] & ... \\ & ... \end{aligned}` | $$\ldots ~ \begin{aligned}[t] & \ldots \\ & \ldots \end{aligned}$$ |

----

[^implicit]:
    The `textcomp` package is automatically loaded in recent $$\LATEX$$ distributions.

[`cbs-latex.sty`]: latex/cbs-latex.txt
[MathJax configuration]: mathjax/config.txt
