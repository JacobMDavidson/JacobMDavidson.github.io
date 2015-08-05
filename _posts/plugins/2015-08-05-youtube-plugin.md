---
layout: post
title: YouTube prettyPhoto Widget
description: "While working on a site that made heavy used of lightboxes to display images and image galleries, the client requested the ability to display a featured video. They wanted this video to be displayed with a thumbnail in a widget area. At the time, there were plenty of YouTube video channel plugins, but I couldn't find any with lightbox capabilities. Using prettyPhoto, I developed this widget."
modified: 2015-08-05
tags: [plugin, personal, WordPress]
comments: false
image:
  feature: plugins/youtube.png
---

## Summary

While working on a site that made heavy used of lightboxes to display images and image galleries, the client requested the ability to display a featured video. They wanted this video to be displayed with a thumbnail in a widget area. At the time, there were plenty of YouTube video channel plugins, but I couldn't find any with lightbox capabilities. Using [prettyPhoto](http://www.no-margin-for-errors.com/projects/prettyPhoto-jquery-lightbox-clone/), I developed this widget.

## The Widget
The [Youtube prettyPhoto Widget](https://github.com/JacobMDavidson/youtube-prettyphoto-widget) is used to embed a youtube video into a specific widget area. When selected, the video will be played in a prettyPhoto lightbox. Once this plugin is installed and activated, YouTube with PrettyPhoto will be found in your available widgets. Add the widget to your preferred location, enter the widget's title, video URL, and thumbnail setting. Hit save, and you're all set.

Choose the widget area location, and adjust the settings as necessary:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/youtube-admin-settings.png" alt="">
</figure>

The video will be embedded in the chosen widget area:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/youtube-lightbox-sidebar.png" alt="">
</figure>

When the video is clicked, it is played inside a prettyPhoto lightbox:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/plugins/youtube-lightbox-video.png" alt="">
</figure>

Feel free to view the source code or fork the repository on [GitHub](https://github.com/JacobMDavidson/youtube-prettyphoto-widget).
