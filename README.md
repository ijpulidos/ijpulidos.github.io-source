# Source for http://ijpulidos.github.io

This repository contains the source for http://ijpulidos.github.io/.

It's basically just a direct copy of [Jake VanderPlas' Pythonic preambulations blog](http://jakevdp.github.io).
License allows it :). Thanks Jake!

## Building the Blog

Clone the repository & make sure submodules are included

```
$ git clone https://github.com/ijpulidos/ijpulidos.github.io.git
$ git submodule update --init --recursive
```

Install the required packages:

```
$ conda create -n pelican-blog python=3.5 jupyter notebook
$ source activate pelican-blog
$ pip install pelican Markdown ghp-import
```

Build the html and serve locally:

```
$ make html
$ make serve
$ open http://localhost:8000
```

Deploy to github pages

```
$ make publish-to-github
```

Don't forget to change the `GITHUB_PAGES_REMOTE` variable in the `Makefile` if
you are going to use this as a template for your own blog.
