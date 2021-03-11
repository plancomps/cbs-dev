---
title: Colors
# parent: Macros
nav_exclude: true
mathjax: true
---

# Colors

### Colors

The default color of text and math symbols is black for PDFs, and either a dark gray or white for web pages.

The following four color macros are used internally by highlighting macros.
The definitions of the colors differ between PDFs and web pages,
and between light and dark color schemes on web pages.

Ideally, the colors should be distinguishable also to readers with color-impaired vision; this has not yet been checked.

`{\GRAYCOLOR ...}`

: For keywords $$\KEY{Keyword}$$ and grouping parentheses $$\LEFTGROUP\dots\RIGHTGROUP$$

`{\REDCOLOR ...}`

: For $$\NAME{funcons}$$ and $$\NAME{entities}$$ 

`{\GREENCOLOR ...}`

: For $$\SYN{syntax-sorts}$$

`{\BLUECOLOR ...}`

: For $$\SEM{semantic-functions}$$
