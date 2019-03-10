---
layout: post
title: AASM SleepTM Select
description: "AASM SleepTM Select is a lightweight, HIPAA compliant telemedicine platform built specifically for sleep doctors. Developed with ease of use in mind, AASM SleepTM Select focuses on a simplified telemedicine encounter process."
modified: 2018-10-28
tags: [web app, .net web app]
comments: false
image:
  feature: webapps/sleeptm-select-header.png
---

## Project Description Coming Soon

<figure style="text-align: center">
    <img src="{{ site.url }}/images/webapps/sleeptm-select.png" alt="">
</figure>

## Summary

[AASM SleepTM Select](https://sleeptm.com) is more than a lightweight version of the AASM SleepTM Pro telemedicine platform. Select focuses on a streamlined encounter process that minimizes the barriers for a patient to join an encounter. With Select, the patient no longer needs a full SleepTM account to have a video encounter with their physician, which means they no longer have to complete the two factor authentication process unless they want to view their health history. This eliminated the cumbersome patient onboarding process that is required with the Pro version.

AASM SleepTM Pro is meant for moonlighting physicians that want to use the platform as an EHR replacement as well as a Telemedicine tool. Select was built for physicians that prefer a simple to use Telemedicine platform while use their own EHR.

### Architecture

This project was created with the initial intention of being a complete replacement for AASM SleepTM Pro allowing us to choose a completely different set of technologies. The plan was to construct a base platform on top of which modules could be added for more functionality. We chose to build Select in ASP.NET 4.5 using C# and MVC 5. Entity Framework 6 was used with the database first approach and the repository pattern for all MS SQL database interactions. SignalR was used for real-time communications, and OpenTok's WebRTC platform formed the basis of the live video interaction.

As soon as the base platform was completed, it was decided not to continue with this modular approach replacing Pro. Instead, this project was marketed as a light weight version of AASM SleepTM Pro.

### Features

*HIPAA-Compliant, Web Based Video Portal*
*Queued Patient Waiting Room*
*Simplified Encounter Process*
*Accept Payments Electronically*
*Simplified Scheduling*

## Conclusion
