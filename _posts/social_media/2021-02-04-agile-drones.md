---
layout: single
title: "Agile drones project"
excerpt: "Handin for the DVIC Data Visualisation Course, Dec '20."
header:
  teaser: /assets/images/posts/covid-data-viz/police.jpg
  overlay_image: /assets/images/posts/covid-data-viz/police.jpg

#categories: Project

tags:
- Data visualisation

tags:
toc: true
toc_sticky: false
date: 2021-01-17
gallery:
  - image_path: /assets/images/posts/covid-data-viz/scatter_deaths.png
    alt: " Deaths in South Africa due to Covid-19 over December 2020"
    title: "Deaths in South Africa due to Covid-19 over December 2020"


gallery2:
  - image_path: /assets/images/posts/covid-data-viz/police.jpg
    alt: "Police in the streets of Alexandra Township, made up of over 20000 informal dwellings."
    title: "Subject categories, Try 2"
  - image_path: /assets/images/posts/covid-data-viz/military_covid.jpg
    alt: "Police in the streets of "
    title: "Subject categories, Try 2"
---
Thomas Carstens and Adem Rahal, December 2020

### \#robotics, autonomous drones, control setup
### \#agility, aggressive manoeuvres research, crazyflies, optitrack
### \#building blocks, trajectory generation, trajectory following

Our specific drone configuration is saved as :
https://github.com/ThomasCarstens/feuuu_config/tree/master


This project is the longest running project in the DVIC Drone Lab. The original aim of this project was to develop a drone for the AlphaPilot autonomous drone race (1). This was a one-of-a-kind drone race in San Francisco, where teams battled autonomy algorithms on real drones. With a million dollar prize sponsored by Lockheed Martin, this race illustrates a nascent trend in the drone industry: to develop drones agile enough to race, and perhaps one day as agile as first-person-view (FPV) piloted drones. Any improvement to the drone’s agility would have an impact: to optimise fuel usage and flight times, but also, to help the drone be more agile during key split-second decisions.

# How far are we from this? A state of the art
This is a wonderful idea, and yet in practice, FPV drones have flown up to 140km/h (2) and autonomous drones reach, perhaps, 40km/h, with a more reliable speed at 15km/h (3). This is because there are many limits on drone autonomy. One is the richness of the data taken in by the drone, and processing this data can easily slow it down. The drone’s perception stack would depend on the speed of an onboard GPU, on the quality of the cameras, and particularly, on the complexity of the environment to be perceived. The drone’s battery life is limited. Another limit, and one we set out to work on, is the drone’s ability to execute its trajectories. The robotics community particularly struggles with this one, especially as onboard sensors provide a very poor measure of the drone’s position. With erratic measures of drone position, a drone will tend to deviate from its trajectory. This is why an early step for the Drone Lab was to set up a flight test platform with an external camera rig that would take care of drone localization. Once the Robotic Test Platform had been put in place (more information on the project page), the goals of the Drone Lab could finally be achieved: innovation with intelligent drones, and making sure we can test these technologies on real drones.

## Stabilisation of the Crazyflie Drone
The technologies that allow the drone to be localized, can be used by the drone itself to correct its movement. In this project, the execution of trajectories is first and foremost about making sure the drone can correct its position automatically (on the fly). For this purpose, we make use of a control loop (a negative feedback control loop). The drone could therefore fly trajectories at a few centimeters accuracy. In this project, we make sure the control architecture reaches a sufficient level of reliability. To put it into numbers, the control loop latency is now 28ms - of which 22ms due to data streaming, and 0.3ms due to the antenna.

{% include video id="2UsXnnARfos" provider="youtube" %}
[control loop video]
https://youtu.be/2UsXnnARfos

The drones now have a high level of stability. We then explore ways to fly custom trajectories. There are two approaches taken here: pre-planned trajectories, and those that are streamed… On the fly. We have tested both approaches, with a range of different figures and usecases.

## Generation of Drone Trajectories
The first approach used the drones’ python API to follow pre-planned trajectories. This is an out-of-the-box approach that we have recoded into ```dvic-demo.py``` for demo purposes at the DVIC Drone Lab. The trajectories are designed by hand in a CSV spreadsheet. They are then converted to Bezier trajectories. With this approach, we designed a spiral trajectory, a few figures of 8, a circle trajectory and more trajectories. These pre-planned trajectories were, in some cases, added in sequence, producing more complex movements. This combination of Bezier trajectories and the drones’ API yielded highly agile results, as you can see below.

{% include video id="q0Xpknpgqu4" provider="youtube" %}
[figure of 8, 2 drones]
https://youtu.be/q0Xpknpgqu4

The agility of this setup is something we decided to use further. If it were possible for the drone itself to select multiple trajectories, this would give the drones the ability to react in complex ways. We therefore created drone building blocks: slight turns and deviations. We hope this form of drone agility will be demoed in the Mixed Reality Arcade Machine project. The spiral trajectory gives an idea of a drone’s reaction to an obstacle.

{% include video id="fL43cDrySBs" provider="youtube" %}
[spiral trajectory]
https://youtu.be/fL43cDrySBs

After using the drones’ Python API for trajectory execution, it was then used for streaming a trajectory in realtime. Trajectory streaming will be particularly important for decision-making drones, but also for piloting drones in realtime. This is something we achieved in coordination with Mr Hoenig who updated his drone swarming API for this functionality (4). The distributed swarm infrastructure was adopted from an opensource project, CrazySwarm developed by USC-ACTLab (5).

{% include video id="tdrO143g21E" provider="youtube" %}
[drone piloting video]
https://www.youtube.com/watch?v=tdrO143g21E&feature=emb_logo&ab_channel=ThomasCarstens

This is fascinating during drone performances. While exploring the drone swarming API, we realised that it had been developed for testing flight algorithms, but it did not have any functionality for drones to fly together in a fully autonomous fashion. This is when we decided to build a framework ourselves for Crazyflie drones to become autonomous (a framework we then shared with the Crazyflie community at large).

At the point of writing (3 February 2020), this framework is not fully complete, but we have built in several functionalities already: see the Collective intelligence for drone swarms project. By expanding a rapidly growing swarming framework, this work has contributed to the HCI and drone research community at large.


Building on this framework, we were able to execute the trajectory building blocks in an independent fashion, guaranteeing a certain condition for autonomy: the ability to initiate and preempt trajectories at any one point in time. A first demonstration of this shows a drone switch from a straight line trajectory to flying through a waypoint. This drone has no prior knowledge of its trajectory since the action is triggered by a keypress.

{% include video id="aeuI5ycFWts" provider="youtube" %}
[drone into waypoint]
aeuI5ycFWts

# The progress so far
Looking back, we have been able to fly trajectories in increasing levels of complexity. We have achieved our goal of flying a drone autonomously to a specific position. This achievement, albeit simple in concept, was a fundamental stepping stone to developing all other projects at the DVIC. You can access these projects via the DVIC Drone Lab FrontPage (see link below). We may not have reached full autonomy. And yet, this project has enabled autonomous flight. We could say we reached the finish line.


# Special thanks
Whoenig (USC-ACTLab): for his personal assistance with the ROS to drone framework called crazyswarm, which was developed in his laboratory.

# References
(1)
(2)
(3)
(4) https://crazyswarm.readthedocs.io/en/latest/
(5)
