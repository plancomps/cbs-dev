---
title: Rules
# parent: Macros
nav_exclude: true
mathjax: true
---

# Rules

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
