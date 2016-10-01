---
layout:     post
title:      "How to Build Your Own Blog"
subtitle:   "best solution-GitHub Pages + Jekyll."
date:       2016-08-19 12:00:00
author:     "Yamin Li"
header-img: "img/post-bg-01.jpg"
---

## #Introduction
<p></p>

#### Github Pages ####

Here is the official introduction to [GitHub Pages](https://pages.github.com).

>"Websites for you and your projects. Hosted directly from your GitHUb repository. Just edit, push, and your changes are live."

Let's see what GitHub Pages can do with some examples. (Ranked by Stars)

  * [Bootstrap](http://getbootstrap.com)
  ![img](/img/in-post/2016-08-19/bootstrap.jpg)

  <!-- * [Facebook React](https://facebook.github.io/react/)
  ![img](/img/in-post/2016-08-19/react.jpg) -->

  * [Ratchet](http://twbs.github.io/ratchet)
  ![img](/img/in-post/2016-08-19/ratchet.jpg)

  * [Electron](http://electron.github.io/electron.atom.io)
  ![img](/img/in-post/2016-08-19/electron.jpg)

#### Jekyll ####

Here is the official introduction to [Jekyll](http://jekyllrb.com/docs/home/).

>Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through a converter (like [Markdown](https://daringfireball.net/projects/markdown/)) and our [Liquid](https://github.com/Shopify/liquid/wiki) renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to host your project’s page, blog, or website from GitHub’s servers for free.

So Github Pages + Jekyll is absolutely a good choice to build our first blog website.

---

## #To Start

* create your github repo first (fork or create your own)

```
git clone https://github.com/username/username.github.io
```

* install Jekyll

  * For mac user, install your own ruby version first(use rbenv)

  ````
  #homebrew to install rbenv
  ~ $ brew update
  ~ $ brew install rbenv

  #install our own ruby
  ~ $ rbenv install 2.3.1

  #check ruby versions
  ~ $ rbenv versions

  #using a ruby in the shell
  ~ $ rbenv shell 'rubyversion'

  ````

  * Install Jekyll and create your blog

  ````
  ~ $ gem install bundle
  ~ $ gem install jekyll
  ~ $ jekyll new myblog
  ~ $ cd myblog
  ~/myblog $ bundle install
  ~/myblog $ bundle exec jekyll serve
  # => Now browse to http://localhost:4000
  ````
* fork from whatever you like from [Jekyll Theme](http://jekyllthemes.org), and build your own on it.

  List some themes I really like.

  I. [Airspace](https://luminousrubyist.github.io/airspace-jekyll/)
  ![img](/img/in-post/2016-08-19/airspace.jpg)
  Auther: Andrew Lee  
  [HomePage](https://github.com/luminousrubyist/airspace-jekyll)

  II. [Jekyll-Uno](http://joshgerdes.com/jekyll-uno/)
  ![img](/img/in-post/2016-08-19/jekyll-uno.jpg)
  Auther: Josh Gerdes  
  [HomePage](https://github.com/joshgerdes/jekyll-uno)

  III. [Mug](http://nandomoreira.me/mug/)
  ![img](/img/in-post/2016-08-19/mug.jpg)
  Auther: nandomoreira.me  
  [HomePage](https://github.com/nandomoreirame/mug)

  VI. [Long Haul](http://brianmaierjr.com/long-haul/)
  ![img](/img/in-post/2016-08-19/long-haul.jpg)
  Auther: Brian Maier Jr.  
  [HomePage](https://github.com/brianmaierjr/long-haul)

  V. [Centrarium](http://bencentra.com/centrarium/)
  ![img](/img/in-post/2016-08-19/centrarium.jpg)
  Auther: Ben Centra  
  [HomePage](https://github.com/bencentra/centrarium)

## #Jekyll Directory Structure

A basic Jekyll site usually looks something like this:

````
.
├── _config.yml
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
├── _data
|   └── members.yml
├── _site
├── .jekyll-metadata
└── index.html

````

* `_config.yml` stores [configuration](https://jekyllrb.com/docs/configuration/) data, including blog title, favicon, description, contact info, visit info (Google Analysis).

* `_includes` are the partials that can be mixed and matched by your layouts an dposts to facilitate reuse. The liquid tag `{``%``include file.ext %}` can be used to include the partial  in `_include/file.ext`.

* `_layouts` are the templates that wrap posts. Layouts are chosen on a post-by-post basis in the [YAML Front Matter](https://jekyllrb.com/docs/frontmatter/). The liquid tag `{``{` `content }}` is used to inject content into the web page.

* `_posts` is your dynamic content lies. The naming must follow the format `YEAR-MONTH-DAY-title.MARKUP`.

* `_site` is where the generated site will be placed(by default) once Jekyll is done transforming it. It's probably a good idea to add this to your `.gitignore` file.

* `index.html` Provided that the file has a [YAML Front Matter section](https://jekyllrb.com/docs/frontmatter/), it will be transformed by Jekyll.

<!-- <h2 class="section-heading">The Final Frontier</h2> -->

<!-- <h2 class="section-heading">Reaching for the Stars</h2> -->

<!-- <a href="#">
    <img src="{{ site.baseurl }}/img/post-sample-image.jpg" alt="Post Sample Image">
</a>
<span class="caption text-muted">To go places and do things that have never been done before – that’s what living is all about.</span> -->
