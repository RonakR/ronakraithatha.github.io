---
title: Making of this Blog
date: '2017-01-24T01:46:00.378Z'
layout: post
path: /making-of-this-blog/
category: FrontEnd
description: Making this Blog
---

For a while I've been wanting to create a place where I can post tidbits of information I've learned through my days, both at work and outside. I set up a couple static site generators trying to find one I like working with. I tested with [Jekyll](https://jekyllrb.com/), [Middleman](https://middlemanapp.com/), [Hexo](https://hexo.io/) and finally landed on [Gatsby](https://www.staticgen.com/gatsby) after coming across it on [risingstars2016](https://risingstars2016.js.org/).

In this post I'm going demonstrate:
1. How to set up Gatsby
2. Add a theme to it
3. Push the blog to GitHub
4. Host it on GitHub pages
5. Redirect that GitHub page to a custom domain.


## Setting up Gatsby

Getting started with Gatsby was incredibly simple, the documentation on their [README](https://github.com/gatsbyjs/gatsby/blob/master/README.md) is in part to thank for that.

- Start off by globally installing Gastby: `npm install -g gatsby`

- Create a new blog: `gatsby new my-blog`

- Change directory to the generated folder: `cd my-blog`

- Run Gatsby in develop mode: `gatsby develop`

At this point you should see:
```
Server started successfully!
Listening at:
   http://0.0.0.0:8000
```
You should see the gatsby blog on your `localhost:8000` with the default theme.

## Adding a theme

Gatsby's repo has starter themes in the `Gatsby Starters` section of the README.