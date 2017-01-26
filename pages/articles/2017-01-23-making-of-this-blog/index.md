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
4  Creating a new post
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

After going through a couple of the themes in that section I landed on  [Lumen](https://github.com/wpioneer/gatsby-starter-lumen).

To use this theme we'll have to create another blog and apply the theme from the start. After we do this we will have no need for the blog we created up there.

- Change directory to parent folder: `cd ..`

- Delete my-blog: `rm -r my-blog`

- Create a new blog with Lumen theme: `gatsby new my-blog https://github.com/wpioneer/gatsby-starter-lumen`

- Change directory to generated folder `cd blog`

- Run Gatsby in develop mode: `gatsby develop`

The blog should be on `localhost:8000` again, with the Lumen theme. Go ahead and open this folder in your editor of choice.

Now lets personalize this site to have more content about you. Right off the bat you'll notice the site title is generic, that picture's not yours, there is dummy text in the description, about me, and contact me, and there may be some extra icons in the 'Social' area than you need.

Most of these can be tackled in the `config.toml` file in your root project directory. Update the `site-title`, `siteDescr`, and `siteAuthor`. As for the social site urls add links to the ones that matter to you, and for the rest you can choose to delete them or leave the `#`. Google analytics ID you can choose to add if you have one and we'll talk about the `linkPrefix` later.

Having added links to social media, it's time we updated the page to reflect that change. Open `components/SiteLinks/index.jsx` and update the list there to only show the links you require.

Next we'll the contents of the blog. Starting with the 'About me' and 'Contact Me' pages, the code to which can be found in the `index.jsx` file under `pages/pages/about` and `pages/pages/contact` respectively. As for the blogs, they are located under `pages/articles`. If you decide to get rid of the blogs, in the next section I have a script that creates a new post for you.

## Creating a post

It's quite arduous creating a blog post, especially with the date format in the file and the folder name. I searched around Gatsby to see if they had an auto-create but couldn't find anything. I did however run into this [script](https://github.com/pamo/pamo.github.io/blob/development/new_post.js), pretty solid script. I made a couple additions to include a couple more details, here is my script:

```Javascript
const prompt = require('prompt')
const mkdirp = require('mkdirp')
const moment = require('moment')
const _ = require('underscore.string')
const yaml = require('js-yaml')
const fs = require('fs')

prompt.start()

/*eslint-disable */
prompt.get(['title', 'path', 'category', 'description'], (err, result) => {
  'use strict'
  const dir = `./pages/articles/${ moment().format('YYYY-MM-DD') }-${ _.slugify(result.path) }`
  mkdirp.sync(dir)

  let postFileStr = '---\n'

  const frontmatter = {
    title: result.title,
    date: moment().toJSON(),
    layout: 'post',
    draft: true,
    path: `/${result.path}/`,
    category: result.category,
    description: result.description,
  }

  postFileStr += yaml.safeDump(frontmatter)
  postFileStr += '---\n'

  fs.writeFileSync(`${ dir }/index.md`, postFileStr, {
    encoding: 'utf-8',
  })

  return console.log(dir);
})
```

This script is also in [my repo](https://github.com/RonakR/ronakraithatha.github.io/blob/master/new_post.js), incase you need to check if it's up to date.

Run the script in your terminal with: `node <file_name>.js`

Follow the prompts and viola, a new folder and post with the frontmatter will be added to your `pages/articles`.


