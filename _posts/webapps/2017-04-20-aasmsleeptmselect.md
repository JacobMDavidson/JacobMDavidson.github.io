---
layout: post
title: AASM SleepTM Select
description: "AASM SleepTM Select is a lightweight, HIPAA compliant telemedicine platform built specifically for sleep doctors. Developed with ease of use in mind, AASM SleepTM Select focuses on a simplified telemedicine encounter process."
modified: 2019-03-10
tags: [web app, .net web app]
comments: false
share: false
image:
  feature: webapps/sleeptm-select-header.png
---

<figure style="text-align: center">
    <img src="{{ site.url }}/images/webapps/sleeptm-select.png" alt="">
</figure>

## Summary

[AASM SleepTM Select](https://sleeptm.com) is more than a lightweight version of the AASM SleepTM Pro telemedicine platform. Select focuses on a streamlined encounter process that minimizes the barriers for a patient to join an encounter. With Select, the patient no longer needs a full SleepTM account to have a video encounter with their physician, which means they no longer have to complete the two factor authentication process unless they want to view their health history. This eliminates the cumbersome patient onboarding process that is required with the Pro version. While AASM SleepTM Pro is meant for physicians that want to use the platform as a pseudo EHR replacement as well as a telemedicine tool, Select was built for physicians that prefer a simple to use telemedicine platform while using a separate EHR.

### Architecture

This project was created with the initial intention of being a complete replacement for AASM SleepTM Pro. With this in mind, we chose a completely different set of technologies to build this new version of platform. The plan was to construct a base platform on top of which modules could be added for more functionality. We chose to build Select in ASP.NET 4.5 using C# and MVC 5. Entity Framework 6 was used with the database first approach and the repository pattern for all MS SQL database interactions. SignalR was used for real-time communications, and OpenTok's WebRTC platform formed the basis of the live video interaction. MembershipReboot was used for identity management and authentication. The application and database are both hosted on Microsoft Azure.

As soon as the base platform was completed, it was decided not to continue with this modular approach replacing Pro. Instead, this project was marketed as a light weight version of AASM SleepTM Pro.

### Features

*Secure, Web Based Video Portal*

AASM SleepTM Select provides a web-based, HIPAA compliant telemedicine platform. Anyone with a web cam, microphone, and access to a supported web browser can take part in an interactive live video one on one encounter. Browser support includes Chrome, Firefox, and IE11. Safari and Edge are not officially supported, but these browsers will work. By building this platform for the devices and software most people are already using, we greatly reduced the costs involved in implementing telemedicine.  

*Queued Patient Waiting Room*

Physicians are given a customizable virtual waiting room when they register an account with AASM SleepTM Select. Patients log in to this virtual waiting room and wait for their physician to invite them to join an encounter. The physician can see a list of all patients logged in to this waiting room at any given moment, and can select any one of them to join an encounter when they're ready.   

*Simplified Encounter Process*

During a Select version encounter the patient cannot access any of their patient health information, allowing us to simplify the join process. Physicians can give patients an access code to join the waiting room. This allows the patient to join the encounter without logging in to or even creating a full SleepTM patient account. If a patient does have a full SleepTM account, they can log in later to view their health information. This process eliminates the cumbersome patient onboarding process that is a frequent complaint of the Pro version.

*Accept Payments Electronically*

Physicians can link a Stripe account to accept credit card payments from patients prior to an encounter. With this "self-pay" feature, physicians can define a cost associated with several appointment types. When they schedule a self-paid appointment, physicians can assign a cost for that appointment. The patient will be required to pay the fee with a credit card before the encounter can begin.

*Simplified Scheduling*

The full, calendar-based scheduling system of the Pro version was replaced with an extremely simple, email-based scheduling system. Scheduling an appointment with a patient generates a unique access code for that patient, and emails both the physician and patient with a generic reminder that they have an appointment scheduled. This email includes a downloadable iCal file that each user can import into their calendar of choice if they want to receive reminders about the scheduled appointment. The physician has the ability to edit or cancel the appointment from within their dashboard and can send a reminder email with a simple click of a button.    

The learning curve for the full featured scheduling system proved to be an inconvenience for physicians. This simplified scheduling system virtually eliminated that learning curve making the Select version platform the best choice for those that want to get their telemedicine program established quickly and efficiently.

## Conclusion

AASM SleepTM Select solves many of the complaints about the AASM SleepTM Pro version platform. Select strips away many of the additional features to focus on a streamlined and seamless telemedicine encounter process. With Select, physicians are able to integrate a telemedicine program into their practice quickly and easily, and by eliminating the need for patients to log in to the system, onboarding them is effortless. If you're entrenched in an existing EHR and only require the telemedicine aspect of SleepTM, the Select version is perfectly suited for you.  
