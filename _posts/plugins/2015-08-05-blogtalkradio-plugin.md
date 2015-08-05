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

My brother hosts a personal fitness podcast on [Blog Talk Radio](http://www.blogtalkradio.com/starkradio). After uploading each episode, he would manually creating a blog post on his business website and embed the Blog Talk Radio show within that post. This was extremely time consuming, and annoying for him. With a little digging, I discovered I could help him automate the process. Shortly thereafter, the [Blog Talk Radio plugin](https://github.com/JacobMDavidson/blogtalkradio-wordpress-plugin) and [Blog Talk Radio widget](https://github.com/JacobMDavidson/blogtalkradio-wordpress-widget) were born.

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

The title for each episode is displayed within the h2 tag. The embedded episode is below the title and to the left of the description for that episode. A link to the episode on blog talk radio is also provided. The following image shows the formatting for the feed of shows:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/starkradio2.png" alt="">
</figure>

The plugin works by compiling information about the host and each episode from a few locations. The logo's URL, as well as the url, title, and description of each episode, are retrieved from http://www.blogtalkradio/username.rss. The host id and iTunes link, as well as the url, show id, and embed code for each episode, are retrieved from http://www.blogtalkradio/username/playlist.xml. The resulting arrays are combined using the episode URL, and the information is displayed.

This plugin is freely available on [GitHub](https://github.com/JacobMDavidson/blogtalkradio-wordpress-plugin). Feel free to fork it and tweak away!

## The Widget

The [blog talk radio widget](https://github.com/JacobMDavidson/blogtalkradio-wordpress-widget) is used to embed the blog talk radio show player for a given host into a widget. Once this plugin is installed and activated, Blogtalkradio will be found in your available widgets. Add the widget to your preferred location, enter the name of the radio show, and enter the number of episodes to display. Hit save, and you're all set.

I'll once again use my brother's show as an example. Adjust the settings as necessary, and the player will be embedded to the selected location.

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/widget-admin-panel.png" alt="">
</figure>

Here's what it looks like when added to the header widget location:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/widget-header.png" alt="">
</figure>

And here it is in a sidebar:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/widget-sidebar.png" alt="">
</figure>

This plugin is also freely available on [GitHub](https://github.com/JacobMDavidson/blogtalkradio-wordpress-widget).
