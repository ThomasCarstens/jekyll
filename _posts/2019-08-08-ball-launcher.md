---
layout: single
title: "Ball launcher"
excerpt: "Ping pong ball launcher: an example of fast prototyping."

header.image: assets/images/posts/ball-launcher/full.jpg
header:
  teaser: assets/images/posts/ball-launcher/full.jpg
  overlay_image: assets/images/posts/ball-launcher/full.jpg
categories: Lifestyle Ventures
toc: true
toc_sticky: true
date: 2019-05-31
gallery:
  - image_path: /assets/images/posts/ball-launcher/ballselector.jpg
    alt: "App pic 4"
    title: "Some snapshots"
  - image_path: /assets/images/posts/ball-launcher/turntable.jpg
    alt: "App pic 3"
    title: "Some snapshots"
  - image_path: /assets/images/posts/ball-launcher/frontshooter.jpg
    alt: "App pic 3"
    title: "Some snapshots"
gallery2:
  - image_path: /assets/images/posts/ball-launcher/shooter.jpg
    alt: "App pic 5"
    title: "Some snapshots"
  - image_path: /assets/images/posts/ball-launcher/base.jpg
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


### Hardware used
{% include gallery id="gallery" caption="Fast prototyping." %}
2. STM32F051C6 with C language
