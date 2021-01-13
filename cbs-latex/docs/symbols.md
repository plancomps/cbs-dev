---
title: Symbols
# parent: Macros
nav_exclude: true
mathjax: true
---

# Symbols

`\KEY{Keyword}`

: CBS keyword: 
  $$\KEY{Rule}$$, $$\KEY{Built-in Funcon}$$, ...

  MathJax-3.1.2 bug: `\KEY{...} ~ \KEY{...}` overlays the keywords

`\STRING{Characters}`

: Literal CBS string, written `"..."` in plain CBS:
  $$\STRING{Hello world!}$$, ...
  
  The macro encloses the argument in double quotes.

`\ATOM{Characters}`

: Literal CBS atom, written `'...'` in plain CBS:
  $$\ATOM{location-42}$$, ...
  
  The macro encloses the argument in single quotes.

`\LEX{Lexeme}`

: Language keyword or separator, written `'...'` in plain CBS grammars and rules:
  
  Ordinary ASCII characters that produce themselves:
  $$\LEX{0}
  ~ \LEX{1} ~ \ldots
  ~ \LEX{9}
  ~ \LEX{A} ~ \ldots
  ~ \LEX{I} ~ \ldots
  ~ \LEX{O} ~ \ldots
  ~ \LEX{Z}
  ~ \LEX{a} ~ \ldots
  ~ \LEX{z}
  ~ \LEX{!}
  ~ \LEX{(}
  ~ \LEX{)}
  ~ \LEX{*}
  ~ \LEX{,}
  ~ \LEX{.}
  ~ \LEX{/}
  ~ \LEX{=}
  ~ \LEX{?}
  ~ \LEX{@}
  ~ \LEX{[}
  ~ \LEX{]}$$
  
  Special characters produced by macros:
  
  | Macro               | character  | $$ $$ | $$ $$ | $$ $$ |
  | ------------------- | ---------- | - | - | - |
  | `\LEX{\HASH}`       | $$\LEX{\HASH}$$ |
  | `\LEX{\DOLLAR}`     | $$\LEX{\DOLLAR}$$ |
  | `\LEX{\PERCENT}`    | $$\LEX{\PERCENT}$$ |
  | `\LEX{\AMPERSAND}`  | $$\LEX{\AMPERSAND}$$ |
  | `\LEX{\APOSTROPHE}` | $$\LEX{\APOSTROPHE}$$ |
  | `\LEX{\PLUSCHAR}`   | $$\LEX{\PLUSCHAR}$$ |
  | `\LEX{\HYPHEN}`     | $$\LEX{\HYPHEN}$$ |
  | `\LEX{\LESS}`       | $$\LEX{\LESS}$$ |
  | `\LEX{\GREATER}`    | $$\LEX{\GREATER}$$ |
  | `\LEX{\BACKSLASH}`  | $$\LEX{\BACKSLASH}$$ |
  | `\LEX{\CARET}`      | $$\LEX{\CARET}$$ |
  | `\LEX{\UNDERSCORE}` | $$\LEX{\UNDERSCORE}$$ |
  | `\LEX{\GRAVE}`      | $$\LEX{\GRAVE}$$ |
  | `\LEX{\LEFTBRACE}`  | $$\LEX{\LEFTBRACE}$$ |
  | `\LEX{\BAR}`        | $$\LEX{\BAR}$$ |
  | `\LEX{\RIGHTBRACE}` | $$\LEX{\RIGHTBRACE}$$ |
  | `\LEX{\TILDE}`      | $$\LEX{\TILDE}$$ |
  
  Note: `\LBRACE` and `\RBRACE` match the fixed-width font used for lexemes. 
  Elsewhere, use `\{` and `\}` to produce the mathematical symbols.
  
  Note: The quotes used in plain CBS would make grammars and semantic rules look messy, so they are omitted.
