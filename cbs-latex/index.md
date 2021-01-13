---
title: Home
layout: default
nav_exclude: true
---
# CBS-LaTeX

This site explains `cbs-latex`, a small LaTeX package for CBS specifications.
When CBS is marked up using the package, LaTeX formatting produces mathematical
typography, suitable for inclusion in published articles. A corresponding MathJax
configuration produces similar results from the same marked-up CBS when embedded
in web pages.

The highlighting of CBS symbols by `cbs-latex` is comparable to that shown on
the CBS-beta website (and to that provided by the CBS editor implemented in
Spoofax). Navigation in CBS specifications is supported by hyperlinks from names 
to declarations.

Markup using `cbs-latex` is quite low-level. This makes it easy to adjust the
layout to fit the intended page width, but tedious to write. Generation of
marked-up CBS from CBS source text is currently being implemented in Spoofax.
