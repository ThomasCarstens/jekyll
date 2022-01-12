---
layout: single
title: "A virtual training ground for autonomous drones"
excerpt: "Our custom hardware-in-the-loop setup for simulation testing."

header.image: assets/images/posts/virtual-training/FG-topview.jpg
header:
  teaser: assets/images/posts/virtual-training/FG-topview.jpg
  overlay_image: assets/images/posts/virtual-training/FG-topview.jpg
categories: Project
toc: true
toc_sticky: true
date: 2019-05-31

tags:
- ROS library
- Python
- Unity3D
- Motion capture
- Hardware-in-the-loop robotics

gallery:
  - image_path: assets/images/posts/virtual-training/DDA.png
    alt: "App pic 4"
    title: "Some snapshots"
  - image_path: assets/images/posts/virtual-training/robotic-platform.jpg
    alt: "App pic 3"
    title: "Some snapshots"
  - image_path: assets/images/posts/virtual-training/skirt.gif
    alt: "App pic 3"
    title: "Some snapshots"


document_path1: /assets/docs/Internship_DVIC_report_2020.pdf
---

## Drones, flight, and autonomous agents

{% include paper/testbed.html %}

{% bibliography --cited %}

What is the single element that all visions of the future since the Renaissance share? Flight. Whether it be bird wings, hot air balloons or flying cars, mankind has dreamt of flying for a long time. But now that airplanes and helicopters are a reality, is flight not a goal of technological evolution anymore? Or is it that we simply went from making man fly, to making something else fly in its stead, or alongside him. Drones are that extension of humanity, free to roam the air to recover data or visuals, to transfer loads, be used as a point in 3D space or to perform a task, in many imaginable ways.

### \#robotics, drone development, autonomous drones, control setup
### \#choose-your-environment, mixed reality, virtual drones, virtual collisions
### \#reinforcement learning, hardware-in-the-loop, research laboratory
Thomas Carstens and Matteo Frossard, December 2020

## The progress of such technologies today

These flying machines are becoming an integral part of the emerging robotic industry, and their span of applications make them an interesting asset for a lot of businesses and communities. But with those possibilities come an important challenge: how can this machine navigate their environment without human commands? They must be able not only to apprehend and know how to navigate the volumes around them, but to know how their own dynamics affect their movement, as a small angle or momentum error that would be easily corrected by a pilot could send an autonomous one into a wall or a person, causing serious harm.


Deep Drone Acrobatics, 2020, RPG Lab (2)

To solve this problem most drone labs train their drones using machine learning, allowing them to understand visible geometry through one or more cameras mounted on the drone frame, and understand not only how they fit in this space, but to correct their flight path with each image frame. But training these networks has hurdles. First we need a wealth of varied locations to help the network learn, and we need to run it with an actual drone that can and probably will crash a lot. It makes training this way a time and money consuming endeavour. Unless…

## Project Goal:
To simulate and customise an environment for drone flight
What if you could train your flying friends not using real world images but a simulated world, where moving it into another training sequence takes no more time than loading a file. Not only is it possible, MIT FastLab developed the first drone crossreality simulator in 2018 (1). In this project, we built and customise our own simulator for our personal use at the DVIC Drone Lab.

[Picture]
MIT FastLab’s FlightGoggles: a drone racing simulator with hardware-in-the-loop drones

How does it work? Your drone exists in VR. The camera feed is replaced by a simulation and so are the objects to avoid. The real drone will fly in an empty and secure training zone while reacting to obstacles on a virtual training ground. A racing drone could train dodging trees in a dense forest by a hair’s width for hours while, in reality, flying over an open field where the nearest impact hazard is 200m away. A care drone could learn to avoid running kids in a cramped room, or not crash into other vehicles when returning from a delivery. This makes sure the drone is the least possible danger for actual kids, or ruining tens of prototypes. The only downside is that, just like in regular VR, you are limited by the physical space in which your drone can fly.

## Project Process: robotic infrastructure
We set up a test and experiment environment. For our first drone experiments, we built a hardware-in-the-loop control system for Crazyflies drones, and made room for a small testing area.

[Picture]

We used the setup mentioned in the Robot Testing Platform project, and connected the Unity3D game engine. Unity is one of the most polyvalent and widely supported video game engines. As required, it is customizable and has a good power/quality render ratio. In total, this setup included Unity3D, Optitrack motion capture cameras, and ROS networking for communication between the drone, the control computer and Unity3D. All connections were made using the ROS-sharp library (3).

In a first naive approach, we transmitted the position of the drone through the ROS network into Unity3D, formatting them and updating the position of a RigidBody, to which were linked a 3D model for visualization, a Collider for, well collision detection, and a camera to simulate the one that would be placed on the drone. When testing we quickly realized the overhead time caused by the detour through ROS made the information unusable. Then, we used OptiTrack’s official plugin to get the position directly from source, and then relayed it to ROS, getting way better results for drone position.

From https://www.youtube.com/watch?v=IlaVBgHXpDU:
{% include video id="IlaVBgHXpDU" provider="youtube" %}

This successfully integrated the drone in a virtual environment. For the drone to register collisions with its environment, we then coded a state machine in ROS. This took flags from Unity to react to virtual boundaries and objects, stopping motors if the drone got close enough to catch the net, and returning to the starting position if the drone got too close to another drone. This state machine was developed to be a behaviour planner, and this is why the fuller explanation is left to the Collective intelligence for drone swarms page. The following video shows a proof of concept with a virtual collision affecting a real drone.

From https://www.youtube.com/watch?v=R65wf4Xhlqo:
{% include video id="R65wf4Xhlqo" provider="youtube" %}

The system is scalable and has shown to detect the 3 drones we currently have. The only noted limit for now is the load of rendering multiple cameras with high definition and render quality at the same time, which can slow the simulation enough to corrupt the drone’s reading of the environment. This can be solved by improving the graphics card.

## Final thoughts: a CrossReality Training Ground
By using an already set-up localization system, a free game engine and open source drones, we reached MIT’s state of the art with a platform capable of controlling and training drones without risk by feeding them a virtual environment. This project is not an innovation in itself as the system is used at the state of the art since 2018. It now gives us a powerful tool for crossing the boundary between virtual and real agents, and maybe taking a step closer to a new dream of flight, a fully autonomous one.

## Special thanks goes to:
Evgeni (école EFREI): for his path following algorithm, accessible at https://github.com/AlphaPilotFrance/adversaryBots.
Thanks to work developed at the DVIC: the Robot Testing Platform and Collective intelligence for drone swarms.

## References
(1) Winter Guerra, Ezra Tal, Varun Murali, Gilhyun Ryou, Sertac Karaman, FlightGoggles: Photorealistic Sensor Simulation for Perception-driven Robotics using Photogrammetry and Virtual Reality, arXiv preprint, 2019. URL: https://arxiv.org/abs/1905.11377
(2) Deep Drone Racing
(3) ROS-Sharp library
