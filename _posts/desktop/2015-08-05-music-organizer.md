---
layout: post
title: Music Organizer
description: "My music file collection has grown rapidly since 1998, when MP3s first became popular. Over the past 17 years, this collection has become a tangled mess. I had no naming or tagging convention for the MP3s I owned. I had many song duplicates located in various folders and under different names. When I first began ripping my music, I didn't take the time to properly name and organize each track of each album. This resulted in many, many songs labeled track1, track2, etc., in a folder structure consisting of just the album name. Furthermore, these songs were not tagged in any way. Searching for a particular song or artist was nearly impossible. Organizing this mess would be a painful task. I set three goals to accomplish this task: properly tag each file, develop a unified folder structure to store each file, and eliminate duplicate files. I developed a Java program to make this possible."
modified: 2015-08-05
tags: [desktop, java, java desktop]
comments: false
image:
  feature: desktop/music-organizer.png
---

## The Problem

My music file collection has grown rapidly since 1998, when MP3s first became popular. Over the past 17 years, this collection has become a tangled mess. I had no naming or tagging convention for the MP3s I owned. I had many song duplicates located in various folders and under different names. When I first began ripping my music, I didn't take the time to properly name and organize each track of each album. This resulted in many, many songs labeled track1, track2, etc., in a folder structure consisting of just the album name. Furthermore, these songs were not tagged in any way. Searching for a particular song or artist was nearly impossible. Organizing this mess would be a painful task. I set three goals to accomplish this task:

1. Properly tag each file.
2. Develop a unified folder structure to store each file.
3. Eliminate duplicate files.

I set out to solve this problem in two parts. First, I used an open source solution to properly tag the music files. Next, I developed a desktop application to automate the renaming and relocating of music files based on tags, and to identify duplicates. The resulting desktop application is available on [GitHub](https://github.com/JacobMDavidson/MusicOrganizer).

## Tagging the Files

The solution for tagging the files was an easy one. A bit of research into audio file fingerprinting led me to the popular open source [MusicBrainz Picard](http://picard.musicbrainz.org) software. This software uses [AcoustID](https://acoustid.org) audio fingerprints to identify music, along with the MusicBrainz database of metadata to tag the identified tracks. I was able to completely tag my entire collection of music using this tool.

What good is a bunch of tagged music if the file names and folder structures haven't been changed? I developed a Java application to accomplish the second and third goals. I chose Java to accommodate the multiple operating systems I currently use.

## Music Organizer

The concept behind the music organizer is simple. It enumerate a directory searching for music files, and copies those music file to /default_documents_directoy/MusicOrganizerOutput/Artist/Album/Song_Title.ext, where ext is the file extension. Whenever a duplicate is found, it is listed as an error in the output, and the file is not copied. With one click of a button, I was able to organize my entire music library using this tool.

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/music-organizer-gui1.png" alt="">
</figure>

The GUI is simple. There's one button used to browse to the folder that the user would like to enumerate, and an output table that displays the results of the enumeration.

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/music-organizer-gui2.png" alt="">
</figure>

When a folder is selected, the application uses a SimpleFileVisitor to enumerate the directory. The extension for each visited file is checked to determine if it is a mp3, m4a, or m4p file. If it is a music file, the artist, album, and song title are extracted using the [Jaudiotagger](http://www.jthink.net/jaudiotagger/) library, and the file is copied to /default_documents_directoy/MusicOrganizerOutput/Artist/Album/Song_Title.ext using the [Commons IO](http://commons.apache.org/proper/commons-io/) library. If that song already exists, an error message is added to a running list of errors. Once completed, all error messages are displayed in the output table allowing the user to review the duplicate files. Note, the source files are not deleted during the migration to ensure no files are lost during the process. The user must manually delete the source files if he or she wants.

#### Features:

1. The SimpleFileVisitor is executed in a SwingWorker allowing it to run in the background. It takes a long time to copy large collections of music, and the SwingWorker eliminates the freezing effect of the enumeration.
2. A Timer is used to constantly update the GUI with the progress of the enumeration.

#### Planned Features:

As is, the application suits my needs, allowing me to accomplish my goals. To make it more user friendly for others there are a few features I may add if I find the time.

1. Allow the user to select the destination folder instead of automatically using /default_documents_directoy/MusicOrganizer/.
2. Allow the user to select the final folder structure instead of forcing the use of /artist/album/song_title.
3. Include more music file types for which to search. The chosen file types represent all of the file types present in my library, but there are many more available.
4. Add the option to automatically delete the source files when they are successfully copied to the destination.

## Conclusion

Though this was a relatively simple project, it really opened my eyes to the power of using programming to solve annoying problems. Had I done this manually, the migration would have taken days to finish. I spent approximately half a day creating this application, which greatly simplified the task.

Feel free to check out the source code on [GitHub](https://github.com/JacobMDavidson/MusicOrganizer).
