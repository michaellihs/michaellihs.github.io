michaellihs.github.io
=====================

This is a blog based on Jekyll which is hosted on Github pages.

````
.
├── Gemfile                                      Dependency configuration for Bundler
├── Gemfile.lock
├── README.md                                    This file
├── _config.yml                                  Base configuration for the blog
├── _includes                                    Partials for the HTML rendering
│   ├── footer.html
│   ├── head.html
│   └── header.html
├── _layouts                                     Layouts for the HTML rendering
│   ├── default.html
│   ├── page.html
│   └── post.html
├── _posts                                       That's the folder where the actual posts go into
│   ├── 2015-03-15-welcome-to-jekyll.markdown
│   └── ...
├── _resources
├── _sass                                         SASS stylesheets for the blog, get compiled by Jekyll automatically
│   ├── base
│   │   └── ...
│   ├── layout
│   │   └── ...
│   └── modules
│       └── ...
├── _site
│   ├── Gemfile
│   ├── Gemfile.lock
│   ├── README.md
│   ├── about
│   │   └── index.html
│   ├── css
│   │   └── main.css                              The compiled CSS file
│   ├── feed.xml                                  The rendered XML feed
│   ├── index.html                                The rendered index page
│   └── jekyll                                    Directory for the rendered posts for category 'jekyll'
│       └── ...
├── about.md                                      Contains the 'About' page
├── css                                           Root folder for the main SCSS file that has to include the SCSS files in _sass
│   └── main.scss
├── feed.xml                                      Template file for the RSS feed
└── index.html                                    Template file for the index page
````


Jekyll Usage
------------

To start a local server with Jekyll, run

    jekyll serve

from the root directory of this repository. Afterwards you can access the blog on [http://localhost:4000/](http://localhost:4000/) on your local machine.

While Jekyll is running, a file watcher will detect all the changes to your blog files and rebuild all artifacts if needed.


TODOs
-----

* Take a look at MetaData and SEO from http://www.fastcompany.com/3044352/the-secrets-of-holacracy
* Improve privacy concerning Disqus comments by first disabling them and using JavaScript switch to enable them - see http://panzi.github.io/SocialSharePrivacy/
