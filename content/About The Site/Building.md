+++
title = "Building the Site"
description = "This website was built using Hugo, an open-source static site generator, as well as a host of other tools and scripts. This doubles as a credits page of sorts."
date = 2018-09-16
+++

This website was made using [Hugo](https://github.com/gohugoio/hugo). It is deployed and built on Netlify with images handled by Netlify large media.

The layout is based on the [DocDock](https://github.com/vjeantet/hugo-theme-docdock) theme. This includes [Featherlight](https://noelboss.github.io/featherlight/) for lightbox viewing. Responsive images and lazyloading use [Lazysizes](https://github.com/aFarkas/lazysizes). This is implemented through a Hugo shortcode which selects from 8 variants of each image, one full-sized and only loaded when the image is clicked. 

I would have liked to use [Commento](https://gitlab.com/commento/commento) for the comment system; it's lightweight, respects privacy, and has good social integration given its size. However, since it requires its own hosting, it's not exactly within the spirit of this project. Comments now use [Disqus](https://disqus.com/). It has its drawbacks (overhead, user tracking, lack of control), but these are mitigated by the button at the bottom of each page, which only loads Disqus when clicked.