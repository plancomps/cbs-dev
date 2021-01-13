---
title: Testing
mathjax: true
---
# Local browsing

This page explains how to browse and edit the website locally.

## Requirements

- [Ruby]\: 2.6.5 or 2.7.2
    
- [Jekyll]\: 3.8.7 or 4.1

## Setting up

1.  Clone or download a zip of the current [cbs-dev repository on Github].

2.  Run the following commands in a terminal from the `cbs-latex` directory:
    
    `jekyll <= 4.1.1`:
    ```bash
    bundle update
    bundle exec jekyll serve
    ```

## Browsing

Open a web browser at
[`http://localhost:4000/cbs-latex/`](http://localhost:4000/cbs-latex/)
(the final `/` is required).

Stop the local server with Control-C when no longer needed.

To browse in dark mode, set `color_scheme: dark` in `_config.yml` and restart
`jekyll serve`.

## Editing

Jekyll updates the web pages when you change the Markdown files (it takes a few seconds).

To experiment with MathJax, add $$\LATEX$$ enclosed in `$$...$$`.
See the MathJax documentation for the list of supported $$\LATEX$$ commands.
To define a new $$\LATEX$$ command for use on more than one page, 
add it to the MathJax configuration in `_includes/head_custom.html`
(see [MathJax] for an explanation of the notation).
You can define a command locally for use on a single page by `$$\newcommand...$$`.

[cbs-dev repository on Github]: https://github.com/plancomps/cbs-dev

[Ruby]: https://www.ruby-lang.org/

[Jekyll]: https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll

[MathJax]: http://docs.mathjax.org/en/latest/input/tex/extensions/configmacros.html
