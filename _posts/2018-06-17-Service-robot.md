---
layout: single
title: "Service Robot"
excerpt: "A low-cost mobile robot to deliver medication, keys and other small items."
header:
  teaser: assets/images/posts/service-robot/line-follower-construction.png
  overlay_image: /assets/images/posts/service-robot/line-follower-construction.png
categories: Other
tags:
- Data Science
- Visualization
toc: true
toc_sticky: true
date: 2019-01-12
---

# Service Robot

In hospitals, offices and other public spaces, medication, keys, and other small items might need to be carried from one place to the other.  In this scenario, people may prefer to focus on more difficult tasks, and a low cost  robot may carry small items.

{%
include figure
image_path="/assets/images/posts/service-robot/flow-chart-diagram.png"
alt="Flow chart diagram"
caption="Fig.1: Flow chart diagram"
%}

Time-bound: 2 months development.

This project took place as part of an undergraduate robotic design course. In a team of 4, we designed an autonomous line-following robot. The main challenge was to have the final prototype cost less than R100 ($1.40), excluding the 8V battery. This meant that custom parts were to be built (namely custom electronics as shown below, custom coupling of gears instead of a gearmotor, and a custom robot frame). An STM32 microcontroller was used and programmed in C to steer the motors from the line sensor input. Sensors were required on the front and back for forward and reverse steering. This project involved careful design and rapid prototyping, requiring strong hands-on and practical ability.


I acted as Head of Mechanical Design and Integration of Circuitry. The design was further optimised for low cost as can be seen below.

{%
include figure
image_path="/assets/images/posts/service-robot/budget-layout.png"
alt="Budget layout"
caption="Fig.2: Budget layout"
%}

What follows are the technical drawings, software and an optimized mechanical structure.

{%
include figure
image_path="/assets/images/posts/service-robot/full-assembly.jpg"
alt="Full assembly"
caption="Fig.3: Full assembly"
%}



{%
include figure
image_path="/assets/images/posts/service-robot/h-bridge.png"
alt="Custom h-bridge"
caption="Fig.4: Custom h-bridge"
%}

{%
include figure
image_path="/assets/images/posts/service-robot/line-sensors.png"
alt="Full assembly"
caption="Fig.5: Custom line-sensors"
%}

{%
include figure
image_path="/assets/images/posts/service-robot/voltage-regulator.png"
alt="Voltage regulator"
caption="Fig.6: Custom voltage regulator"
%}

Limitation: the local UCT lasercutters did not do a good job on cutting our gears. It turned out that it was not accurate enough.

I later went and improved the chassis.

{%
include figure
image_path="/assets/images/posts/service-robot/mechanical-structure.jpeg"
alt="Mechanical structure"
caption="Fig.6: Improved chassis"
%}
