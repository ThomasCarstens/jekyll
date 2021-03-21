---
layout: single
title: "Achieving more reliable drone choreographies"
excerpt: "We set up the control PC to monitor drone flight safely."

header.image: assets/images/posts/dvic_internship/internship.PNG
header:
  teaser: assets/images/posts/dvic_internship/internship.PNG
  overlay_image: assets/images/posts/dvic_internship/internship.PNG
categories: Project
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
  - image_path: /assets/images/posts/ball-launcher/shooter.jpg
    alt: "App pic 3"
    title: "Some snapshots"
gallery2:
  - image_path: /assets/images/posts/ball-launcher/frontshooter.jpg
    alt: "App pic 5"
    title: "Some snapshots"
  - image_path: /assets/images/posts/ball-launcher/base.jpg
    alt: "App pic 6"
    title: "Some snapshots"


document_path1: /assets/docs/Internship_DVIC_report_2020.pdf
---

# Achieving more reliable drone choreographies

Swarm drones are a branch of swarm robotics, or swarm robotic. The principle is to have a group of drones or robots within which each drone or robot adapts its behavior according to that of the others. One of the robots in the group can sometimes be completely useless on its own but a form of intelligence emerges when they are in sufficient numbers.
The origin of this discipline comes from a biological inspiration, social insects such as ants or bees, whose swarm is endowed with a great intelligence thanks to the cooperation between the different insects.

The advantages of swarm robotics are the low cost of producing a single robot, the easy replacement of a failed robot, and its adaptability to a varying size surface by changing the number of robots in the swarm. This technology is however still in development. To date, swarming robots can only complete tasks that are still relatively simple.
Drones in swarms, or drone fleets, are today mainly used in military or artistic fields.

###robotics, autonomous drones, control setup
###agility, aggressive manoeuvres research, crazyflies, optitrack
###building blocks, trajectory generation, trajectory following
Thomas Carstens and Bérénice Dufaure, December 2020

## Contexte

This project takes place in the DVIC drone cluster. If this cluster is still nascent when the project begins, it is now complete.
The objective of this project was to incorporate complex behaviors into the drones of the DVIC robotics platform. We wanted to be able to retrieve data related to the behavior of one or more drones to make them interact with the behavior of other drones, so that the drones can interact with each other, in swarms. Several application cases are possible, avoiding collisions between drones, defining an action perimeter for them or implementing an emergency landing for them under certain conditions, for example. The main part of the job was having to create a structure to organize the project. Indeed, behaviors that may seem simple can be very difficult and complex to translate in terms of algorithms to be incorporated on drones. On top of that, behavioral tests on drones can be costly in time and material. A drone takes time to recharge, the robotics platform takes time to set up, and a drone crash can damage it, break a propeller.
One ambition of this project is therefore also to provide a secure environment for drones, by avoiding their collisions, for example.

## Simulation

To test our algorithms, we first used a simulator. Using the simulator makes it possible to test faster, without needing to reload drones, to set them up in the arena, at a lower cost, no risk of drone crash, no broken propeller.
We turned to the TurtleSim simulator provided by the Robot Operating System (ROS) software. We used this same software to structure our code, this simulator was easy to implement for us. Even if this simulator is only in two dimensions, unlike drones which navigate in three dimensions, it allowed us to quickly experiment with the basis of different logics.
We finally implemented a SMACH state machine using ROS, linked to aROS ActionServer and the Crazyflie API.
A state machine is a structure making it possible to organize its code according to a paper diagram, one passes from one state to another according to the result of the operation associated with the state in which one finds oneself. This technology is now used in everyday devices such as elevators or traffic lights. It is also found in video games, a context in which it is often referred to as AI.

## Example of a state machine used for video games

The implementation of the state machine with ROS has been long since there are very few online resources related to ROS and SMACH and ActionServers. The use of all these technologies makes it possible to have several layers of abstraction and to more easily read the code, even if it requires learning ROS and SMACH. For a drone to perform an action, even simple, algorithms quickly become complicated and cumbersome, it was essential for us to use a structure of this type.
Here are some examples of what we were able to do with TurtleSim:

TurtleSim window, a turtle is keyboard controlled, the others are responsible for avoiding it:

From https://www.youtube.com/watch?v=igky-1YNK64:
{% include video id="igky-1YNK64" provider="youtube" %}

TurtleSim with the SMACH state machine visible on the left.

## Implementation

We then adapted our work to Crazyflies drones on the drone lab arena. We used the Crazyflie API as well as the Optitrack technology to give instructions to the drones and retrieve their positions. We use a central computer to process all the data. Crazyflies drones are indeed used in warm flights and using ROS.
We also used what has been done in agile trajectory project at the DVIC to allow drones to have precise trajectories.
The simulations we have done previously allowed us to focus on just adapting our algorithms to drones, without having to doubt the logic behind.
We were therefore able to add collision preemption between the drones, to ensure that they could not leave their space.
We've also added sphero bolts to spice up the Crazyfly drone ballet:

From https://www.youtube.com/watch?v=w8bYu9bxiII:
{% include video id="w8bYu9bxiII" provider="youtube" %}

## Conclusion

This project allows us today to have a stable structure for autonomous drones, based on a state machine. The state machine is ideal for beginners in robotics or swarm robotics, it remains a limited tool. It is necessary to implement each of the possible cases yourself, the state machine diagram may be too complex. A transition to machine learning, or machine learning, can then be considered for the future.
