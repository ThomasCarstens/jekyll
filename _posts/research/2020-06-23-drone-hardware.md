---
layout: single
title: "Drone Hardware"
excerpt: "An overview of drone hardware."
header:
  teaser: ../assets/images/posts/braai-tongs/tongs-header.jpg
  overlay_image: assets/images/posts/braai-tongs/detail-open.jpg
categories: Research
tags:
- Drone
- Hardware
toc: true
toc_sticky: true
date: 2020-06-23
gallery:
  - image_path: /assets/images/posts/braai-tongs/left-attached.jpg
    alt: "Braai tongs attached"
    title: "Braai tongs attached"

  - image_path: /assets/images/posts/braai-tongs/left-detached.jpg
    alt: "Braai tongs detached"
    title: "Braai tongs detached"

---

# ![favicon](/assets/images/favicon.jpg){: .aligned-left} Drone hardware
**De Vinci Innovation Lab, ESILV: INFRASTRUCTURE | June 2020**

# TO BE EDITED
This and other tutorials are under construction for September 2020.


## Aim
This tutorial has 2 parts: a broad theoretical basis and then a tutorial to follow. I will want my drone to bring me back a pizza (large with cheese ~= 230g ). I want to figure out the drone specifics so that it brings me back my pizza. The main give-and-take takes place in balancing power and performance.


# Overview of drone components

{%
include figure
image_path="/assets/images/posts/drone_hardware/drone_components.jpg"
alt="All components"
caption="All drone components"
%}

A typical FPV racing quadcopter – whether assemble-to-fly or ready to fly – includes the following components:

- Air Frame
- 4 motors + spares
- 4 ESCs + spares ($20-40 for a total of 4)
- 4 props + lots of spares
- RC Flight controller
- Lithium-polymer (LiPo) battery + spares
- FPV Video transmitter (vTx) and receiver (vRx)
- Radio Control transmitter (Tx) and receiver (Rx)
- Antennas
- Battery straps
- FPV goggles
- Board camera for FPV feed
- HD camera for recording (optional, adds weight)

Where to start? Selecting components serves to balance drone **power and performance**.
However these vary depending on the specifications of all our components.
Ultimately, this is an **iterative process**.


# Balancing thrust to weight vs the energy needs of the drone
Battery-motors-frame take up 50-70% of the full drone weight. This will help get a first working estimate.
99% of the battery is used up by motors. Once our motors are selected, we look to satisfy the energy needs of the drone

## Equipment weight
### Rx and Tx radio components
Weight:
### Power Distribution Board, Landing gear
### Battery Connectors
Soldering battery connectors can be a real pain, so it is a good idea to try find a battery connector that you like, and stick to it. That allows you to swap batteries easily, and if you decide to build another drone in the future you can use the same batteries. Common connectors include Deans/Tplug, XT60, and also EC3 connectors.

## Frame
The drone frame will affect drone dynamics, including speed

### How do I get the drone to fly faster?
Tilting a craft sideways provides the thrust for movement, tilt too far and you lose the fight against gravity.
https://dronerush.com/how-fast-can-a-drone-fly-science-of-flight-10953/

## Motors

### Start selection with hover thrust
Manufacturers of drone motors express the thrust in grams or ounces. This is the weight that one motor is able to lift off the ground. It doesn't mean, though, that a thrust equal to the weight of the drone is sufficient! In most cases, you should plan for a 2:1 thrust to weight ratio, to allow your drone to hover at just half throttle.

- We will analyze a drone that has a body weighing 500 grams, and a 4S LiPo battery weighing 150 grams. Additionally, we want to attach an FPV camera that puts an additional 50 grams on our drone.
- Pick the thrust to weight ratio. Let's assume we just begun to learn shooting FPV videos, and a ratio of 3:1 will be sufficient.
- Determine the number of motors in your drone. We're building a quadcopter, so we will keep the default value of four.

### Motor quality
Obviously at the motors: more coils/ thicker wire means more Volts at fewer Amps thus more torque (ie. More agility e.g. turns vs sprints) however heavier.
Motor quality: Relating Torque to V/I/efficiency/output Power.

Motors supposed to do some work and two important values define how powerful the motor is. It is motor speed and torque – the turning force of the motor.
τ = (I * V * E * 60) / (rpm * 2π)
https://simplemotor.com/calculations/
As you can see, this is variable:
{%
include figure
image_path="/assets/images/posts/drone_hardware/Power-Curves.jpg"
alt="All components"
caption="All drone components"
%}

Minitestbench
https://www.miniquadtestbench.com/
{%
include figure
image_path="/assets/images/posts/drone_hardware/motor_select.png"
alt="All components"
caption="All drone components"
%}

The most popular motor manufacturers include:

- T-Motor: the F-series can deliver up to 7kg thrust
- Cobra: high quality choice
- EMax: especially the RS2205 S
- Brotherhobby: esp. R4 or T2


### Selecting propellers
Propellers can also offer more torque when more surface area/angle of attack. All to be calculated according to local air density. More surface area means more battery consumption!

### Total battery consumption

## Battery
(Usually Last step) A bigger battery can either increase your flight time, or allow for unusual bursts of current (more power), but the weight returns to the TtoW ratio.

{%
include figure
image_path="/assets/images/posts/drone_hardware/LiPo.jpg"
alt="All components"
caption="All drone components"
%}

- Turnigy Nano-tech
- Turnigy Graphene
- Tattu (expensive but excellent performance)
### Longer Flight Time: Balancing Voltage and Capacity

time = capacity * discharge / AAD

A cell which can be considered a battery in itself, holds a nominal voltage of 3.7V. By connecting more of these in series, the voltage can increase to 7.4V for a 2 cell battery, 14.8V for a 4 cell battery and so on.

So the number of cells is what defines the voltage of the battery. Having a higher voltage means the battery can provide more power to drive bigger motors, however more power does not necessarily mean the battery will provide energy for longer, that is defined by the battery capacity.

Factors that will sap energy:
- Motor speed
- Bursts of power


### Bursts of power

### Selecting ESCs when selecting the battery: iteration
Three things that tend to increase your current draw and put more stress on your ESC:

- Higher motor KV
- Larger motor size (stator width and height)
- Heavier propellers (length and pitch)

https://oscarliang.com/choose-esc-racing-drones/
The firmware that an ESC can use is dependent on the hardware.
ESC firmware is the software running on every ESC, which determines the ESC’s performance, which protocols are supported, and what configuration interface can be used.

{%
include figure
image_path="/assets/images/posts/drone_hardware/esc_firmware.jpg"
alt="All components"
caption="All drone components"
%}

https://oscarliang.com/esc-firmware-protocols/

- T-Motor F30A FPV 30A: very high quality, BLHeli_S Dshot capable
- KISS 24A Race Edition: Expensive, high quality, proven.
- DYS BLHeli_S XS30A: Dshot capable
- Spedix 30a ESC HV 3-6s DSHOT: inexpensive, light (5g), Dshot capable and smaller than most other ESCs

# Balancing the drone's center of gravity
The physical size of drone, and especially of battery, can affect the center of gravity.

# How to maintain the Lipo battery?
See here: https://www.genstattu.com/bw
