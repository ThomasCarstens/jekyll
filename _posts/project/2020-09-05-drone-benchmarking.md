---
layout: single
title: "Benchmarking drone flight"
excerpt: "We perform real-life demonstrations of our progress in our custom flight arena."

header.image: assets/images/posts/drone-benchmarking/wide-gates.jpg
header:
  teaser: assets/images/posts/drone-benchmarking/wide-gates.jpg
  overlay_image: assets/images/posts/drone-benchmarking/wide-gates.jpg
categories: Project

tags:
- Autonomy stack for robotics
- Python
- Motion capture
- Trajectory planning algorithms

toc: true
toc_sticky: true
date: 2019-05-31


document_path1: /assets/docs/Internship_DVIC_report_2020.pdf
---

#Benchmarking drone flight
As part of the development of the robotics cluster of the De Vinci Innovation Center, I was required set up a standardized platform for developing swarm robotics. I interned at the DVIC for 6 months, and this platform was put into service to future employees from the start of the September 2020 school year. The priority is on system security and the writing of tutorials at different levels.

###robotics, autonomous drones, control setup
###agility, aggressive manoeuvres research, crazyflies, optitrack
###building blocks, trajectory generation, trajectory following
Thomas Carstens, September 2020

## Context
This project is the longest running project in the DVIC Drone Lab. The original aim of this project was to develop a drone for the AlphaPilot autonomous drone race (1). This was a one-of-a-kind drone race in San Francisco, where teams battled autonomy algorithms on real drones. With a million dollar prize sponsored by Lockheed Martin, this race illustrates a nascent trend in the drone industry: to develop drones agile enough to race, and perhaps one day as agile as first-person-view (FPV) piloted drones. Any improvement to the drone’s agility would have an impact: to optimise fuel usage and flight times, but also, to help the drone be more agile during key split-second decisions.

This is a wonderful idea, and yet in practice, FPV drones have flown up to 140km/h (2) and autonomous drones reach, perhaps, 40km/h, with a more reliable speed at 15km/h (3). This is because there are many limits on drone autonomy. One is the richness of the data taken in by the drone, and processing this data can easily slow it down. The drone’s perception stack would depend on the speed of an onboard GPU, on the quality of the cameras, and particularly, on the complexity of the environment to be perceived. The drone’s battery life is limited. Another limit, and one we set out to work on, is the drone’s ability to execute its trajectories. The robotics community particularly struggles with this one, especially as onboard sensors provide a very poor measure of the drone’s position. With erratic measures of drone position, a drone will tend to deviate from its trajectory. This is why an early step for the Drone Lab was to set up a flight test platform with an external camera rig that would take care of drone localization. Once the Robotic Test Platform had been put in place (more information on the project page), the goals of the Drone Lab could finally be achieved: innovation with intelligent drones, and making sure we can test these technologies on real drones.

## Stabilisation of the Crazyflie Drone
The technologies that allow the drone to be localized, can be used by the drone itself to correct its movement. In this project, the execution of trajectories is first and foremost about making sure the drone can correct its position automatically (on the fly). For this purpose, we make use of a control loop (a negative feedback control loop). The drone could therefore fly trajectories at a few centimeters accuracy. In this project, we make sure the control architecture reaches a sufficient level of reliability. To put it into numbers, the control loop latency is now 28ms - of which 22ms due to data streaming, and 0.3ms due to the antenna.

From https://youtu.be/2UsXnnARfos:
{% include video id="2UsXnnARfos" provider="youtube" %}

The drones now have a high level of stability. We then explore ways to fly custom trajectories. There are two approaches taken here: pre-planned trajectories, and those that are streamed… On the fly. We have tested both approaches, with a range of different figures and usecases.

## Generation of Drone Trajectories

The first approach used the drones’ python API to follow pre-planned trajectories. This is an out-of-the-box approach that we have recoded into ```dvic-demo.py``` for demo purposes at the DVIC Drone Lab. The trajectories are designed by hand in a CSV spreadsheet. They are then converted to Bezier trajectories. With this approach, we designed a spiral trajectory, a few figures of 8, a circle trajectory and more trajectories. These pre-planned trajectories were, in some cases, added in sequence, producing more complex movements. This combination of Bezier trajectories and the drones’ API yielded highly agile results, as you can see below.

From https://youtu.be/q0Xpknpgqu4:
{% include video id="q0Xpknpgqu4" provider="youtube" %}

The agility of this setup is something we decided to use further. If it were possible for the drone itself to select multiple trajectories, this would give the drones the ability to react in complex ways. We therefore created drone building blocks: slight turns and deviations. We hope this form of drone agility will be demoed in the Mixed Reality Arcade Machine project. The spiral trajectory gives an idea of a drone’s reaction to an obstacle.

From https://youtu.be/fL43cDrySBs:
{% include video id="fL43cDrySBs" provider="youtube" %}

After using the drones’ Python API for trajectory execution, it was then used for streaming a trajectory in realtime. Trajectory streaming will be particularly important for decision-making drones, but also for piloting drones in realtime. This is something we achieved in coordination with Mr Hoenig who updated his drone swarming API for this functionality (4). The distributed swarm infrastructure was adopted from an opensource project, CrazySwarm developed by USC-ACTLab (5).

From https://youtu.be/tdrO143g21E:
{% include video id="tdrO143g21E" provider="youtube" %}

This is fascinating during drone performances. While exploring the drone swarming API, we realised that it had been developed for testing flight algorithms, but it did not have any functionality for drones to fly together in a fully autonomous fashion. This is when we decided to build a framework ourselves for Crazyflie drones to become autonomous (a framework we then shared with the Crazyflie community at large).
At the point of writing (3 February 2020), this framework is not fully complete, but we have built in several functionalities already: see the Collective intelligence for drone swarms project. By expanding a rapidly growing swarming framework, this work has contributed to the HCI and drone research community at large.

Building on this framework, we were able to execute the trajectory building blocks in an independent fashion, guaranteeing a certain condition for autonomy: the ability to initiate and preempt trajectories at any one point in time. A first demonstration of this shows a drone flying through a waypoint, directly on a keypress, with no prior knowledge of its trajectory.

From https://youtu.be/aeuI5ycFWts:
{% include video id="aeuI5ycFWts" provider="youtube" %}


## The progress so far
Looking back, we have been able to fly trajectories in increasing levels of complexity. This longstanding project has helped to develop all other projects at the DVIC. You can access these projects via the DVIC Drone Lab FrontPage (see link below). We may not have reached the autonomy we hoped for, let’s just hope we can get to the finish line.

Special thanks
Whoenig (USC-ACTLab): for his personal assistance with the ROS to drone framework called crazyswarm, which was developed in his laboratory.


## References
(1)
(2)
(3)
(4) https://crazyswarm.readthedocs.io/en/latest/
(5)
