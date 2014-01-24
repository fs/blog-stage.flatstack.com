# blog-stage.flatstack.com
  
[![](https://semaphoreapp.com/api/v1/projects/fe841dbb-8871-4168-982e-fa3ee9d23659/130433/shields_badge.png)]
(https://semaphoreapp.com/fs/blog-flatstack-com)

Source code for http://blog-stage.flatstack.com

## How to create new post

* [Create new](https://github.com/fs/blog.flatstack.com/new/master/source?filename=yyyy-mm-dd-your-title.html.markdown)
  file inside [`source`](source) direcotry
* Set correct date and title in the new file name

![](https://www.monosnap.com/image/VF3xZsAewX5yOAsCV9qzBoJGlAjGyF.png)

* Set correct layout, date and title at the start of the file

```markdown
---
layout: post
title: Example Article
date: 2012-01-01
---
```

* Fill in post with your awesome content using [GitHub Flavored Markdown](http://github.github.com/github-flavored-markdown/)
* Commit file using "Commit changes" green button

![](https://www.monosnap.com/image/jN4wrsjq5iWlkNnuTVVWnEdBGgQiXz.png)

* Wait while post will be deployed to the http://blog-staging.flatstack.com


## Installation

```bash
# Clone the template
git clone git@github.com:fs/static-base.git ~/.middleman/fs-static-base

# Scaffold a project using static-base template
middleman init sitename --template=fs-static-base
cd sitename
bin/bootstrap
```

## Development workflow

1. Start server with `bin/server`
2. Make changes in the `source` folder
3. Checkout results in the browser on `http://localhost:4567`

## Manual deploy to Github pages

Run `bin/deploy`

Make sure you have specified correct `source/CNAME`

## Semaphore integration

### Test build

You can use [Semaphore](https://semaphoreapp.com) to make sure you source code
will be build successfully.

Add these build commands:

```bash
bin/bootstrap
bin/build
```

### Deploy automatically to Github pages

* Deploy type: `Capistrano`
* Deployment Strategy: `Manual`
* Deploy commands:

```bash
# git identity required for git push
git config --global user.email "firstname.lastname+semaphore@flatstack.com"
git config --global user.name "Semaphore"
bin/deploy
```
* SSH key: specify your ssh key or unique per project.
