---

sources: https://github.com/hh-lohmann/jekyll-basal-scaffold

---


.... ! jbs als Präfix einschmuggeln als Wiedererkennungswert - oder "hh"? ... oder "nat" für "NOT A THEME" ...

# jekyll-basal-scaffold

***A basal, transparent, and portable scaffold for Jekyll (NOT A THEME)***

Meant for a quick initialization of a full functional [Jekyll](https://jekyllrb.com/) environment without stumbling over the fuzzes of *feature packed* themes and dependencies.


## Background

`jekyll new` creates an environment with rather demonstrational and often unneeded stuff, while at the same time some things seem to miss. A top example is Jekyll's default [minima](https://github.com/jekyll/minima) theme that at the same time produces an `assets` directory in the output while hiding important mechanics like the `_includes` and `_layouts` folders in its [RubyGems `gemdir` directory](https://guides.rubygems.org/command-reference/#gem-environment). This may hinder quick understanding for what's going on under the hood and of course is not portable at all (see considerations for the `Gemfile` below).

Note that the [`--blank` option](https://github.com/jekyll/jekyll/blob/0728ccf08b08759d75b6bac40091151a80556565/lib/jekyll/commands/new.rb#L15) for `jekyll new` gives you a source directory without a theme and its impacts, but also without `_includes` and some other things. 


## Goal

Coming near the **source** structure as depicted in [Jekyll's documentation](https://jekyllrb.com/docs/structure/):

```sh
    .
    ├── _config.yml
    ├── _data
    |   └── members.yml
    ├── _drafts
    |   ├── begin-with-the-crazy-ideas.md
    |   └── on-simplicity-in-technology.md
    ├── _includes
    |   ├── footer.html
    |   └── header.html
    ├── _layouts
    |   ├── default.html
    |   └── post.html
    ├── _posts
    |   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
    |   └── 2009-04-26-barcamp-boston-4-roundup.md
    ├── _sass
    |   ├── _base.scss
    |   └── _layout.scss
    ├── _site
    ├── .jekyll-metadata
    └── index.html
```

... but still more reduced, and yet with the - standard Jekyll, but not mentioned above - "404" (here, same with "index", as MD, not HTML), `presets.yml` in `_data, `head.html` in `_includes`, and `main.html` instead of `default.html` in `_layouts` (see below), as well as, of course, `.gitignore`:

---
```sh
    .
    ├── _config.yml
    ├── _data
    |   ├── presets.yml
    ├── _includes
    |   ├── footer.html
    |   └── head.html
    |   └── header.html
    ├── _layouts
    |   ├── main.html
    ├── _site
    ├── .gitignore
    ├── .jekyll-metadata
    ├── 404.md
    └── index.md
```
---

Note that `_site` and `.jekyll-metadata` are resulting unavoidable from Jekyll builds *in local directories*. On GitHub Pages the Jekyll build process stages behind the curtain, so you won't have them there (if you are using a local Jekyll for development befor publishing on GitHub Pages, the `.gitignore` should keep them local).

The **output** structure and contents of the "empty" scaffold alone should be like this:

---
```sh
    .
    ├── 404.html
    └── index.html
```
---

Anything else that is output will come from your content, not from the scaffold or from hidden defaults like the [`jekyll feed` plugin](https://github.com/jekyll/jekyll-feed) - of course you may add such features as you like, but esp. a default feed mechanism you are not aware of might be a way to your data you are not aware of.


## Prunings

Compared to `jekyll new`:

* theme (mimima): deleting `minima` for `theme:` in `_config.yml`
    * effects in no `about.md` in the source directory and no `about` and `assets` in the output
* feeds: deleting `-jekyll-feed` under `plugins:` in `_config.yml`
    * effects in no `feed.xml` in the output
* no Sass cache: adding [`cache: false` under `sass:` in `_config.yml`](https://github.com/jekyll/jekyll-sass-converter/issues/49#issuecomment-212600316)
    * effects in no `.sass-cache` in the source directory
* no `Gemfile` / `Gemfile.lock` in the source directory
    * A `Gemfile` and its accompanying `Gemfile.lock` are part of Ruby programs distributed as "gems" (packages) via [RubyGems package manager](https://rubygems.org/) and describe dependencies of a given gem like "command line Jekyll" (<https://rubygems.org/gems/jekyll/>). Jekyll instruments its `Gemfile` [to make projects more portable](https://jekyllrb.com/docs/ruby-101/#bundler) since the statements in the `Gemfile` define the environment that is required to run without errors - but effectively it can make projects less portable since a certain environment is required. In practice a `Gemfile` makes sense if you are using very special features of Jekyll, a theme, plugins etc. that may fail even with another version of Jekyll, a theme, plugins etc., but in that case you should be experienced enough to maintain a `Gemfile` that fits your needs on your own and better not rely on a default `Gemfile`, or if in a special scenario required "settings" are clearly given as for [local Jekyll vs. GitHub Pages](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) or for [Jekyll under Windows](https://jekyllrb.com/docs/installation/windows/).
* no `_posts` (not in the source directory and so not as default in the output)
    * `_posts` is a crucial part in the design of Jekyll, but, on the one hand, may not be important for many environments, and, on the other hand, does not depend on a special position in the directory structure and should, also in this respect, be handled as rather content specific (like user defined [Collections](https://jekyllrb.com/docs/collections/)).


## Additions

Compared to `jekyll new`:

* `presets.yml` in `_data` in the source directory
    * ... "description" etc. aus `_config.yml` ...
    * `_config.yml` should configurate Jekyll, esp. the build process, but not content
    * also to illustrate the mechanics
* `_includes` in the source directory with
    * `footer.html`
        * for inclusion in `main.html` as HTML `<footer></footer>`
        * empty besides "footer"-Tag, mainly to illustrate the mechanics
    * `head.html`
        * for inclusion in `main.html` as HTML `<head></head>`
    * `header.html`
        * for inclusion in `main.html` as HTML `<header></header>`
        * empty besides "header"-Tag, mainly to illustrate the mechanics
* `_layouts` in the source directory with `main.html` instead of `default.html`
    * "main" expresses the non-technical reading of "default" as "for most cases"
        * note that in the proper technical definition a "default" may be exactly a case that never happens in reality
    * "default" suggests "failed to provide a more suitable solution"
        * a "default.html" would make sense if this file would step in if no layout was explicitly specified, but, on the contrary, you need to explicitly define "default" to use it


## Changes

Compared to `jekyll new`:

* `index.md` and `404.md` instead of `*.html` in the source directory
    * ".md" should make it clearer that this are content files
        * other than the functional files in `_layouts` or files that are just copied to the output
    * note that the resulting `404.html` only works under GitHub Pages and Ruby's [WEBrick server](http://ruby-doc.org/stdlib-2.0.0/libdoc/webrick/rdoc/WEBrick.html) behind `jekyll serve` without any [further steps](https://jekyllrb.com/tutorials/custom-404-page/)
        * including a 404 in the scaffold is a strong reminder not to forget something that catches typos etc.
* [`.gitignore`](https://git-scm.com/docs/gitignore)
    * no mention of `.sass-cache` since Sass cache is deactivated by `_config.yml`
    * `_site` commented out, uncomment with e.g. Git Hub Pages when developing with local builds, but pushing only source
    * explanations for entries as comments in file
* ... `_config.yml`... "description" etc. nach _data/presets.yml


## WONTFIX

* no css, no js, no metadata, no libraries, no frameworks, no tools, no hooks, no admin, no preconfiguration

This scaffold has to be basal, transparent, and portable. There should be no purpose or use case built in, it should rather be possible to use it even to compose program code out of building blocks, [dot graph](https://www.graphviz.org/) layouts, or anything else that has no deeper relationship to webpages and their properties besides that a web browser should be able to display it. So any "helpful preconfiguration" or anything that looks like will lead to something else and WILL NOT happen here.

Pure skeleton, no flesh.

        
## Usage

1. Fork or download.
2. Check `.gitignore` for possible adjustments (see above)
3. Change / add / delete files and their contents depending on your needs
    * ... besides this README file and the ...COPYING file ...
    * tip: have a look at [Jekyll's manifold options and / or flags](https://jekyllrb.com/docs/configuration/) for the construction of content
      * esp. the `--config` option could be worth for a look


## Copyright / Warranty

```
    MIT License

    Copyright (c) 2018 hh.lohmann@yahoo.de

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.
```
