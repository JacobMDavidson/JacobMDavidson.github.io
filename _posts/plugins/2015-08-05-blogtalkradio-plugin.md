---
layout: post
title: Blog Talk Radio Plugins
description: "My brother hosts a personal fitness podcast on blogtalkradio. After uploading each episode, he would manually creating a blog post on his business website and embed the blogtalkradio show within that post. This was extremely time consuming, and annoying for him. With a little digging, I discovered I could help him automate the process. Shortly thereafter, the blogtalkradio plugin and widget were born."
modified: 2015-08-05
tags: [plugin, personal, WordPress]
comments: false
image:
  feature: plugins/blog-talk-radio.png
---

## The Problem

My brother hosts a personal fitness podcast on [Blog Talk Radio](http://www.blogtalkradio.com/starkradio). After uploading each episode, he would manually creating a blog post on his business website and embed the Blog Talk Radio show within that post. This was extremely time consuming, and annoying for him. With a little digging, I discovered I could help him automate the process. Shortly thereafter, the Blog Talk Radio plugin and Blog Talk Radio widget were born.

## The Plugin

The [blog talk radio plugin](https://github.com/JacobMDavidson/blogtalkradio-wordpress-plugin) adds a shortcode that can be used to post the entire Blog Talk Radio show for any host. This shortcode takes the form [blocktalkradio username="" itemcount="" itunes="" logo=""].

1. username - The host of the radio show.
2. itemcount - The maximum number of episodes to display on the page.
3. itunes - If set to "true", displays a link to the show's iTunes page.
4. logo - If set to "true", displays the shows logo at the top of the page.

Using my brother's site as an example, the following image depicts the logo and iTunes link displayed at the top of the page, along with the most recent show's details:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/starkradio.png" alt="">
</figure>

The title for each episode is displayed with the h2 tag. The embedded episode is below the title and to the left of the description for that episode. A link to the episode on blog talk radio is also provided. The following image shows the formatting for the feed of shows:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/starkradio2.png" alt="">
</figure>

The plugin works by compiling information about the host and each episode from a few location. The logo's URL, as well as the url, title, and description of each episode are retrieved from http://www.blogtalkradio/username.rss. The host id and iTunes link, as well as the url, show id, and embed code for each episode are retrieved from http://www.blogtalkradio/username/playlist.xml. The resulting arrays are combined via the episode URL, and the information is displayed.

This plugin is freely available on [GitHub](https://github.com/JacobMDavidson/blogtalkradio-wordpress-plugin). Feel free to fork it and tweak away!

## The Widget
