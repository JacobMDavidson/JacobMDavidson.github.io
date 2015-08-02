---
layout: post
title: Coordinate Transformation
description: "My wife is a licensed land surveyor. She used an old c based console program to perform two dimensional coordinate transformations. This program required a carefully crafted text file as input in the same folder that the program resides. When run, it would produce a text file output in that same folder. In other words, she had a copy of this program in every project folder that required a coordinate transformation. Granted, this was an extremely small program, so the multiple copies didn't take up much space. After many years of use, computer upgrades rendered this program useless, and she didn't have access to the source code. She asked if I could create an updated application for her."
modified: 2015-08-01
tags: [csharp]
comments: false
image:
  feature: csharp/survey.png
---

## An App Request from my Wife

My wife is a licensed land surveyor. She used an old c based console program to perform two dimensional coordinate transformations. This program required a carefully crafted text file as input in the same folder that the program resides. When run, it would produce a text file output in that same folder. In other words, she had a copy of this program in every project folder that required a coordinate transformation. Granted, this was an extremely small program, so the multiple copies didn't take up much space. After many years of use, computer upgrades rendered this program useless, and she didn't have access to the source code. She asked if I could create an updated application for her.

## Chosen Framework

As an engineering firm, my wife's company runs everything on Windows systems. I chose to construct this application in C#.NET to ensure compatibility with their existing systems, and to simplify installation. The project used Git for version control with the main repository hosted on [GitHub](https://github.com/JacobMDavidson/Coordinate-Transformation/tree/master/CoordinateTransformation).

## Research

Not having access to the source code, I had to research 2D coordinate transformation calculations using the least squares algorithm. I settled on the fifth edition of *Adjustment Computations - Spatial Data Analysis* by Charles D. Ghilani, as my algorithm source. Specifically, chapter 18 provided the necessary information to perform this calculation.

The coordinate transformation calculations are matrix based. Instead of developing my own matrix calculations, I found a freely available [C# matrix class](https://github.com/darkdragon-001/LightweightMatrixCSharp) written by [Ivan Kuckir](http://blog.ivank.net). This resource saved me a TON of time!

## The Solution

<figure style="text-align: center">
    <img src="{{ site.url }}/images/csharp/coordinate.png" alt="">
</figure>

The completed application employs a simple GUI with text editing capabilities. There are two text boxes side by side. The left text box displays the input, and the right text box provides the calculated output. The input uses the same form to ensure backward compatibility, but adds the ability to include comments. There are four actions:

1. Open - Allows the user to browse for an input text file.
2. Save Input - Allows the user to save any changes made to the input file.
3. Run - Performs the 2D coordinate transformation and displays the output in the output text box.
4. Save Output - Allows the user to save the output to a chosen location.

## Improvements Over the Original Application

Adding the GUI to allow the user to open existing input files, or create new input files, eliminates the need to copy the program to every project folder in which it is needed. The user can install the application to one location, and use it for every project. Adding comment capability greatly increases readability of the input file, reducing mistakes. Adding immediate error messages allows the user to quickly locate mistakes in the input file, and the built in editing capabilities allows the user to quickly correct those mistakes.

Feel free to download the source code from [GitHub](https://github.com/JacobMDavidson/Coordinate-Transformation/tree/master/CoordinateTransformation).
