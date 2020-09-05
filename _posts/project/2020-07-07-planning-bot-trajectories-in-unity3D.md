---
layout: single
title: "Planning Unity3D Bot trajectories"
excerpt: "How to plan simple trajectories for videogame bots."
header:
  teaser: ../assets/images/posts/braai-tongs/tongs-header.jpg
  overlay_image: assets/images/posts/braai-tongs/detail-open.jpg
categories: Simulators for performance
tags:
- Crazyflie
- ROS
- Gazebo
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

# ![favicon](/assets/images/favicon.jpg){: .aligned-left} Drone programming: Hello World
**De Vinci Innovation Lab, ESILV: INFRASTRUCTURE | June 2020**

# TO BE EDITED
This and other tutorials are under construction for September 2020.

# Aim
The Crazyflie 2.1 drone flies a predefined trajectory. This tutorial will apply your code for Behaviour Planning onto a real drone.
Behind the scenes, the **Python code** sends commands to the Crazyflie 2.1 via the **Udacidrone API**.

## Portability of code from simulator to real life
You might want to develop such code. Are you fairly confident about your **programming logic**? After all, motors are sensitive and electronics break very easily.
You can test out your code on a **simulator** before you port it to a drone.
The github will be up shortly.

# Event-based Behaviour planning

## Introduction
## How a Chatbot uses behaviour planning
A basic Chatbot needs to respond to user input over time. This means we need some kind of sequence.

## How NOT to plan out our code: using variables as flags
This comes from a previous project I was engaged in.
A wheeled robot was required to rotate until it saw a face, and then approach the face.
This meant transitioning from `start` to `rotate` to `detect` to `approach` to `stop`.
The code for this will be available soon.

## How we plan out our code: better flow between transitions
We use Python classes and functions to make our code easily readable.

## Deciding when to transition
The transitions can occur according to some time or space constraints.
### Takeoff transition
### Waypoint transition
The waypoint transitions use some nifty code!

# Safety Concerns
[Wrap the Crazyflie]
[Disconnect the Battery]

## Testing the drone


{%
include figure
image_path="assets/images/posts/helloworld/system_overview.jpg"
alt="poster"
caption="For this tutorial, you will be using the PC Client and Crazyradio. The Mobile App can also connect to the drone."
%}


### Connecting the Crazyradio
[Connecting Crazyradio]
You will need to load the Crazyradio firmware on your PC. Please refer to the Crazyradio setup instructions.

### Drone is assembled and default firmware is booted onto drones
This tutorial begins at this point. Else this is well explained at https://www.bitcraze.io/documentation/tutorials/getting-started-with-crazyflie-2-x/.

### Turning on the crazyflie
[Turn on GIF]

### Testing a keyboard control script
This serves to check if the drone flies correctly, before applying your custom code.
The github will be up shortly.
It uses the keyboard as such:
`    def on_press(self, key):
        if key.char == 'w':
            self.mc.start_forward(self.velocity)
        if key.char == 'u':
            self.mc.take_off(0.3)
        if key.char == 's':
            self.mc.start_back(self.velocity)
        if key.char == 'a':
            self.mc.start_left(self.velocity)
        if key.char == 'd':
            self.mc.start_right(self.velocity)
        if key.char == 'c':
            self.mc.start_down(self.velocity)
        if key.char == 'z':
            self.mc.start_up(self.velocity)
        if key.char == 'l':
            print('Kill engines')
            return False
        if key.char == 'q':
            self.mc.start_turn_left(self.ang_velocity)
        if key.char == 'e':
            self.mc.start_turn_right(self.ang_velocity)
    def on_release (self, key):
        self.mc.stop()
`

## Porting your code
The github will be up shortly.
