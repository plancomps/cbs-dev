---
title: Languages
# parent: Macros
nav_exclude: true
mathjax: true
---

# Languages

The following markup is only for use when specifying syntax phrases in language specifications.

`\LEFTPHRASE...\RIGHTPHRASE` 

: Sequences of lexemes and variables, written `[[...]]` in plain CBS:
  
  `\LEFTPHRASE ... \RIGHTPHRASE` produces $$\LEFTPHRASE \ldots \RIGHTPHRASE$$

`\LEFTGROUP...\RIGHTGROUP`

: Grouping in a regular expression, written `(...)` in plain CBS:
  
  `\LEFTGROUP ... \RIGHTGROUP` produces $$\LEFTGROUP \ldots \RIGHTGROUP$$

  Elsewhere, use `(` and `)`.

`\mid`

: Alternatives, written `...|...` in plain CBS:
  
  `... \mid ...` produces $$\ldots \mid \ldots$$

`\PLUS`, `\STAR`, `\QUERY`

: Iterations, written `+`, `*`, `?` in plain CBS:
  
  `\SYN{stmts}\QUERY`, ...
