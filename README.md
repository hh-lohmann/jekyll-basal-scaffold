---

sources: https://github.com/hh-lohmann/jekyll-basal-scaffold

---

[TODO]:<f>

  [ !jkBS als Präfix einschmuggeln als Wiedererkennungswert - oder "hh"? ]: #

  [ oder "nat" für "NOT A THEME" ]: #

[/TODO]:</f>

# jekyll-basal-scaffold (jkBS)

***A basal, transparent, and portable scaffold for Jekyll (NOT A THEME)***

Meant for a quick initialization of a full functional [Jekyll](https://jekyllrb.com/) environment without stumbling over the fuzzes of *feature packed* themes and dependencies.


## *TL;DR*

A plain directory structure for Jekyll projects that you can directly [download](https://github.com/hh-lohmann/jekyll-basal-scaffold/archive/master.zip) 


## Background

`jekyll new` creates an environment with rather demonstrational and often unneeded stuff, while at the same time some things seem to miss. A top example is Jekyll's default theme [minima](https://github.com/jekyll/minima) that at the same time produces an `assets` directory in the output while hiding important mechanics like the `_includes` and `_layouts` directories in its [RubyGems `gemdir` directory](https://guides.rubygems.org/command-reference/#gem-environment). This may hinder quick understanding for what's going on under the hood and of course is not portable at all (see considerations for the `Gemfile` below).

Note that the [`--blank` option](https://github.com/jekyll/jekyll/blob/0728ccf08b08759d75b6bac40091151a80556565/lib/jekyll/commands/new.rb#L15) for `jekyll new` gives you a source directory without a theme and its impacts, but also without `_includes` and some other things (see the [site_template on GitHub](https://github.com/jekyll/jekyll/tree/master/lib/site_template)).


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

... but still more reduced, and yet with the - standard Jekyll, but not mentioned above - "404" (like other files as MD, not HTML, see below), a new file `presets.yml` in `_data`, `head.md` and `main` directory in `_includes`, and `main.md` instead of `default.html` in `_layouts` (see below), as well as, of course, `.gitignore`:

---
```sh
    .
    ├── _config.yml
    ├── _data
    |   └── presets.yml
    ├── _includes
    |   └── _main-layout
    |       ├── footer.md
    |       ├── head.md
    |       └── header.md
    ├── _layouts
    |   └── main-layout.md
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

Anything else that is output will come from your content, not from the scaffold or from hidden defaults like the [`jekyll feed` plugin](https://github.com/jekyll/jekyll-feed) - of course you may add such features as you like, but esp. a default feed mechanism you are not aware of might be a way to your data that you are not aware of.


### Flavors?

*RTFM*: flavored to be basal AND transparent AND portable
* Allergics may replace all *files* completey by own ones, the sole directory structure should not smell
* OK: pure \_post'er boys and girls are not addressed by this project

Note that some file extensions here (see below) differ from some examples in the Jekyll docs, but this should even lead to a better understanding of the docs.


## Prunings

Compared to `jekyll new`:

* theme (mimima): deleting `theme:` key in `_config.yml` (including value `minima`)
    * effects in no `about.md` in the source directory and no `about` and `assets` in the output
* feeds: deleting `plugins:` key in `_config.yml` (including `-jekyll-feed`)
    * effects in no `feed.xml` in the output
* no Sass cache: adding [`cache: false` under `sass:` in `_config.yml`](https://github.com/jekyll/jekyll-sass-converter/issues/49#issuecomment-212600316)
    * effects in no `.sass-cache` in the source directory
    * note that Jekyll hat Sass support [built in](https://jekyllrb.com/docs/assets/) and that a `.sass-cache` dir would result even if you might have no idea what Sass is
        * if you enjoy Sass, you should have or strive for enough know-how to make things appropriate without default dirs
* no `Gemfile` / `Gemfile.lock` in the source directory
    * A `Gemfile` and its accompanying `Gemfile.lock` are part of Ruby programs distributed as "gems" (packages) via [RubyGems package manager](https://rubygems.org/) and describe dependencies of a given gem like "command line Jekyll" (<https://rubygems.org/gems/jekyll/>). Jekyll instruments its `Gemfile` [to make projects more portable](https://jekyllrb.com/docs/ruby-101/#bundler) since the statements in the `Gemfile` define the environment that is required to run without errors - but effectively it can make projects less portable since a certain environment is required. In practice a `Gemfile` makes sense if you are using very special features of Jekyll, a theme, plugins etc. that may fail even with another version of Jekyll, a theme, plugins etc., but in that case you should be experienced enough to maintain a `Gemfile` that fits your needs on your own and better not rely on a default `Gemfile`, or in a special scenario where required "settings" are clearly given as for example [local Jekyll vs. GitHub Pages](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) or for [Jekyll under Windows](https://jekyllrb.com/docs/installation/windows/).
* no `_posts`
    * `_posts` is a crucial part in the design of Jekyll, but, on the one hand, may not be important for many environments, and, on the other hand, does not depend on a special position in the directory structure and should, also in this respect, be handled as rather content specific (like user defined [Collections](https://jekyllrb.com/docs/collections/)).


## Changes

Compared to `jekyll new`:

* `.md` instead of `*.html` in the source directory
    * `.md` should say clearly "this is a source file"
    * `.md`'s typical file association to a Markdown editor should benefit your workflow
    * :exclamation: note that this does not affect the functioning of includes concerning [Front matter variables](https://jekyllrb.com/docs/step-by-step/03-front-matter/)
        * Generally Jekyll doesn't care about file extensions, i.e it opens all files in the source directory (that are not excluded by `_config.yml`) and parses those who have textual content and processes their Front matters and [Liquid Tags](https://jekyllrb.com/docs/step-by-step/02-liquid/#tags), but in files that are connectetd via [`include` tag](https://jekyllrb.com/docs/includes/) it processes only tags and no Front matters, i.e. Front matters will be output as literal file content (if not encapsualed in a [comment tag](https://shopify.github.io/liquid/tags/comment/) - note here that Liquid primarily is a "third party component" from Shopify what may explain the divergent behaviour with includes).
            * Note that there are no [Jekyll Variables](https://jekyllrb.com/docs/variables/) concerning includes
            * Compare [Jekyll's Order of Interpretation](https://jekyllrb.com/tutorials/orderofinterpretation/)
        * [Parts of the Jekyll docs](https://jekyllrb.com/tutorials/orderofinterpretation/#markdown-in-include-file-not-processed) name a difference between Markdown files and "HTML files" without stating what defines an "HTML file", but clearly it is not the file extension that decides
* [`.gitignore`](https://git-scm.com/docs/gitignore)
    * no mention of `.sass-cache` since Sass cache is deactivated by `_config.yml`
    * `_site` commented out, do uncomment it for e.g. Git Hub Pages when developing with local builds, but pushing only source
* `_config.yml`
    * *Guidelines*
        * frequently updated settings in data files, not in `_config.yml`
            * cf. the out-of-the-box `_config.yml`: "If you find yourself editing this file very often, consider using Jekyll's data files feature for the data you need to update frequently."
        * `_config.yml` should house settings, data should go to data files
            * data concern content
            * settings concern build options and defaults
              * note that defaults for Front matters should also count as rather content related, but they only work as settings in `_config.yml`
    * added
        * `exclude:`
            * `- LICENSE`
                * this repo's license of course has little to with your output content
                    * but DO NOT DELETE LICENSE FILES neither in this repo nor in others, as in most cases you are not allowed to use / fork the repo without a copy of LICENSE
            * `- README.md`
                * the README is meant for dealing with the repo, not for the audience or purpose of your output
                    * but do not delete it since it contains valuable information
    * moved
        * `description:` to `meta:` in _data/presets.yml (see there)
    * deleted (alphabetical order)
        * `baseurl:` - not necessary since not used anywhere
            * note: has nothing to do with the [HTML base tag ](https://developer.mozilla.org/de/docs/Web/HTML/Element/base)
        * `email:` - not necessary since not used anywhere
            * contained in the out-of-the-box `_config.yml` for theme `minima`, not for Jekyll itself
        * `markdown:` (with value `kramdown`) - technically not necessary
            * Jekyll uses kramdown  [by default](https://jekyllrb.com/docs/configuration/markdown/#kramdown), i.e. you neither have to specify kramdown nor `markdown:` at all
            * note that kramdown's "non-standard" Markdown features raises no problems since, with Jekyll, you would at most interchange Markdown files with other Jekyll environments that run also kramdown
        * `title:` - not necessary since not used anywhere
            * contained in the out-of-the-box `_config.yml` for theme `minima`, not for Jekyll itself
        * `url:` - not necessary since not used anywhere
            * contained in the out-of-the-box `_config.yml` for theme `minima`, not for Jekyll itself


## Additions

Compared to `jekyll new`:

* `presets.yml` in `_data` in the source directory
    * ... "description" etc. aus `_config.yml` ...
    * ... ! https://jekyllrb.com/docs/datafiles/
    * ... ! https://symfony.com/doc/current/components/yaml/yaml_format.html#collections ...
    * `_config.yml` should configurate Jekyll, esp. the build process, but not content
    * also to illustrate the mechanics
* `_includes/` in the source directory with
    * `_main-layout/` directory with
      * `footer.md`
          * for inclusion in `_layouts/main-layout.md` as HTML `<footer></footer>`
          * empty besides "footer"-Tag, mainly to illustrate the mechanics
      * `head.md`
          * for inclusion in `_layouts/main-layout.md` as HTML `<head></head>`
      * `header.md`
          * for inclusion in `_layouts/main-layout.md` as HTML `<header></header>`
          * empty besides "header"-Tag, mainly to illustrate the mechanics
      * :bulb: the `_main-layout` subdirectory makes explicit that these includes are meant for the `main-layout` layout
        * note that not only layouts may use includes, so "-layout" is a hint
        * for further layouts and /or complex includes you should also use a subdirectory, e.g. `post-layout`
* `_layouts/` in the source directory with `main-layout.md` instead of `default.html`
    * "main" expresses the non-technical reading of "default" as "for most cases"
        * note that in the proper technical definition a "default" may be exactly a case that never happens in reality
        * "default" suggests "failed to provide a more suitable solution"
            * a "default.html" would make sense if this file would step in if no layout was explicitly specified, but, on the contrary, you need to explicitly define "default" to use it
              * a real default layout may be defined by a [Front matter default](https://jekyllrb.com/docs/configuration/front-matter-defaults/)
              * compare the [default *filter*](https://shopify.github.io/liquid/filters/default/) that throws in a value if a required variable is empty, but also note that this might hide deeper errors and misconfigurations
    * :bulb: the `-layout-` suffix makes explicit that this is a layout template - though that also follows directly from the containing directory and the utilisation by `layout: `, the suffix gives more overall transparency
* Hints, Don't forgets, and references in all files
    * of course you may delete all of that, esp. if you are experienced enough and only interested in a small and empty scaffold


## WONTFIX

* no css, no js, no metadata, no libraries, no frameworks, no tools, no hooks, no admin, no preconfiguration

This scaffold has to be basal, transparent, and portable. There should be no purpose or use case built in, it should rather be possible to use it for databases, databanks, data collection systems, or even to compose program code out of building blocks or [dot graph](https://www.graphviz.org/) layouts, or anything else that has no deeper relationship to webpages or something to display in web browser. So any "helpful preconfiguration" or anything that looks like will lead to something else and WILL NOT happen here.

Pure skeleton, no flesh.

        
## Usage

1. Fork / clone / download
2. Check `.gitignore` for possible adjustments (see above)
3. Change / add / delete files and their contents depending on your needs
    * ... besides this README file and the ...COPYING file ...
    * tip: have a look at [Jekyll's manifold options and / or flags](https://jekyllrb.com/docs/configuration/) for the de- / construction and organisation of content
      * esp. the `--config` option could be worth for a look

Be aware that `404.html` in the output without any [further steps](https://jekyllrb.com/tutorials/custom-404-page/) only works under GitHub Pages and Ruby's [WEBrick server](http://ruby-doc.org/stdlib-2.0.0/libdoc/webrick/rdoc/WEBrick.html) behind `jekyll serve`. Including a 404 in the scaffold mainly is a strong reminder to not forget something that catches typos etc.


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
