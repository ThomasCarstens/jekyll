---
layout: single
title: "Service Robot"
excerpt: "A low-cost mobile robot to deliver medication, keys and other small items."
header:
  teaser: assets/images/posts/service-robot/line-follower-construction.png
  overlay_image: /assets/images/posts/service-robot/line-follower-construction.png
categories: Projects
tags:
- Robot
- Autonomous system
- Solidworks
- Lasercutting
- C++
- STM32
toc: true
toc_sticky: true
date: 2019-01-12
gallery:
  - image_path: /assets/images/posts/service-robot/h-bridge.png
    alt: "Custom h-bridge"
    title: "Custom h-bridge"

  - image_path: /assets/images/posts/service-robot/line-sensors.png
    alt: "Custom line-sensors"
    title: "Custom line-sensors"

  - image_path: /assets/images/posts/service-robot/voltage-regulator.png
    alt: "Custom voltage regulator"
    title: "Custom voltage regulator"

---

# Service Robot

In hospitals, offices and other public spaces, medication, keys, and other small items might need to be carried from one place to the other.  In this scenario, people may prefer to focus on more difficult tasks, and a low cost  robot may carry small items.

{%
include figure
image_path="/assets/images/posts/service-robot/line-follower-construction.png"
alt="Line follower construction"
caption="Here it is."
%}

## Aim
This project took place as part of an undergraduate robotic design course. In a team of 4, we designed an autonomous robot that follows a figure-of-8 line traced on the floor, first forwards, then in reverse.  An STM32 microcontroller was used and programmed in C to steer the motors from the line sensor input. Sensors were required on the front and back for forward and reverse steering.

{%
include figure
image_path="/assets/images/posts/service-robot/flow-chart-diagram.png"
alt="Flow chart diagram"
caption="Flow chart diagram"
%}

### Time-bound
2 months development in a team of 4, in a very busy 3rd year of engineering.
I acted as Head of Mechanical Design and Integration of Circuitry.

### Limitations
The main challenge was to have the final prototype cost less than R100 ($1.40), excluding the 8V battery. This meant that custom parts were to be built (namely custom electronics as shown below, custom coupling of gears instead of a gearmotor, and a custom robot frame).

{%
include figure
image_path="/assets/images/posts/service-robot/budget-layout.png"
alt="Budget layout"
caption="Budget layout"
%}

This project involved careful design and rapid prototyping of the chassis, requiring strong hands-on and practical ability.
The design was further optimised for low cost as can be seen below.

## Mechanical design
What follows are the technical drawings, software and an optimized mechanical structure.

{%
include figure
image_path="/assets/images/posts/service-robot/full-assembly.jpg"
alt="Full assembly"
caption="Full assembly"
%}

## Electronics
{% include gallery caption="Custom electronics: h-bridges (2), line sensors (8), voltage regulator (1), custom-made for cost." %}

Limitation: the local UCT lasercutters did not do a good job on cutting our gears. It turned out that it was not accurate enough.

## Mechanical optimisation
I later went and improved the chassis.

{%
include figure
image_path="/assets/images/posts/service-robot/mechanical-structure.jpeg"
alt="Mechanical structure"
caption="Improved chassis"
%}
