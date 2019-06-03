---
layout: post
title: Link Testing blog
image: /img/testing-image.png
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

# References

I worked through this using several blogs from other GIThub accounts below:

-
