---
layout: post
title: JacobMDavidson.com
description: "A few months back, I finally decided to develop a personal website to provide a blogging platform and to showcase my project experience. I had acquired JacobMDavidson.com more than a year ago, and realized it was time to do something with it when it came up for renewal. The first step was to choose a platform. I chose to use GitHub Pages with Jekyll for this task."
modified: 2015-08-06
tags: [website, jekyll, jekyll website]
comments: false
image:
  feature: jekyll/github-jekyll.png
---
## Introduction

A few months back, I finally decided to develop a personal website to provide a blogging platform and to showcase my project experience. I had acquired JacobMDavidson.com more than a year ago, and realized it was time to do something with it when it came up for renewal. The first step was to choose a platform.

When I develop personal projects, I like to ensure they'll include a learning experience. I typically choose to sacrifice efficiency to gain experience with different technologies. The variety of tools and languages used to develop the applications found on this site will hopefully back that claim. I've created, and helped others create, several WordPress and Joomla based sites. I could have easily used one of those platforms to quickly get this site up and running, but I wanted to try something different.

Jekyll kept popping up within a technology related circle of friends on Facebook. I was intrigued by the server side page generation that ultimately serves static pages to visitors. This would mean no more dynamically generated pages, and no more database queries! Jekyll looked to be a fantastic answer to the bloated Wordpress and Joomla platforms I was used to. As soon as I discovered GitHub's free Jekyll site hosting via [GitHub Pages](https://pages.github.com), I decided to give it a try.

And I'm glad I did!

## Setup

Setting up a Jekyll site using [GitHub Pages](https://pages.github.com) is as simple as creating a repository named *username.github.io*. A custom url can be added in a few steps. First, a [CNAME record](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/) must be added to the repository that includes the custom url. Next, if you're configuring an apex domain, an [A record must be configured](https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/) with the DNS provider that points to GitHub's IP addresses. If you're configuring a subdomain, you must instead [configure a CNAME record](https://help.github.com/articles/tips-for-configuring-a-cname-record-with-your-dns-provider/) with the DNS provider. It may take some time for the changes to your DNS provider to take affect, but that's it. You now have a custom url pointing to your site.

To create a local environment, you'll need to install Jekyll on your machine. Fortunately, GitHub provides an easy way to [install Jekyll](https://help.github.com/articles/using-jekyll-with-pages/) with all of the settings that match GitHub's configuration.

To finish setting up your local environment, I suggest installing the GitHub desktop application for [Mac](https://mac.github.com) or [Windows](https://windows.github.com), along with the [Atom](https://atom.io) text editor. These tools work extremely well together and provide a seamless workflow.  Any text editor can be used, but I've found Atom to be an excellent choice. Clone the repository to your local machine, open a terminal at the projects folder, and, assuming you followed GitHub's installation instructions for terminal, type *bundle exec jekyll server*. You should now be able to view any changes made to your project at http://localhost:4000.

You're now up and running. Any changes you make to your site should be immediately visible locally once they are saved. Once you're satisfied, commit the changes and sync the repository. Now the changes will be visible on your GitHub pages website.

## Jekyll Basics

This is an extremely short introduction to using Jekyll. Check out the [Jekyll documentation](http://jekyllrb.com/docs/home/) for detailed information on using Jekyll.

The [Jekyll documentation](http://jekyllrb.com/docs/structure/) explains the overall folder structure quite nicely. I suggest downloading a [Jekyll theme](http://jekyllthemes.org) when you first start out. It'll get you up and running quickly. I went with the [HPSTR theme](https://www.mademistakes.com/work/hpstr-jekyll-theme/) created by Michael Rose as my starting template, and customized it to fit my needs as necessary. This theme is also available on [Github](https://github.com/mmistakes/hpstr-jekyll-theme).

When you get the theme set up, the first thing you'll want to do is add the \_site folder to your .gitignore file. Jekyll builds your site and stores the static version that it'll serve to clients in this folder. In other words, you don't want to make any changes to it. Next, you'll want to edit the \_config.yml file to suit your needs. After that, you can start creating posts in your \_posts folder.

[Posts](http://jekyllrb.com/docs/posts/) are generally markdown or HTML files, and need to include [YAML front matter](http://jekyllrb.com/docs/frontmatter/) to allow Jekyll to properly convert them into static pages. The file name must take the format YEAR-MONTH-DAY-title.md, YEAR-MONTH-DAY-title.html, etc, depending on the file type you're using. When building the site, Jekyll will convert every post in the \_posts folder to static pages regardless of the folder structure within \_posts.

To edit your layouts or add more functionality to your site, you'll need to brush up on [Liquid](https://github.com/Shopify/liquid/wiki). The [Jekyll documentation](http://jekyllrb.com/docs/templates/) provides detailed descriptions of the supported tags and filters.

This should be enough to get you started!

## Additional Tools

Though this isn't Jekyll related, I've been using [Mathjax](https://www.mathjax.org) to provide LaTeX functionality for formatting equations. [LaTeX](http://www.latex-project.org) is a document markup language that relies on markup tagging to stylize text.

## Review of Jekyll

Jekyll is an amazing tool that eliminates the bloat of conventional content management systems. Jekyll serves static pages, relying on the server to build those static pages once. There are no databases to interact with or php scripts building pages over and over as requests arrive. The result is a reliable and efficient site that won't break from plugin conflicts (as frequently happens with CMS platforms). Quite frankly, I'm surprised more people aren't using this tool for blogging. Once you get passed the learning curve, content generation is just as easy as with any popular CMS.

In other words, I'll be using this as a blogging tool for the foreseeable future.
