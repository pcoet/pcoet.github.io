---
date: 2025-01-06
categories:
  - MkDocs
  - Material for MkDocs
  - web development
---

# Site migration

In 2019, I created this site using [Jekyll](https://jekyllrb.com/). At the time,
I thought that Jekyll had the best integration with
[GitHub Pages](https://pages.github.com/), which is where I planned to host the
site.

Over the 2024-2025 holidays, I decided to publish new content for the first time
in a few years. But the custom [Bootstrap](https://getbootstrap.com/) styling
that I'd implemented back in 2019 and 2020 looked dated. I could have refreshed
the styles and scripts from within my Jekyll setup, but I wanted to explore the
possibility of migrating to a modern static site generator &ndash; something not
built on Ruby. I considered [Hugo](https://gohugo.io/) and looked into several
themes, including [PaperMod](https://github.com/adityatelange/hugo-PaperMod) and
[Docsy](https://www.docsy.dev/about/). Ultimately I decided to migrate the site
to the third-party [MkDocs](https://www.mkdocs.org/) theme
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/), which is
currently the top-ranked theme in the MkDocs
[theme catalog](https://github.com/mkdocs/catalog#-theming).

At this point, the initial migration is complete, and I'm reasonably happy
with the result. Material for MkDocs is a nice tool if you want to stand up a
documentation website without doing any web development. If you want a fully
custom look and feel, you'd probably be better off creating your own theme for
MkDocs or Hugo. But at this point I don't have a lot of time for side projects,
and I want to focus on content, rather than CSS.

## New quickstarts

In addition to migrating the site, I created three new quickstart tutorials:

* [Go quickstart](../../tutorials/go-quickstart.md)
* [Python quickstart](../../tutorials/py-quickstart.md)
* [TypeScript quickstart](../../tutorials/ts-quickstart.md)

I frequently use the workflows documented in these tutorials, so I'll try to
keep the content fresh and accurate. 

