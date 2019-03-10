---
layout: post
title: AASM SleepTM Pro
description: "AASM SleepTM Pro is a full featured, HIPAA compliant telemedicine platform built specifically for sleep doctors. In addition to a secure video portal, this platform features an advanced scheduling system, integrated sleep diaries, secure messaging and file sharing, access to patient health information, the ability to accept patient payments electronically, a branded website, and branded marketing materials. AASM SleepTM Pro is an electronic health record replacement in addition to a telemedicine platform."
modified: 2019-03-10
tags: [web app, .net web app]
comments: false
share: false
image:
  feature: webapps/sleeptm-header-image.png
---

<figure style="text-align: center">
    <img src="{{ site.url }}/images/webapps/sleeptm-pro.png" alt="">
</figure>

## Summary

[AASM SleepTM Pro](https://sleeptm.com) is a full featured, HIPAA compliant telemedicine platform developed specifically for sleep doctors. AASM SleepTM Pro includes many of the features found in a full EHR and was developed for physicians that want an all-in-one telemedicine platform. Ideal for moonlighting physicians, this platform is capable of not only providing telemedicine services, but can also serve as an EHR replacement at a fraction of the cost.

### Architecture

Hosted in an Azure App Service, this project was built in ASP.NET 4.5 using VB.NET and Web Forms. The data access layer utilizes ADO.NET to connect to a MS SQL database also hosted on Azure. SignalR was used for real-time communications, and OpenTok's WebRTC platform formed the basis of the live video interaction. MembershipReboot was used for identity management and authentication.

### Features

*Secure, Web Based Video Portal*

AASM SleepTM Pro provides a web-based, HIPAA compliant telemedicine platform. Anyone with a web cam, microphone, and access to a supported web browser can take part in an interactive live video one on one encounter. Browser support includes Chrome, Firefox, and IE11. Safari and Edge are not officially supported, but these browsers will work. By building this platform for the devices and software most people are already using, we greatly reduced the costs involved in implementing telemedicine.

Within the encounter screen, patients and physicians can easily access information on past encounters and view all of the patients vital health information. Both the physician and the patient can take private notes during the encounter that are not accessible by the other party, and physicians have an opportunity to share specific notes at the conclusion of the encounter. Physicians can also share their screen during the encounter. With this feature, they have the option to share one of their monitors or to limit the screen share to a specific application. The physician has the ability to take screen shots of the encounter screen and is able to grant the patient access to these screen shots or any other document that they have previously uploaded to the system.

The encounter screen also includes a text chat feature that is typically used before the live interactive video portion of the encounter. This gives the physician the chance to let the patient know that they're reviewing the patients information before they begin the encounter. Typically the physician will warn the patient that the encounter is about to begin through this chat feature before they click the "Start Encounter" button. This also provides a mode of communication should there be a hardware failure for either user.

*Branded Webpage and Marketing Materials*

Each facility that registers with AASM SleepTM Pro is given a branded webpage and access to printable marketing materials that they can give to their patients. Facility administrators have complete control over the content, staff, and logo that are displayed on the facility's webpage. Patients can be directed to this page to request telemedicine appointments.

*Queued Patient Waiting Room*

Facilities are also given a virtual waiting room with their account. Patients log in to this waiting room and wait for their physician to invite them to join an encounter. The physician can see a list of all patients logged in to this waiting room at any given moment, and can select any one of them to join an encounter when they're ready.   

*Accept Payments Electronically*

Physicians can link a Stripe account to accept credit card payments from patients prior to an encounter. With this "self-pay" feature, physicians can define a cost associated with several appointment types. When they schedule a self-paid appointment, physicians can assign a cost for that appointment. The patient will be required to pay the fee with a credit card before the encounter can begin.

*Advanced Scheduling*

A full-featured, calendar-based scheduling system is included with AASM SleepTM Pro subscriptions. Physicians can schedule appointments and view past and future encounters at a glance within their dashboard. Patients can access details for past and future appointments on their own calendar. Growler notifications are displayed within physicians and patient accounts detailing upcoming appointments, and both user types can elect to receive email and text message notifications for all appointment reminders.

*Integrated Sleep Diaries*

Patients are able to track their sleep patterns using an integrated sleep diary. They can set reminders to manually fill out their diary each day or connect a Fitbit to automatically import their sleep data. Physicians are able to access the sleep diary of each of their patients.

*Patient Tasks*

Physicians can assign various tasks that the wish their patients to complete prior to any telemedicine encounter. Through these tasks physicians can assign reading material, questionnaires, etc. Patients are then requested to acknowledge that they have completed the task.

*Access Patient Health information*

Physicians can require patients to fill out a patient health history. When enabled, patients are given the opportunity to update this history and attest to it prior to joining the physician's virtual waiting room. The patient and the physician can later download this health history in a CDA R2 formatted document that can be imported in to many popular EHR systems.

*Secure File Sharing*

Physicians can upload documents and securely share them with specific patients. Only the patients that have been granted access to the document by their physician will be able to view the document. Physicians can grant and remove access to these documents at any time.

*Secure Messaging*

Physicians and patients can send messages to each other securely within the platform. Physicians can indicate whether or not their patients can initiate messages to them through the platform and can assign this permission to specific patients.   

## Conclusion

With AASM SleepTM Pro, physicians have all of the tools they need to effectively see and treat patients using telemedicine. This tool can virtually replace the physicians existing EHR giving them a single platform for all of their telehealth needs, making it the perfect solution for retired and moonlighting physicians.
