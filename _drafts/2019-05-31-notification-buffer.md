---
layout: single
title: "Notification buffer"
excerpt: "Most apps just mute notifications completely. I want to buffer them until I’m ready to receive them."

header.image: assets/images/posts/notification-buffer/buffer-header.jpeg
header:
  teaser: assets/images/posts/notification-buffer/buffer-header.jpeg
  overlay_image: assets/images/posts/notification-buffer/buffer-header.jpeg
categories: Lifestyle Ventures
toc: true
toc_sticky: true
date: 2019-05-31
gallery:
  - image_path: /assets/images/posts/notification-buffer/typing.jpeg
    alt: "App pic 4"
    title: "Some snapshots"
  - image_path: /assets/images/posts/notification-buffer/front-view.jpeg
    alt: "App pic 3"
    title: "Some snapshots"
gallery2:
  - image_path: /assets/images/posts/notification-buffer/macrodroid.jpeg
    alt: "App pic 5"
    title: "Some snapshots"
  - image_path: /assets/images/posts/notification-buffer/goodvibrations.jpeg
    alt: "App pic 6"
    title: "Some snapshots"
---

# Notification buffer
**Personal project – seeking funding**

## Project details


| Aim  | To better manage the flow of notifications from my social media  |
| Constraints  | The apps on the Playstore just mute notifications completely. I want to buffer them until I’m ready to receive them.  |
| Limitations  | There is no built-in mechanism to manage the flow of notifications.  |
| Success  | I wired up a system that works for me. (1)	I turn on the ‘silent’ button to put my phone on plane mode, and unmute to allow notifications. (2)	When notifications arrive, my phone vibrates in custom heartbeat patterns depending on which social media app sent the notification. |
| Recommendations  | Someone should develop this into a single app. I would only do it if there is enough support for this. I would love to take this a step further and send back automated messages depending on hand movements: I wrote below how I would do this. |


### Software used
{% include gallery id="gallery2" caption="Using two appstore apps in combination." %}
1. Macrodroid app for step 1
2. Good Vibrations app for step 2

### Work proposition
I am seeking funding to be able to make this a fully functional app. Please consider donating here.  
- If I reach R500, I will build an app that fulfills step 1.
- If I reach R1000 I will build an app that fulfills step 2.
- If I reach R2000 I will build the embedded system for step 3.

## Developing an embedded system for automated replies
I would love to take this a step further and send back automated messages depending on hand movements.

### Equipment

{% include gallery caption="Using Fitbit wristbands during development." %}

In each wristband is a vibration element to receive notifications.
Each wristband has a gyroscope to send rapid hand motion.
Finally each wristband has a microcontroller to connect remotely to the phone.

### Usecase 1
When the user taps the wristband, the gyroscope, micro and app become active.
The user can then tap a certain pattern that will be transmitted to the phone.
The app converts the pattern to a message, which is sent via social media.
