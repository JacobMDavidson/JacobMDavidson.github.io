---
layout: post
title: AASM SleepTM iOS Application
description: "The AASM SleepTM iOS application gives patients access to the AASM SleepTM telemedicine platform from their iOS device. With this iOS app, patients can have a face to face encounter with their sleep provider from just about anywhere using their mobile device."
modified: 2018-10-28
tags: [ios, xamarin]
comments: false
image:
  feature: ios/sleeptm-ios-header.png
---

<figure style="text-align: center">
    <img src="{{ site.url }}/images/ios/sleeptm-ios.png" alt="">
</figure>

## Summary

The [AASM SleepTM iOS App](https://itunes.apple.com/us/app/aasm-sleeptm/id1253586517?mt=8) integrates with the AASM SleepTM platform allowing patients to engage in telemedicine encounters via an iOS device. Built using Xamarin.iOS, this application was launched in July of 2017 in the iOS App Store.  

Built with ease of use as a primary focus, this application enables a patient to log in to their encounter quickly and easily using one of two methods:

1. The username and password the patient selected when registering with AASM SleepTM.
2. An access code generated when a physician schedules an appointment with a patient.

If a patient uses the access code approach, they are immediately logged in to the physician's lobby where they wait until the physician is ready to start the encounter. If the patient fully logs in to their account, they are presented with a list of physicians to which their account is connected. They can choose to join the lobby for any of these physicians where they will wait until that physician starts an encounter with them.

## Architecture And Features

The development of this application required the use of many platform specific features so it was built using Xamarin.iOS. To facilitate the creation of this mobile app, AASM SleepTM database interactions were exposed via a web API built in ASP.NET 4.5 using MVC 5. Identity server 4 was used to protect this API using OpenID Connect and OAuth 2.0.

#### Shared Code

*API Communication*

All communications with the Identity Server and API are platform independent. To reuse this code, these communications were implemented in a portable class library. This includes logging the patient in using two factor authentication, and all other calls to the API for data stored within the database.

*Real-Time Communication With SignalR*

This mobile app connects to the SignalR hub of the web application for real time communication between both parties. This allows the physician to immediately see when a patient has joined their lobby and allows the patient to be notified as soon as a physician invites them to an encounter. All communications with the SignalR hub are platform independent allowing both the Android and iOS apps to use the same code.  

#### Platform Specific Code

*Interactive Video*

The video based encounter relies on the Xamarin bindings for the native iOS OpenTok SDK. OpenTok is a WebRTC based platform for interactive video. The encounter screen allows the patient to change their camera that is transmitting the feed, mute/unmute the patients microphone, mute/unmute the physicians audio, and request an end to the encounter. Ending the encounter requires both parties to mutually agree that the encounter is finished. One party requests the end of the encounter, and the other party must agree.

*Touch ID*

If available, the user can use the device's Touch ID to log in to their account. After initially logging in to their account with the username and password, the user can open the application settings to enable to this feature. Subsequent logins will ask the user to log in using Touch ID.

## Conclusion

This project was my first experience using Xamarin for mobile app development. Using C# for iOS development was an absolute game changer for me. Being able to develop a mobile app without having to "switch gears" saved a ton of time. To top it all off, I really enjoyed building the interface in XCode's interface builder. I can't wait to tackle my next Xamarin app!  
