---
layout: post
title: Link Testing blog
image: /img/testing-image.jpg
tags: ["test", "tools","jekyll", "comms","home"]
permlink: /jekyll-links/
---

When I transferred my blog post from the free `username.github.io` web address to my personal domain name `www.ssnhub.com` I ad many of my links break. This is the short bit of code that explains what happened to me.

Use the following three lines of code to explore how Jekyll handles links:

```{r }
* [An absolute link](http://www.ssnhub.com/index)
* [A root relative link](/index/)
* [A Jekyll post_url link]({% post_url 2017-06-05-checking-links %})
```

* [An absolute link](http://www.ssnhub.com/index)
* [A root relative link](/index/)
* [A Jekyll post_url link]({% post_url 2017-06-05-checking-links %})
* `[A Jekyll post_url link]({% post_url 2017-06-05-checking-links %})`

## References

I worked through this using several blogs from other GIThub accounts below:

- [Stack Overflow](https://stackoverflow.com/questions/4629675/jekyll-markdown-internal-links): jekyll markdown internal links

- [Configuration-Jekyll](https://jekyllrb.com/docs/configuration/): Simple, blog-aware, static sites

- [Jekyll site](https://www.chenhuijing.com/blog/handling-articles-on-external-sites/): Handling external posts on your own 

- [Jekyll 3.2.1](https://github.com/jekyll/jekyll/issues/5709): https mixed content problem, Issue #5709, jekyll/jekyll
- [Controlling URLs](https://www.digitalocean.com/community/tutorials/controlling-urls-and-links-in-jekyll): and Links in Jekyll-DigitalOcean
