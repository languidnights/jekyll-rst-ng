.. contents:: Table of Contents
   :backlinks: top

Overview
========

This plugin adds `ReStructuredText`_ support to `Jekyll`_ and `Octopress`_.
It renders ReST in posts and pages, and provides a custom directive to
support Octopress-compatible syntax highlighting.

Requirements
============

* `Jekyll`_ *or* `Octopress`_ >= 2.0
* `Docutils`_
* `Pygments`_
* `RbST`_

Installation
============

1. Install Docutils and Pygments.

   One convenient way is to use `venv`_ and `pip`_:

   ::

      $ python3 -m venv ${site_directory}/.venv
      $ .venv/bin/pip install docutils pygments

   You can also use your distibution's package manager if you're on a
   linux install. For example, in Debian or Ubuntu, you can use apt ::

     $ sudo apt install python3-docutils python3-pygments

   or in Fedora, use dnf ::

     $ dnf install python-docutils python-pygments

   From here on, we assume you have these installed and in your PATH
   such that if you type ``command -v rst2html5`` and
   ``command -v pygmentize`` you get a result indicating where it's
   installed.

2. Install the Plugin

   In your ${site_root}/Gemfile add the following line. ::

      gem "jekyll-rst_ng", git: "https://github.com/languidnights/jekyll-rst-ng", tag: "v2.1.1"

   In your ${site_root}/_config.yml add the folling line in the plugins
   definition. Yes using a *slash* is the only way I can get it to work! ::
      plugins:
         - jekyll/rst_ng

   Before you start blogging, issue a ``bundle install`` even if you
   installed jekyll and its plugins from your package manager.

3. Start blogging in ReStructuredText. Any file with the ``.rst`` extension
   will be parsed as ReST and rendered into HTML.

   .. note:: If you installed Docutils and Pygments via virtualenv and
   pip, be sure to activate the ``jekyll-rst`` virtualenv before
   generating the site by issuing a
   ``. ${site_directory}.vev/bin/activate``. I suggest you follow
   `Harry Marr's advice`_ and create a ``.venv`` file that will
   automatically activate the ``jekyll-rst`` virtualenv when you
   ``cd`` into your project.

Source Code Highlighting
========================

A ``code-block`` ReST directive is registered and aliased as
``sourcecode``.  It adds syntax highlighting to code blocks in your
documents::

   .. code-block:: ruby

      # Output "I love ReST"
      say = "I love ReST"
      puts say

Optional arguments exist to supply a caption, link, and link title::

   .. code-block:: console
      :caption: Read Hacker News on a budget
      :url: http://news.ycombinator.com
      :title: Hacker News

      $ curl http://news.ycombinator.com | less

Octopress already includes style sheets for syntax highlighting, but
you'll need to generate one yourself if using Jekyll ::

   $ pygmentize -S default -f html > css/pygments.css

Octopress Tips
==============

* Use ``.. more`` in your ReST documents to indicate where Octopress's
  ``excerpt`` tag should split your content for summary views.

Restoring Default CSS
=====================

If you want to restore the default stylesheet for rst2html5, copy the
math.css, miminal.css, and plain.css from your
${site_directory}/share/docutils/writers/" directory docutils into your
css folder and include them in the ``<head>`` of your
_includes/head.html. For example, in my setup I have my css in
<site_root>/assets/css/style.css.
::

  <link rel="stylesheet" href="{{ "/assets/css/math.css" | relative_url }}">
  <link rel="stylesheet" href="{{ "/assets/css/minimal.css" | relative_url }}">
  <link rel="stylesheet" href="{{ "/assets/css/plain.css" | relative_url }}">

Known Limitations
=================

jekyll-rst only knows about the directives python-docutils'
implementation of rst2html5 knows about. In Debian Stable, for example,
the `:ref:` directive isn't known about by docutils, and so it isn't
recognized here

Contributing
============

I have only tested this fork on my personal websites. As the `original
project`_ hasn't had development since 2013, so things in the
`Docutils`_ universe has changed since then, so I anticipate there to be
issues for more complex setups.

If you have any issues, the best way to report them is through
`Github Issues`_

If you want to contribute and are proficient in either Python or Ruby,
then sending a `Pull request`_ is the best way to get your patch in
front of our eyes.

.. _original project: https://github.com/xdissent/jekyll-rst
.. _ReStructuredText: https://docutils.sourceforge.io/rst.html
.. _Jekyll: https://jekyllrb.com/
.. _Octopress: https://octopress.org/
.. _Docutils: https://pypi.org/project/docutils/
.. _Pygments: https://pypi.org/project/Pygments/
.. _RbST: https://rubygems.org/gems/RbST
.. _bundler: https://bundler.io/
.. _Harry Marr's advice: https://hmarr.com/2010/jan/19/making-virtualenv-play-nice-with-git/
.. _venv: https://docs.python.org/3/library/venv.html
.. _pip: https://docs.python.org/3/installing/index.html#installing-index
.. _Github Issues: https://github.com/languidnights/jekyll-rst/issues
.. _Pull request: https://github.com/languidnights/jekyll-rst/pulls
