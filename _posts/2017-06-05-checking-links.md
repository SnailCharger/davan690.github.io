---
layout: post
title: Link Testing blog
image: /img/testing-image.jpg
---

When I transferred my blog post from the free `username.github.io` web address to my personal domain name `www.ssnhub.com` I ad many of my links break. This is the short bit of code that explains what happened to me.

Use the following three lines of code to explore how Jekyll handles links:

```{}
* [An absolute link](http://www.ssnhub.com/index)
* [A root relative link](/index/)
* [A Jekyll post_url link]({% post_url 2017-06-05-checking-links %})
```

* [An absolute link](http://www.ssnhub.com/index)
* [A root relative link](/index/)
* [A Jekyll post_url link]({% post_url 2017-06-05-checking-links %})

## References

I worked through this using several blogs from other GIThub accounts below:

- [jekyll markdown internal links - Stack Overflow](https://stackoverflow.com/questions/4629675/jekyll-markdown-internal-links)

- [Configuration-Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/configuration/)

- [Handling external posts on your own Jekyll site](https://www.chenhuijing.com/blog/handling-articles-on-external-sites/)

- [Jekyll 3.2.1 https mixed content problem · Issue #5709 · jekyll/jekyll](https://github.com/jekyll/jekyll/issues/5709)

- [Controlling URLs and Links in Jekyll-DigitalOcean](https://www.digitalocean.com/community/tutorials/controlling-urls-and-links-in-jekyll)
