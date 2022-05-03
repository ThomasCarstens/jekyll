---
layout: single
title: "Gesture Piloting: a performance analysis"
excerpt: "Testing the Performance of a custom Piloting Pipeline."

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

<style>
.img-container {
text-align: center;
}
</style><style>
.row {
margin-left:-5px;
margin-right:-5px;
}
</style><style>
.column {
float: left;
width: 50%;
padding: 5px;
}
</style><h1 id="c2">Experimentations for Human-Drone Interfaces</h1>
<h2 id="introduction">Introduction</h2>
<p>In (<span class="citation" tezza_andujar_2019"></span>), define Human-Drone Interaction (HDI) as a field of research that consists of understanding, designing and evaluating drone systems for use by humans, and in contact with humans. This field is similar to human-robot interaction (HRI), however, a drone’s unique characteristic to freely fly in a 3D space, and unprecedented shape makes human-drone interaction a research topic of its own. Researchers develop control modalities and better understand means of communicating with a drone.</p>
<p>Human-drone interaction is a broad research field, for instance, a researcher can design new drones’ shapes with friendly-like appearance, while another researcher can focus on designing new user interfaces that allow non-skilled pilots to accurately operate drones without extensive training.</p>
<p>In line with the thesis goal, we look at two types of smart systems that enhance the interactions between humans and drones. The first allows the human to pilot a drone through a gesture interface. The second looks to a virtual interface as a training ground for a real drone to avoid a virtual object. A distributed system is used to to communicate and coordinate these pipelines by passing messages to one another from any system. To better understand their tradeoffs, the distributed systems are explored and evaluated in this chapter.</p>
<h2 id="related-work">Related Work</h2>
<div class="img-container">
<p><img src="../../assets/images/hdi_fields_bw.png" style="width:6cm" alt="image" /></p>
</div>
<h3 id="exploring-more-intuitive-gesture-control">Exploring more Intuitive Gesture Control</h3>
<p>{% cite tezza_andujar_2019%}<span class="citation" data-cites="cauchard_e_zhai_landay_2015"></span> <em></em> focalise on innovative methods to interact with drones, including gesture, speech, brain-computer interfaces, and others (Figure <a href="#hdi:fields" data-reference-type="ref" data-reference="hdi:fields">[hdi:fields]</a>). As drones have different characteristics than ground robots, such as not allowing touch interaction, it is unclear whether existing techniques can be adapted to flying robots. Their user-centric design strategy seeks to understand how users naturally interact with drones.</p>
<h3 id="computer-vision-for-uav-research">Computer Vision for UAV Research</h3>
<p>With state-of-art computer vision technology, gesture-based interaction is growing and several publications are identified.</p>
<div class="margintable">
<table>
<thead>
<tr class="header">
<th style="text-align: left;"><strong>Number</strong></th>
<th style="text-align: center;"><strong>Name</strong></th>
<th style="text-align: left;"><strong>Gesture</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1</td>
<td style="text-align: center;">Help</td>
<td style="text-align: left;"><img src="../../assets/images/hdi_discussion/Help.PNG" style="width:0.5cm" alt="image" /></td>
</tr>
<tr class="even">
<td style="text-align: left;">2</td>
<td style="text-align: center;">Ok</td>
<td style="text-align: left;"><img src="../../assets/images/hdi_discussion/Ok.PNG" style="width:0.5cm" alt="image" /></td>
</tr>
<tr class="odd">
<td style="text-align: left;">3</td>
<td style="text-align: center;">Nothing</td>
<td style="text-align: left;"><img src="../../assets/images/hdi_discussion/Nothing.PNG" style="width:0.5cm" alt="image" /></td>
</tr>
<tr class="even">
<td style="text-align: left;">4</td>
<td style="text-align: center;">Peace</td>
<td style="text-align: left;"><img src="../../assets/images/hdi_discussion/Peace.PNG" style="width:0.5cm" alt="image" /></td>
</tr>
<tr class="odd">
<td style="text-align: left;">5</td>
<td style="text-align: center;">Punch</td>
<td style="text-align: left;"><img src="../../assets/images/hdi_discussion/Punch.PNG" style="width:0.5cm" alt="image" /></td>
</tr>
</tbody>
</table>
</div>
<div class="img-container">
<p><img src="../../assets/images/hdi_discussion/drone_and_me.PNG" style="width:4cm" alt="image" /></p>
</div>
<p>{% cite cauchard_e_zhai_landay_2015%}<span class="citation" data-cites="liu_szirányi_2021"></span> <em></em> contribute to an opensource database of body gestures which they test in practice with a drone (Figure <a href="#tab:rescue_dataset" data-reference-type="ref" data-reference="tab:rescue_dataset">[tab:rescue_dataset]</a>). This paper contributes with an outdoor recorded drone video dataset for action recognition, an outdoor dataset for UAV control and gesture recognition, and a dataset for object detection and tracking. These datasets are developed for emergency rescue services, which reveals how critical these applications can be.</p>
<p>{% cite liu_szirányi_2021%}<span class="citation" data-cites="gesture_interface"></span> <em></em> explores real-time vision-based Human Drone Interaction with multi-robot systems. To create a team the user focuses attention on an individual robot by simply looking at it, then adds or removes it from the current team with a motion-based hand gesture. Another gesture commands the entire team to begin task execution.</p>
<p>Compared to wearable sensor-based approaches, automated methods for video analysis based on computer vision technology are almost non-invasive. This is beneficial, and even critical, for applications in emergency rescue services.</p>
<h3 id="pose-recognition-algorithms">Pose Recognition Algorithms</h3>
<p>As a result, performance becomes application-critical for automated methods for video analysis. This, however, remains a technical challenge. According to {% cite gesture_interface%}<span class="citation" data-cites="48292"></span>, “Robust real-time hand perception is a decidedly challenging computer vision task, as body parts often occlude themselves or each other (e.g. finger/palm occlusions and handshakes) and lack high contrast patterns (e.g. between fingers).” To respond to this challenge, the Mediapipe framework {% cite 48292%}<span class="citation" data-cites="48292"></span> bases itself on a Machine Learning model, and on techniques for efficient resource management for low latency performance on CPU and GPU.</p>
<div class="img-container">
<p><img src="../../assets/images/openpose.png" style="width:6cm" alt="image" /></p>
</div>
<p>In contrast, OpenPose {% cite 48292%}<span class="citation" data-cites="liu_szirányi_2021"></span> employs a convolutional neural network to produce two heap-maps, one for predicting joint positions, and the other for partnering the joints into human skeletons. In brief, the input to OpenPose is an image and the output is the skeletons of all the people this algorithm detects. Each skeleton has 18 joints, counting head, neck, arms, and legs. Each joint position is spoken to within the image arranged with coordinate values of x and y, so there’s an add up to 36 values of each skeleton.</p>
<h3 id="mixed-reality-for-uav-research">Mixed Reality for UAV Research</h3>
<p>Simulation systems have long been an integral part of the development of robotic vehicles. They allow engineers to identify errors early on in the development process, and allow researchers to rapidly prototype and demonstrate their idea.</p>
<p>One of the first simulators that could recreate complex worlds in 3D is Gazebo, circa 2004 {% cite liu_szirányi_2021%}<span class="citation" data-cites="simulator_history"></span>. The difference between Gazebo and different 3D simulation software of that time is that Gazebo was one of the first to focus on resembling the world as realistic as possible for the robot instead of for the human. Immersive robotic simulations can be used to judge the performance of the robot and/or its concept {% cite simulator_history%}<span class="citation" data-cites="gcs_validation"></span>. In this way, simulators can increase the efficiency and decrease the costs of the development {% cite gcs_validation%}<span class="citation" data-cites="simulator_history"></span>.</p>
<p>The first published definition of Mixed Reality (MR) was given by Milgram and Kishino {% cite simulator_history%}<span class="citation" data-cites="mixed_reality"></span> as the merging of physical and virtual worlds. In their definition, Augmented Reality (AR) and Augmented Virtuality (AV) are seen as special instances of MR. In Augmented Reality, virtual objects are projected onto the physical environment, while in Augmented Virtuality, physical objects are incorporated into a virtual environment.</p>
<p>In {% cite mixed_reality%}<span class="citation" data-cites="mixed_reality_robotics"></span>, the definition of Mixed Reality is expanded to robotics by accommodating seamless interaction between physical and virtual objects in any number of physical or virtual environments. It is further demonstrated in {% cite mixed_reality_robotics%}<span class="citation" data-cites="phan_hönig_ayanian_2018"></span> that Mixed Reality can reduce the gap between simulation and implementation by enabling the prototyping of algorithms on a combination of physical and virtual objects within a single virtual environment.</p>
<div class="img-container">
<p><img src="../../assets/images/xr_sota/applications_flightmare.png" style="width:5cm" alt="image" /></p>
</div>
<p>In drone research, immersive simulators have various applications {% cite phan_hönig_ayanian_2018%}<span class="citation" data-cites="simulator_history"></span>, of which two are explored here:</p>
<ul>
<li><p><strong>Generating exteroceptive sensor data</strong>: capturing sensor feeds of the environment for one or more drones simultaneously.</p></li>
<li><p><strong>Testing navigation behaviour</strong>: Testing flight patterns subject to simulated environment stimuli, prior to real-world deployment.</p></li>
</ul>
<h3 id="generating-exteroceptive-sensor-data">Generating exteroceptive sensor data</h3>
<p>Simulation can be a huge advantage when real robot prototypes or products are not available or cannot be used due to other circumstances. During the development, simulation can be used to assess the basic hardware functionality.</p>
<p>For instance, FlightGoggles is capable of high-fidelity simulation of various types of exteroceptive sensors, such as RGB-D cameras, time-of-flight distance sensors, and infrared radiation (IR) beacon sensors. This example can be extended to multiple sensors simultaneously, leading the way to richer distributed swarm systems.</p>
<p>However, older simulators don’t provide an efficient API to access 3D information of the environment {% cite simulator_history%}<span class="citation" data-cites="flightmare"></span>. To foster research in this direction, Flightmare provides an interface to export the 3D information of the full environment (or a region of it) as point cloud with any desired resolution.</p>
<h3 id="testing-navigation-behaviour">Testing navigation behaviour</h3>
<p>Controllers evolved in simulation can be found to be inefficient once transferred onto the physical robot, remains a critical issue in robotics, referred to as the reality gap. the most efficient solutions in simulation often exploit badly modeled phenomena to achieve high fitness values with unrealistic behaviors. This gap highlights a conﬂict between the efficiency of the solutions in simulation and their transferability from simulation to reality. When deploying to real-life scenarios, there are several challenges {% cite flightmare%}<span class="citation" data-cites="drl_review"></span>:</p>
<ul>
<li><p>Optimising the flight control of a UAV. This is relevant with changing payloads, unexpected weather conditions (dust, rain, changing wind), as well as preventive maintenance (motor degradation, battery damage).</p></li>
<li><p>Optimising the flight path of a UAV. Several sensor inputs can inform the drone’s flight path and flight speed. This gives several ways to optimise the data acquisition process, from more complex data intakes and various activation/triggering optimisations.</p></li>
</ul>
<p>Prior to real-world deployments, different functional elements on a robot can be tested in parallel and reduce development time. For instance, the algorithms for localization, motion planning or control can be tested, improved, and integrated continuously. There are various artificial intelligence algorithms concerned with the thematic of guidance, navigation and control (GNC). A subset of these algorithms is explored in, pertaining to Deep Reinforcement Learning (DRL). These techniques can improve the drone operation as shown in Table <a href="#tab:RL_applications" data-reference-type="ref" data-reference="tab:RL_applications">[tab:RL_applications]</a>.</p>
<div class="table*">
<table>
<thead>
<tr class="header">
<th style="text-align: left;"><strong>Task</strong></th>
<th style="text-align: center;"><strong>Input Observations</strong></th>
<th style="text-align: left;"><strong>Output Actions</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1. Quadrotor control</td>
<td style="text-align: center;">[<span class="math inline"><em>p</em>, <em>θ</em>, <em>v</em></span>], dim=10</td>
<td style="text-align: left;">[<span class="math inline"><em>c</em>, <em>ω</em><sub><em>x</em></sub>, <em>ω</em><sub><em>y</em></sub>, <em>ω</em><sub><em>z</em></sub></span>]], dim=4</td>
</tr>
<tr class="even">
<td style="text-align: left;">2. Control under motor failure</td>
<td style="text-align: center;">[<span class="math inline"><em>p</em>, <em>θ</em>, <em>v</em>, <em>ω</em></span>], dim=12</td>
<td style="text-align: left;">[<span class="math inline"><em>f</em><sub>1</sub>, <em>f</em><sub>2</sub>, <em>f</em><sub>3</sub></span>], dim=3</td>
</tr>
<tr class="odd">
<td style="text-align: left;">3. Flying through a gate</td>
<td style="text-align: center;">[<span class="math inline"><em>p</em>, <em>θ</em>, <em>v</em>, <em>ω</em>, <em>p</em><sub><em>g</em><em>a</em><em>t</em><em>e</em></sub>, <em>θ</em><sub><em>g</em><em>a</em><em>t</em><em>e</em></sub></span>], dim=18</td>
<td style="text-align: left;">[<span class="math inline"><em>f</em><sub>1</sub>, <em>f</em><sub>2</sub>, <em>f</em><sub>3</sub>, <em>f</em><sub>4</sub></span>], dim=4</td>
</tr>
</tbody>
</table>
</div>
<p>Current research of drone quadrotor control employs newly architected neural networks and learning time-optimal controllers for drone racing {% cite drl_review%}<span class="citation" data-cites="drl_review"></span>. This element is largely figured in Flightmare’s {% cite drl_review%}<span class="citation" data-cites="flightmare"></span> simulation usecases, and echoes the state of the art research in Reinforcement Learning for UAVs {% cite flightmare%}<span class="citation" data-cites="drl_review"></span>, suggesting that new RL implementations can optimising the flight stability of a UAV as well as new perception pipelines for the navigation of a UAV. Flightmare offers convenient wrappers for reinforcement learning. Those gym wrappers give researchers a user-friendly interface for the interaction between Flightmare and existing RL baselines designed around the gym interface.</p>
<h2 id="section:gesture_piloting">Drone Piloting With Gesture</h2>
<p>Gestures are the most natural way for people to express information in a non-verbal way. Users can simply control devices or interact without physically touching them. Nowadays, such types of control can be found from smart TV to surgery robots, and UAVs are not the exception.</p>
<div class="img-container">
<p><img src="../../assets/images/intro/step2_diagram.png" style="width:5cm" alt="image" /></p>
</div>
<p>Drone piloting and other control modalities {% cite drl_review%}<span class="citation" data-cites="tezza_andujar_2019"></span> make use of various inputs to assist in flight. Perception modules for drone flight usually consist of data-driven models based on multiple sensor modalities. These inputs can be sensor modalities, such as camera, lidar, and radar, published in autonomous-driving related datasets, but also human commands, in the case on drone piloting. In this way, perception pipelines are routinely developed as a realtime interface for sensor data from multiple perception configurations.</p>
<p>As of , multiple gesture interfaces have been developed for UAVs {% cite tezza_andujar_2019%}<span class="citation" data-cites="liu_szirányi_2021"></span> {% cite liu_szirányi_2021%}<span class="citation" data-cites="gesture_interface"></span>, but are lacking in drone piloting. Realtime interfaces for drone piloting are discouraged {% cite gesture_interface%}<span class="citation" data-cites="tezza_andujar_2019"></span> due to high latency and low control precision compared to other drone control modalities. As of , the literature utilizing the Crazyflie nanodrone does not include realtime streaming commands {% cite tezza_andujar_2019%}<span class="citation" data-cites="crazyflie_research"></span>.</p>
<h3 id="overview-of-pipeline">Overview of Pipeline</h3>
<p>A pipeline is implemented to ensure that the right gesture is associated to the right drone command, in real-time and continuously. This pipeline is conceptualised as in Figure <a href="#fig:handpipeline" data-reference-type="ref" data-reference="fig:handpipeline">[fig:handpipeline]</a>.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/gesture_pipeline.png" style="width:11cm" alt="image" /></p>
</div>
<p>The Testbed of Chapter <a href="#c1" data-reference-type="ref" data-reference="c1">[c1]</a> offers a working environment, as well as a command streaming interface between a drone and a companion computer. The focus is therefore on the two first elements: a gesture recognition workflow, followed by a drone control workflow.</p>
<h3 id="gesture-recognition-layer">Gesture Recognition Layer</h3>
<p>In this project, we employ a <strong>3D Pose Estimator</strong>, described in the following section, followed by a <strong>Gesture Classification</strong> Script.</p>
<div class="img-container">
<p><img src="../../assets/images/hca.png" style="width:11cm" alt="image" /></p>
</div>
<h4 id="machine-learning-3d-pose-estimation">Machine Learning 3D Pose Estimation</h4>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/hdi_bookmark1.png" style="width:3cm" alt="image" /></p>
</div>
<p>MediaPipe Hands {% cite crazyflie_research%}<span class="citation" data-cites="48292"></span> is a high-fidelity hand and finger tracking solution. It employs machine learning (ML) to infer 21 landmarks of a hand from just a single video frame.</p>
<div class="img-container">
<p><img src="../../assets/images/hand_landmarks.png" style="width:10cm" alt="image" /></p>
</div>
<p>Precise key-point localization of 21 3D hand-knuckle coordinates remain inside the detected hand regions. This allows us to have the spatial position of each of the joints of a hand using only a normal camera.</p>
<p>Whereas current state-of-the-art approaches rely primarily on powerful desktop environments for inference {% cite 48292%}<span class="citation" data-cites="liu_szirányi_2021"></span>, MediaPipe Hands achieves real-time performance on a mobile phone, and even scales to multiple hands, making it an ideal solution for real-time pose tracking.</p>
<p>The desired gesture is hardcoded by its absolute position. For example, if Figure 1’s landmark 8 is below the landmark 5, it can be interpreted as closing your index.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/hdi_bookmark2.png" style="width:3cm" alt="image" /></p>
</div>
<h4 id="gesture-classification-script">Gesture Classification Script</h4>
<div class="img-container">
<p><img src="../../assets/images/hand_drone_interaction/up_censored.jpg" style="width:3.5cm" alt="image" /> <img src="../../assets/images/hand_drone_interaction/fist_censored.png" style="width:3.5cm" alt="image" /> <img src="../../assets/images/hand_drone_interaction/peace_censored.jpg" style="width:3.5cm" alt="image" /></p>
</div>
<p>While the model is precise in landmark detection, there are false detections of gestures due to marginal cases. A special buffer is used to filter the most frequent gesture on a sliding window (for every 10 detections). This helps to remove glitches or inconsistent recognition.</p>
<h3 id="drone-control-layer">Drone Control Layer</h3>
<p>Using a live gesture recognition module, a system is designed for streaming commands to be sent to the drone.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/gesture_pipeline1.png" style="width:11cm" alt="image" /></p>
</div>
<p>Note that the critical information flow between the components of the system is unidirectional. Bidirectional communication, e.g. telemetry from the vehicles, is supported, but is not required for controlled operation. All communication is done in a distributed, one-way manner, such that the gesture recognition workflow is not affected by the drone listener and there is no reliance on high-level code to keep track of the various components, preventing unnecessary interdependence. The Gesture-to-Command script decrypts the messages encoded into a custom ROS message. This workflow serves as a fallback during experiments and demonstrations.</p>
<h4 id="message-passing-between-applications">Message passing between applications</h4>
<p>The following message is passed via a ROS topic (TCP/IP message). It is then depacketized upon arrival.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/msg_structure.png" style="width:10cm" alt="image" /></p>
</div>
<h4 id="mode-selection">Mode Selection</h4>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/gesture_pipeline2.png" style="width:5.5cm" alt="image" /></p>
</div>
<p>The following element in the drone control layer is the selection of an adequate mode.</p>
<ul>
<li><p>Flight Mode 1: Position Update Mode. This mode moves the drone translationally in three axes based on an absolute position.</p></li>
<li><p>Flight Mode 2: Velocity Update Mode. This mode moves the drone according to inputted velocities.</p></li>
</ul>
<p>In each mode, the drone can move up, down, left or right. The following hand gestures are associated with these directions.</p>
<div class="img-container">
<p><img src="../../assets/images/hand_drone_interaction/pose_association_white.png" style="width:11cm" alt="image" /></p>
</div>
<h4 id="velocity-filter">Velocity Filter</h4>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/gesture_pipeline3.png" style="width:5.5cm" alt="image" /></p>
</div>
<p>The velocity filter serves as a safety measure during development and demonstrations. Given a drone’s position in the Flight Arena, it attributes a particular value between 0 and 1. This value is then multiplied to the velocity value determined from the gesture movement.</p>
<p>The shape of this Velocity Filter was defined using an ellipsoid, with a near constant velocity within the ellipsoid and a sigmoid on the boundaries of this shape. An initial volume is designed on <a href="#equation:ellipsoid" data-reference-type="ref" data-reference="equation:ellipsoid">[equation:ellipsoid]</a>.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/velocity_1_crop2.png" style="width:3cm" alt="image" /></p>
</div>
<p><span class="math display">$$A_{1} = \frac{x^2}{a^2} +\frac{y^2}{b^2} +\frac{z^2}{c^2} \text{ with } (a, b, c) = (1.35, 0.85, 1.1)
    \label{equation:ellipsoid}$$</span></p>
<p>This figure is scaled according to constants (a, b, c). They are determined empirically by measuring the furthest distance measured by the motion capture. This ellipsoid is then transformed to better approximate the required filter.</p>
<p><span class="math display"><em>A</em><sub>2</sub> = <em>α</em> * ((1−<em>A</em><sub>1</sub>)−<em>β</em>) with (<em>α</em>,<em>β</em>) = (18,0.3)</span></p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/velocity_2_crop.png" style="width:3cm" alt="image" /></p>
</div>
<p>The volume is scaled up by <span class="math inline"><em>α</em></span> and shifted down by <span class="math inline"><em>β</em></span>. Determining the <span class="math inline"><em>α</em></span> and <span class="math inline"><em>β</em></span> scaling parameters, leading to the shape in Figure <a href="#fig:vel2" data-reference-type="ref" data-reference="fig:vel2">[fig:vel2]</a>.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/velocity_3_crop.png" style="width:3cm" alt="image" /></p>
</div>
<p><span class="math display">$$A_{3} = \frac{1}{1+e^{-A_{2}}}
    \label{equation:sigmoid}$$</span></p>
<p>A logistic regression allows for a smooth speed transition at the limits of this volume.</p>
<h4 id="gesture-speed-and-angle">Gesture Speed and Angle</h4>
<div class="img-container">
<p><img src="../../assets/images/hdi_system/gesture_pipeline4.png" style="width:5.5cm" alt="image" /></p>
</div>
<p>Hand movement is separated into angle and speed. As the hand moves in a specific direction on the screen, the components of that vector can be used to calculated the speed and angle of the drone’s movement. To help smoothen the output velocity, the mean pixel distance is taken over a rolling window.</p>
<div class="img-container">
<p><img src="../../assets/images/hand_drone_interaction/grab_down_censored.jpg" style="width:3.5cm" alt="image" /> <img src="../../assets/images/hand_drone_interaction/grab_up_fast_censored.jpg" style="width:3.5cm" alt="image" /> <img src="../../assets/images/hand_drone_interaction/grab_up_slow_censored.jpg" style="width:3.5cm" alt="image" /></p>
</div>
<p>Using these key landmarks, it is possible to discern hand poses and develop a library of drone-piloting hand signals. These are programmed accordingly in the Experimentation Section.</p>
<h3 id="performance-analysis">Performance Analysis</h3>
<h4 id="aim">Aim</h4>
<p>We put in place a demonstration for flight piloting in real-time using the developed gesture interface. We present the workflow of real-time gesture piloting pipeline and we evaluate it in terms of:</p>
<ul>
<li><p>System response time</p></li>
<li><p>Accuracy of gesture recognition</p></li>
</ul>
<h4 id="evaluation-techniques">Evaluation Techniques</h4>
<div class="img-container">
<p><img src="../../assets/images/intro/step2_diagram.png" style="width:5cm" alt="image" /></p>
</div>
<p><em>System Response Time</em><br />
The system response time is verified by applying a series of rapid maneuvers to register any significant delays between the pilot’s commands and their execution by the flight control system. Similarly, {% cite liu_szirányi_2021%}<span class="citation" data-cites="experimental_tuning"></span> choose to modify the drone’s angle in a specified direction. This choice is arbitrary and the changes in velocity are used in this case.The input was a demanded velocity in a specified direction. The input was changed randomly by the operator with hand movements, using the workflow described in this chapter. The output was a delay of the velocity change in the drone. Finally, a system response time is determined by averaging the response delays over the experiment.</p>
<p><em>Gesture Recognition Effectiveness</em><br />
In order to evaluate gesture recognition performance, we identify the false positive and negative rates of the pose detection, to compare with existing research in real-time gesture detection. In comparison, {% cite experimental_tuning%}<span class="citation" data-cites="bolin_crawford_macke_hoffman_beckmann_sen_2017"></span> evaluates the false positive and negative rates of the pose detection by manually identifying both the incorrectly recognised gestures, and the unrecognised gestures. Similarly, we identify the false positive and negative rates of the pose detection, but instead of doing it manually, we examine any discrepancies in the UAV’s trajectory flight. Any inconsistencies in recognition are considered false positives.</p>
<h4 id="methodology-for-piloting-operation">Methodology for Piloting Operation</h4>
<p>We design our experiments for an operator to guide the drone in an intuitive way through hand commands.</p>
<div class="img-container">
<p><img src="../../assets/images/Signal_Mode.JPG" style="width:5cm" alt="image" /></p>
</div>
<p><em>Dataset</em> The experiment was filmed from three angles, and a presentation video is uploaded on Youtube {% cite bolin_crawford_macke_hoffman_beckmann_sen_2017%}<span class="citation" data-cites="piloting_video"></span>. The results were saved in a rosbag format on Google Drive {% cite piloting_video%}<span class="citation" data-cites="piloting_data"></span>. The data that is examined extends from 11:19:20 to 11:20:30 on July 29, 2021.</p>
<p>Throughout this procedure, data is collected as a rosbag, a self-contained file for recording ROS nodes and topics. In post-processing, we timestamp the hand signal stream. This file is available at {% cite piloting_data%}<span class="citation" data-cites="piloting_data"></span> and contains:</p>
<ul>
<li><p>The poses of the drone, ordered by timestamp: /tf topic.</p></li>
<li><p>The hand gesture message contents: /hand_signal topic.</p></li>
</ul>
<h4 id="results">Results</h4>
<p><strong>Overview of Results</strong> The two flight regions were plotted separately. The trajectory is plotted on 3 planes. The drone’s trajectory is first plotted on the X-Z plane (as per Figure <a href="#fig:refframe1" data-reference-type="ref" data-reference="fig:refframe1">[fig:refframe1]</a>). The two flight regions are separated by locating the transition gesture’s timestamp.</p>
<div class="img-container">
<p><img src="../../assets/images/coordinates.png" style="width:3cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/Piloting_Frontview.png" style="width:11cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/Piloting_Topview.png" style="height:3.1cm" alt="image" /> <img src="../../assets/images/hdi_graphs/piloting_3dview3.png" style="height:4cm" alt="image" /><br />
<img src="../../assets/images/hdi_graphs/Piloting_Frontview.png" style="height:3cm" alt="image" /> <img src="../../assets/images/hdi_graphs/Piloting_Sideview.png" style="height:3cm" alt="image" /></p>
</div>
<p><strong>Gesture Recognition Effectiveness</strong> In preparation for this evaluation, we label the drone positions where each hand signal is detected. Figure <a href="#fig:command_labels" data-reference-type="ref" data-reference="fig:command_labels">[fig:command_labels]</a> superposes the drone’s trajectory and the hand gestures identified at that particular point on the drone’s path.</p>
<p><strong>Flight Timeline with Annotated Hand Signs</strong></p>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/position_mode_gestures.png" style="width:9cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/Position_update_mode.png" style="width:9cm" alt="image" /></p>
</div>
<p>The detection of hand gestures is found to be mostly continuous. Using the methodology outlined earlier, the false positive and false negative rates can be determined.</p>
<div class="table*">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Criteria</th>
<th style="text-align: center;">RIGHT</th>
<th style="text-align: center;">LEFT</th>
<th style="text-align: center;">UP</th>
<th style="text-align: center;">DOWN</th>
<th style="text-align: left;">THUMBUP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">len</td>
<td style="text-align: center;">342</td>
<td style="text-align: center;">280</td>
<td style="text-align: center;">150</td>
<td style="text-align: center;">87</td>
<td style="text-align: left;">201</td>
</tr>
<tr class="even">
<td style="text-align: left;">False Positives</td>
<td style="text-align: center;">5</td>
<td style="text-align: center;">33</td>
<td style="text-align: center;">3</td>
<td style="text-align: center;">6</td>
<td style="text-align: left;">201</td>
</tr>
<tr class="odd">
<td style="text-align: left;">False Negatives</td>
<td style="text-align: center;">30</td>
<td style="text-align: center;">175</td>
<td style="text-align: center;">10</td>
<td style="text-align: center;">5</td>
<td style="text-align: left;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">Accuracy (% correct)</td>
<td style="text-align: center;">89.7</td>
<td style="text-align: center;">25.7</td>
<td style="text-align: center;">93.33</td>
<td style="text-align: center;">87.35</td>
<td style="text-align: left;">0</td>
</tr>
</tbody>
</table>
</div>
<div class="table*">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Criteria</th>
<th style="text-align: center;">INDEX</th>
<th style="text-align: center;">PEACE</th>
<th style="text-align: center;">THUMBDOWN</th>
<th style="text-align: left;">TOTAL</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">len</td>
<td style="text-align: center;">192</td>
<td style="text-align: center;">131</td>
<td style="text-align: center;">100</td>
<td style="text-align: left;">1483</td>
</tr>
<tr class="even">
<td style="text-align: left;">False Positives</td>
<td style="text-align: center;">15</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">100</td>
<td style="text-align: left;">369</td>
</tr>
<tr class="odd">
<td style="text-align: left;">False Negatives</td>
<td style="text-align: center;">23</td>
<td style="text-align: center;">36</td>
<td style="text-align: center;">0</td>
<td style="text-align: left;">299</td>
</tr>
<tr class="even">
<td style="text-align: left;">Accuracy (% correct)</td>
<td style="text-align: center;">80.2</td>
<td style="text-align: center;">67.94</td>
<td style="text-align: center;">0</td>
<td style="text-align: left;">56.3</td>
</tr>
</tbody>
</table>
</div>
<p>Looking at the graphs, it seems that left and down gestures are quite regularly mistaken for one another. In contrast, gestures are different enough (such as right and index) are recognised at 90%.This demonstrates an interesting limitation in the pipeline’s design: the recognition seems stumble between two similar gestures.</p>
<p>The effectiveness is averaged as the total percentage of correct gestures over the full dataset. The accuracy is determined as of the full gesture dataset.</p>
<p><strong>System Response Time</strong> In preparation for this evaluation, we to plot the speeds at which the poses are streamed, as well as the desired speed transmitted from the gesture script. The velocities of the actual drone are calculated as per Equation <a href="#eq:speeds" data-reference-type="ref" data-reference="eq:speeds">[eq:speeds]</a> from successive pose data points over the period of interest.</p>
<p><span class="math display"><em>Δ</em><sub><em>x</em></sub> = <em>x</em><sub><em>f</em></sub> − <em>x</em><sub><em>i</em></sub> and similarly for <em>Δ</em><sub><em>y</em></sub>, <em>Δ</em><sub><em>z</em></sub></span></p>
<p><span class="math display">$$v^* = \frac{\delta u}{\delta t} = \frac{\sqrt{\Delta_{x}^2 + \Delta_{y}^2 + \Delta_{z}^2}}{t_f - t_i}
    \label{eq:speeds}$$</span> This calculation is a simplification given the pose data has a stable <span class="math inline">120 ± 0.4</span> Hz transmission frequency, which is ascertained during the experiment (Figure <a href="#fig:frequency_check" data-reference-type="ref" data-reference="fig:frequency_check">[fig:frequency_check]</a>).</p>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/freq_hdiC.png" style="width:8cm" alt="image" /></p>
</div>
<p>Figure <a href="#fig:velocities" data-reference-type="ref" data-reference="fig:velocities">[fig:velocities]</a> plots the drone’s position and its associated velocity in Position Update Mode (<strong>blue</strong>) followed by Velocity Update Mode (<strong>red</strong>).</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/actual_velocities.png" style="width:10cm" alt="image" /></p>
</div>
<p>The red graph is significantly more jaggered. This is expected since the velocity updates depend on fast moving hand movements. In Figure <a href="#fig:responsiveness" data-reference-type="ref" data-reference="fig:responsiveness">[fig:responsiveness]</a>, we take a closer look at the interactions between a drone’s trajectory and the signs identified at that particular instance. The velocity commands (in <strong>green</strong>) are plotted alongside the drone responses (<strong>red</strong>).</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/desired_velocities.png" style="width:10cm" alt="image" /></p>
</div>
<p>The system response time is determined from Figure <a href="#fig:responsiveness" data-reference-type="ref" data-reference="fig:responsiveness">[fig:responsiveness]</a> by locating specific spikes of velocity change, in the velocity command stream, and locating spikes of velocity change in the drone flight stream. Their timestamps are recorded in Table <a href="#tab:velocity_latency" data-reference-type="ref" data-reference="tab:velocity_latency">[tab:velocity_latency]</a>.</p>
<div class="table*">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Points</th>
<th style="text-align: center;">1</th>
<th style="text-align: center;">2</th>
<th style="text-align: center;">3</th>
<th style="text-align: center;">4</th>
<th style="text-align: left;">5</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Velocity Command</td>
<td style="text-align: center;">19.49.636</td>
<td style="text-align: center;">19.50.2053</td>
<td style="text-align: center;">50.4723</td>
<td style="text-align: center;">51.3419</td>
<td style="text-align: left;">52.2437</td>
</tr>
<tr class="even">
<td style="text-align: left;">Velocity Response</td>
<td style="text-align: center;">19.9789</td>
<td style="text-align: center;">19.568</td>
<td style="text-align: center;">50.728</td>
<td style="text-align: center;">51.6482</td>
<td style="text-align: left;">52.5579</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Duration of Latency</td>
<td style="text-align: center;">342.9</td>
<td style="text-align: center;">362.7</td>
<td style="text-align: center;">255.7</td>
<td style="text-align: center;">306.3</td>
<td style="text-align: left;">314.2</td>
</tr>
</tbody>
</table>
</div>
<div class="table*">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Points</th>
<th style="text-align: center;">6</th>
<th style="text-align: center;">7</th>
<th style="text-align: center;">8</th>
<th style="text-align: center;">9</th>
<th style="text-align: left;">10</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Velocity Command</td>
<td style="text-align: center;">53.753</td>
<td style="text-align: center;">54.7583</td>
<td style="text-align: center;">55.3996</td>
<td style="text-align: center;">56.4005</td>
<td style="text-align: left;">57.6692</td>
</tr>
<tr class="even">
<td style="text-align: left;">Velocity Response</td>
<td style="text-align: center;">53.9478</td>
<td style="text-align: center;">54.898</td>
<td style="text-align: center;">55.6579</td>
<td style="text-align: center;">56.6375</td>
<td style="text-align: left;">57.9679</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Duration of Latency</td>
<td style="text-align: center;">194.8</td>
<td style="text-align: center;">139.7</td>
<td style="text-align: center;">258.3</td>
<td style="text-align: center;">237.0</td>
<td style="text-align: left;">298.7</td>
</tr>
</tbody>
</table>
</div>
<p>The average latency is found to be from the average latency of 10 points. This latency remains rather consistently between 200 and 300 ms, which demonstrates stability over time. We can perform a cross-validation this result with a visual check: we superpose the graphs by eye to determine an approximate value (Figure <a href="#fig:response_shift" data-reference-type="ref" data-reference="fig:response_shift">[fig:response_shift]</a>).</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/velocity_adapted.png" style="width:11cm" alt="image" /></p>
</div>
<p>To create this superposition, we shift the second graph by a difference of 250ms. This agrees with the experimental latency of 200-300ms.</p>
<h3 id="discussion">Discussion</h3>
<div class="img-container">
<p><img src="../../assets/images/DSCF0871.jpg" style="width:5cm" alt="image" /></p>
</div>
<p>While Chang Liu et al. focus on outdoor datasets for single large drones, this work looks towards interacting specifically on the drone’s position. Such a specific usecase of hand-following seems to be relatively rare in the literature. In fact, Tezza et al. {% cite piloting_data%}<span class="citation" data-cites="tezza_andujar_2019"></span>, despite their survey of the research field, remain sceptical as to whether this method might be the best approach to applications that require fine and precise control, as they pose the problems of higher latency and lower accuracy than other methods such as a remote controller. This vision is coerced with other members of the HDI community, and most datasets focus rather on signaling events to the drone, instead of direct piloting (Figure <a href="#tab:rescue_dataset" data-reference-type="ref" data-reference="tab:rescue_dataset">[tab:rescue_dataset]</a> from {% cite tezza_andujar_2019%}<span class="citation" data-cites="liu_szirányi_2021"></span>). .</p>
<div class="margintable">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Model</th>
<th style="text-align: center;">Pixel 3</th>
<th style="text-align: center;">Samsung S20</th>
<th style="text-align: center;">iPhone11</th>
<th style="text-align: center;"></th>
<th style="text-align: left;"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Light</td>
<td style="text-align: center;">6.6</td>
<td style="text-align: center;">5.6</td>
<td style="text-align: center;">1.1</td>
<td style="text-align: center;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Full</td>
<td style="text-align: center;">16.1</td>
<td style="text-align: center;">11.1</td>
<td style="text-align: center;">5.3</td>
<td style="text-align: center;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Heavy</td>
<td style="text-align: center;">36.9</td>
<td style="text-align: center;">25.8</td>
<td style="text-align: center;">7.5</td>
<td style="text-align: center;"></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
</div>
<p>This performance analysis has measured the pipeline latency is evaluated at 270ms. This is in large part thanks to MediaPipe Hands algorithm {% cite liu_szirányi_2021%}<span class="citation" data-cites="48292"></span>. This algorithm is relatively new, and demonstrates real-time inference capabilities, with a maximum inference of 36ms for hand landmarks (as shown in Figure <a href="#fig:mediapipe_alone" data-reference-type="ref" data-reference="fig:mediapipe_alone">[fig:mediapipe_alone]</a>). This performance is evidently far different from that of the perception pipeline developed here around the Mediapipe framework, with different equipment.</p>
<p>This experiment has offered a way to approach hand-drone interaction. Other approaches can offer a fuller exploration of the operator’s ease in controlling the drone, by examining the frequency at which different hand signals are used. As the operator controls the drone by sight, it is possible for them to make minute readjustments. As a result, further research could examine the role of intuition within this gesture loop. It might also be possible to explore instances where the operator does not look at the drone. Without visual feedback, this could give better hints as to the controller’s effectiveness subject to clear hand commands.</p>
<h4 id="regarding-the-thesis">Regarding the Thesis</h4>
<div class="img-container">
<p><img src="../../assets/images/hdi_discussion/drone_and_me.PNG" style="width:5cm" alt="image" /></p>
</div>
<p>In creating better service drones, one might wonder if a piloting system is an effective means to research and development. It could easily help manage swarms of drones, but is drone development the type of research that requires the operator to make split-second decisions? After all, certain tasks require split-second reactions: drones doing free-fall recovery for instance. Perhaps it could be the beginning of an era of drone real-time learning, where drones can develop functionalities more rapidly than before, through kinetic means. Figure <a href="#fig:selfie" data-reference-type="ref" data-reference="fig:selfie">[fig:selfie]</a> is taken from the DJI website, and shows a gesture instruction for a drone to take a picture. Perhaps functionalities like this can become more natural, more closely coupled with human behaviour.</p>
<h3 id="summary">Summary</h3>
<p>The gesture interface used to pilot the drones is given 56% accuracy. While the pipeline is based on MediaPipe Hands, the pose classification was hardcoded, and the software can then be improved with a neural classifier or an ML pipeline. In practice, the errors were filtered out by the drone control pipeline.</p>
<h2 id="section:xreality">Mixed Reality Interface</h2>
<div class="img-container">
<p><img src="../../assets/images/xr_system/xr_topview_margin.jpg" style="width:4cm" alt="image" /></p>
</div>
<p>Drone piloting and other control modalities {% cite 48292%}<span class="citation" data-cites="tezza_andujar_2019"></span> make use of various inputs to assist in flight. Perception modules for drone flight usually consist of data-driven models based on multiple sensor modalities. These inputs can be sensor modalities, such as camera, lidar, and radar, published in autonomous-driving related datasets, but also human commands, in the case on drone piloting. In this way, perception pipelines are routinely developed as a realtime interface for sensor data from multiple perception configurations.</p>
<p>A mixed reality interface serves to enable data transmission between a physical drone and its virtual equivalent. This section documents the design of a mixed reality environment (Figure <a href="#fig:reality_interface" data-reference-type="ref" data-reference="fig:reality_interface">[fig:reality_interface]</a>). The first objective of the simulated environment is to serve as a graphical interface in order to develop tasks otherwise too difficult to deploy. The priority of the virtual reality is therefore set on rendering capabilities, and the ability to obtain camera streams from this environment.</p>
<h3 id="selected-modules-and-technologies">Selected modules and technologies</h3>
<p>This section is a brief mention of all the platforms, systems, services, and processes this interface depends on.</p>
<ul>
<li><p>Unity3D {% cite tezza_andujar_2019%}<span class="citation" data-cites="unity3d"></span> is a popular game engine which offers a simulated environment. It is set up as the virtual companion to the Flight Arena. Unity is well suited since it enables high-fidelity graphical rendering, including realistic pre-baked or real-time lighting, flexible combinations of different meshes, materials, shaders, and textures for 3D objects, skyboxes for generating realistic ambient lighting in the scene, and camera post-processing {% cite unity3d%}<span class="citation" data-cites="flightmare"></span>.</p></li>
<li><p>ROS Sharp {% cite flightmare%}<span class="citation" data-cites="rossharp"></span> is a set of open source software libraries and tools in C# for communicating with ROS from .NET applications, in particular Unity.</p></li>
<li><p>ROS {% cite rossharp%}<span class="citation" data-cites="ros"></span> is a set of software libraries and tools that assist in building robot applications.</p></li>
</ul>
<p>For the sake of replicability, the version of each module is documented in the references.</p>
<h3 id="conceptual-overview">Conceptual Overview</h3>
<p>The link between the real and the mixed reality is designed with the following core capabilities:</p>
<ul>
<li><p>Transmitting the <strong>pose of a real drone</strong> into a virtual environment.</p></li>
<li><p>Transmitting <strong>an event</strong> between the physical and the virtual environment.</p></li>
</ul>
<p>For instance, a drone collision with a virtual object would have the following workflow (Figure <a href="#proposed_workflow" data-reference-type="ref" data-reference="proposed_workflow">[proposed_workflow]</a>).</p>
<div class="img-container">
<p><img src="../../assets/images/xr_system/collision_workflow.png" style="width:11cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/xr_pres.png" style="width:5.5cm" alt="image" /></p>
</div>
<p>The process of transmitting the pose of the drone to the simulator is referred to as <strong>pose injection</strong>. This is done via the Network interface, from ROS to the simulator. The process of collision occurs in the simulator, between the injected pose, and a virtual body. This is done via a collision interface within Unity.</p>
<p>These two elements can be readapted to a variety of event-driven scenarios. For this reason, a mixed reality setup offers inexhaustive resources to drone development.</p>
<h3 id="overview-of-system-network-interfaces">Overview of System Network Interfaces</h3>
<p>In order to establish a two-way mixed reality interface, the simulator and the robotics backend are configured to communicate to each other.</p>
<div class="img-container">
<p><img src="../../assets/images/xr_system/xr_overview.png" style="width:8cm" alt="image" /></p>
</div>
<p>To return to the System Network Layout (Chapter <a href="#c1" data-reference-type="ref" data-reference="c1">[c1]</a>, Figure <a href="#fig:network_reference" data-reference-type="ref" data-reference="fig:network_reference">[fig:network_reference]</a>), the Mixed Reality Interface involves Unity3D as well as the Task Manager.</p>
<h3 id="event-sharing-workflow">Event Sharing Workflow</h3>
<h4 id="a-network-interface-for-mixed-reality-event-sharing">A Network Interface for Mixed Reality Event Sharing</h4>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/collision_process1.png" style="width:5cm" alt="image" /></p>
</div>
<p>A Network Interface is used for the two objectives: injecting pose messages into the game engine and retrieving event data to be sent to the ROS Task Manager.</p>
<h4 id="collision-detection-in-the-virtual-environment">Collision Detection in the Virtual Environment</h4>
<p>The virtual environment is a Virtual Arena. A particularity of this arena is that it is 3 times larger than the actual flight arena. In other words, the drone’s recorded position differs from the real arena by a factor of 3, and the drone’s velocity also differs by 3. The two agents are also embodied by virtual characters, annotated as 1 and 2 in the visual below. Video feeds (Figure <a href="#fig:video_feed" data-reference-type="ref" data-reference="fig:video_feed">[fig:video_feed]</a>) show the perspectives of both agents, and these are recorded as part of the experiment.</p>
<h4 id="an-event-stream-using-this-network-interface">An Event Stream Using this Network Interface</h4>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/collision_process2.png" style="width:5cm" alt="image" /></p>
</div>
<p>An Event Detection is triggered within the game engine when a particular condition is met, and it then publishes the corresponding message.</p>
<p>The Message Stream communicates the event data using ROS Messages {% cite ros%}<span class="citation" data-cites="ros_docs"></span>. ROS messages cater to a variety of sensor formats, from cameras, to pointcloud data, allowing for the ROS backend to make further decisions upon processing this data.</p>
<h4 id="registering-an-event-in-the-robotics-backend">Registering an Event in the Robotics backend</h4>
<p>The robotics interface, explored in Chapter <a href="#c1" data-reference-type="ref" data-reference="c1">[c1]</a>, functions on a Task basis. Events that are streamed on the network therefore need to be connected to processes for task rescheduling as well as drone state changes. Using the Topic Monitor from Section <a href="#section:SPI" data-reference-type="ref" data-reference="section:SPI">[section:SPI]</a>, changes in a streamed message can be made to induce state changes which, in turn, affects task management processes.</p>
<p>Until the event reaches the task management interface, the real drone is programmed to fly using Chapter <a href="#c1" data-reference-type="ref" data-reference="c1">[c1]</a>’s high level interface. The full behaviour of the drone can be visualised as in Figure <a href="#collision:sm_design" data-reference-type="ref" data-reference="collision:sm_design">[collision:sm_design]</a>.</p>
<div class="img-container">
<p><img src="../../assets/images/choreography/trajectory_diagram.png" style="width:8cm" alt="image" /></p>
</div>
<p>This state machine functions for a single drone: using the swarm building blocks developed in Section <a href="#section:SPI" data-reference-type="ref" data-reference="section:SPI">[section:SPI]</a>, the real drone to move to certain waypoints indefinitely. When a virtual collision is detected by the robotics backend, it induces a state change. The next state loads a custom trajectory on the drone, which is executed, before returning to an its looping trajectory.</p>
<p>In the next section, an experiment demonstrates the proposed workflow with a collision between a drone and a virtual body, and then to examine the performance of such a system.</p>
<h3 id="section:collisions">Performance Analysis</h3>
<p>We set up a virtual interface between real and virtual objects in real time. This MR simulation consists of a network interface between a robotics backend (ROS) and virtual environments (Unity3D). Similarly to {% cite ros_docs%}<span class="citation" data-cites="mr_planetary"></span>, the pipeline is then evaluated in terms of communication latency for two separate scenarios.</p>
<ul>
<li><p>when transmitting parameters into the simulated environment</p></li>
<li><p>when transmitting parameters to the robotics backend.</p></li>
</ul>
<h4 id="prediction">Prediction</h4>
<p><em>Latency of drone pose into a virtual environment</em></p>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/latencies_method1.png" style="width:4cm" alt="image" /></p>
</div>
<p>The latency of the pose injection is measured by determining the time difference between the ROS position and the time when it was received by the simulator.</p>
<p><em>Latency of event from the simulator to ROS</em></p>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/latencies_method2.png" style="width:4cm" alt="image" /></p>
</div>
<p>We can answer the performance question by investigating the lag time between the moment of collision and the moment the drone reacts. We choose the moment of a Virtual Collision because it is the ideal moment of a collision between the drone’s virtual avatar, and the bot agent. The collision lag time is illustrated in Figure <a href="#collision_lag_time" data-reference-type="ref" data-reference="collision_lag_time">[collision_lag_time]</a>.</p>
<h4 id="method">Method</h4>
<p>The time of different events is recorded as shown in Figure <a href="#feedback_loop" data-reference-type="ref" data-reference="feedback_loop">[feedback_loop]</a>. The experiment runs as such:</p>
<ol>
<li><p>a single drone is flown in the Flight Arena and it is virtualised as the drone agent.</p></li>
<li><p>Likewise, a virtual bot agent flies a trajectory in a game Engine.</p></li>
<li><p>When the drone and the bot collide, the drone is designed to react, by flying a pre-programmed spiral trajectory.</p></li>
</ol>
<p><strong>Data logger setups</strong></p>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/datalogger_setup1.png" style="height:4.5cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/datalogger_setup2.png" style="height:4.5cm" alt="image" /></p>
</div>
<p>This requires two separate data loggers: the one, monitoring the Unity environment, logs the timestamp and pose upon the virtual collision, and the other logs the timestamp of the drone State Change from within the Task Manager.</p>
<h3 id="results-1">Results</h3>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/ros_vs_unity_logs_inv3.png" style="width:6cm" alt="image" /></p>
</div>
<p><strong>Real-to-virtual Recorded Positions</strong> The drone poses are obtained through ROS and the simulator. In Figure <a href="#fig:superposition" data-reference-type="ref" data-reference="fig:superposition">[fig:superposition]</a>, these posees are superposed. The drone can be seen in green for ROS-times at high-rate sampling (120Hz) and in purple for Unity-times at a lower sampling (10Hz). The positions superpose perfectly. This is expected. This low sampling is sufficient to show the accuracy of the real-to-virtual procedure.</p>
<p><strong>Real-to-virtual Timestamps</strong> A second graph examines the differences in timestamps of simulator time (<strong>green</strong>) relative to ROS-time (<strong>red</strong>). Figure <a href="#fig:pos_time" data-reference-type="ref" data-reference="fig:pos_time">[fig:pos_time]</a> shows a substantial lag in positions.</p>
<div class="img-container">
<p><img src="../../assets/images/coordinates.png" style="width:4cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/time_delay_inv.png" style="width:11cm" alt="image" /></p>
</div>
<p>The avatar positions occur "before" real positions. This is due to the logs being based on simulation time, which records events slower than real time. This simulator clock seems to be affected by a system latency.</p>
<p><strong>Latency of Pose Injection</strong> We determine the latency of elements when injected into the virtual environment. The latency of the system is associated to the time between simulation and ROS time when recording the same drone pose. The resulting graph is plotted in Figure <a href="#fig:xr_poses" data-reference-type="ref" data-reference="fig:xr_poses">[fig:xr_poses]</a> and shows a linear trend.</p>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/latency_plot_inv2_fakeregression.png" style="width:11.5cm" alt="image" /></p>
</div>
<p>By adapting a linear regression, we determine a gradient of of cumulative latency.</p>
<p><strong>Latency During State Change</strong> In order to visualise the event sequence, each collision is assigned a <strong>red</strong> marker, with the moment of robotics backend state change being assigned a <strong>yellow</strong> marker. All the collisions are taken from the virtual logs and assigned ROS-compatible timestamps.</p>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/timelineview_legend.png" style="width:3.5cm" alt="image" /></p>
</div>
<p><strong>Collision Graphs of the Latency Experiment</strong></p>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/timelineview_inv1.png" style="width:11cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/hdi_graphs/front_inv.png" style="width:11.3cm" alt="image" /></p>
</div>
<p>The first plot shows a timeline view, where the moments of start and end of the experiment clearly show a change in Z, on three different occasions. These three collisions are associated to state changes.</p>
<p>These three collisions in particular are investigated, occurring 15 seconds from each other. Each collision latency is calculated according to the method set in the methodology. Figure <a href="#fig:latency_collisions_xr" data-reference-type="ref" data-reference="fig:latency_collisions_xr">[fig:latency_collisions_xr]</a> demonstrates a growing lag time that approximates an exponential - a similar performance bottleneck to the previous section.</p>
<div class="img-container">
<p><img src="../../assets/images/xr_discussion/exponent_fit.png" style="width:5cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/xr_graphs/latency_sm_crop.png" style="width:9cm" alt="image" /></p>
</div>
<p>This trendline is modelled after an exponential as follows: <span class="math display"><em>L</em><sub><em>o</em><em>u</em><em>t</em></sub> = (6.67589×10<sup>−8</sup>)<em>e</em><sup>0.190664<em>t</em></sup> ms</span></p>
<p>We can model the full end-to-end system latency as the addition of the latency and the 98t ms above:</p>
<p><span class="math display"><em>L</em><sub><em>s</em><em>y</em><em>s</em><em>t</em><em>e</em><em>m</em></sub> = <em>L</em><sub><em>i</em><em>n</em></sub> + <em>L</em><sub><em>o</em><em>u</em><em>t</em></sub> = 89(7.501×10<sup>−7</sup><em>e</em><sup>0.190664<em>t</em></sup>+<em>t</em>)ms</span></p>
<h3 id="evaluation">Evaluation</h3>
<div class="img-container">
<p><img src="../../assets/images/xr_discussion/gcs_simulation_bw.png" style="width:6cm" alt="image" /></p>
</div>
<p>Similarly to the Swarm Application Interface of Chapter <a href="#c1" data-reference-type="ref" data-reference="c1">[c1]</a>, Flightmare offers several tasks as part of their simulator, however they do not undergo tests with real hardware. This discrepancy naturally reflects in the differences in latency, where our system is dependent on a robotics backend on top of a simulator. This chapter can be considered a perception pipeline as opposed to a set of tests that undergo in simulation.</p>
<p>As opposed to simulators with an independent block for the physics engine, this experiment has focused mainly on visualising drone flight. Flight physics modelling is deliberately excluded. This lends itself well to a more photo-realistic, but slower, configuration.</p>
<p>On a <strong>functional</strong> standpoint, the proposed workflow worked as expected. A virtual body did come in collision a number of times with the drone’s avatar; through event data, the drone has reacted accordingly. This sequence of events was ensured by the choices of software architectures.</p>
<p>To respond to the <strong>performance</strong> question, we focus on the three key aspects highlighted in the Mixed Reality literature review:</p>
<ul>
<li><p>Fast prototyping of new environments: <strong>programmability</strong>.</p></li>
<li><p>A wide suite of sensors and of physical effects: <strong>variability</strong>.</p></li>
<li><p>A true-to-reality physical environment: the <strong>physical</strong> model.</p></li>
</ul>
<p>While the Mixed Reality Interface provides us with a simulated graphics engine, a communication channel was put in place that would communicate virtual events to the robot swarm. However, the collision experiment has demonstrated a cumulative delay of for a single quadrotor, and this can only increase with larger swarms and more complex manoeuvres. Since latency is a primary measure for image streaming and high performance drone tasks, we suggest the exploration of a network interface more focused on performance, and possibly the integration of existing simulators like Flightmare within the testbed.</p>
<div class="table*">
<div class="flushleft">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Test Description</th>
<th style="text-align: left;">Result</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><strong>Gesture Piloting</strong></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Gesture Recognition Effectiveness</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">System Response Time</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>Mixed Reality Interface</strong></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Latency of Pose Transmission</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Latency of State Changes</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">System Latency</td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
</div>
</div>
<h4 id="summary-1">Summary</h4>
<p>According to {% cite mr_planetary%}<span class="citation" data-cites="gcs_validation"></span>, a fully functional GCS provides for research capabilities which cannot be achieved through R/C flight alone. They emphasize Parameter Identification (PID) research as an alternative for flying a UAV by tracking values of flight and performing precise maneuvers. The second emphasis is into "research into new applications of subscale aircraft for otherwise dangerous or long mundane tasks". These goals echo the elements for live performances and flight recording used in our testbed.</p>
<p>Preiss et al. {% cite gcs_validation%}<span class="citation" data-cites="phan_hönig_ayanian_2018"></span> envision that mixed reality would interconnect a wide variety of physical spaces for collaboration. Humans can work safely within their own physical confines, while their intelligent counterparts can operate in more hazardous environments.</p>
<p>With these new mixed reality tools, Preiss et al. position their robotics testbed as "serving to acclimate end users with autonomous systems". They believe their approach is also well suited for mixed reality prototyping since they "will be able to substitute networking and AI components with alternative implementations", for instance by substituting onboard path finding onto offboard components. They further demonstrate that peer-to-peer networking can better simulate intercommunication between drones. With this, Preiss et al. uphold that mixed reality is a vital addition to better human-drone interfaces.</p>
<p>This chapter demonstrates a similar vision, through the practical means of human-agent interactions. With the data streaming interfaces of this Mixed Reality section, as well as from the Piloting section, this shows that new modalities can be created for autonomous vehicles.</p>
<p>Using the networked approach of events and sensor data, further tasks can be prototyped. This aligns with the goals of better service drones. Using the example tasks developed in the previous chapter, various GNC algorithms can be programmed, developed, and tested on hardware conditions.</p>
<p>This method encompasses a major amount of development on the drone platform. From the development of a custom backend, to the interconnection of a graphical simulator, this completes an ecosystem for research and development. While this work has been in major part, infrastructural, it opens the door to the development and testing of GNC algorithms, for instance Reinforcement Learning algorithms, a common occurrence in recent robotics.</p>
<h2 id="chapter-conclusion">Chapter Conclusion</h2>
<p>This chapter presents a streaming architecture for piloting UAVs using a webcam, and various forays into Human-Drone interactions. This architecture, which makes use of the drones’ command architecture, but also of a shared network, has lent itself to integrating various inputs – in this case webcam images. The output of this exercise is evident in the precision of the drones’ movement, as it was noticed in the various visualisations of the data.</p>
<p>However, While the Mixed Reality Interface provides us with a simulated graphics engine, a communication channel was put in place that would communicate virtual events to the robot swarm. However, the collision experiment has demonstrated a cumulative delay of for a single quadrotor, and this can only increase with larger swarms and more complex manoeuvres. Since latency is a primary measure for image streaming and high performance drone tasks, we suggest the exploration of a network interface more focused on performance, and possibly the integration of existing simulators like Flightmare within the testbed.</p>
<p>Using the networked approach of events and sensor data, further tasks can be prototyped. Various GNC algorithms can be programmed, developed, and tested on hardware conditions.</p>
<p>All in all, this work has come to demonstrate that a swarm setup can be rather easily adapted to human-drone research, and despite the performance bottlenecks, it succeeds in providing an end-to-end experience for the pilot, and further work should aid in{% cite phan_hönig_ayanian_2018%} streamlining this.</p>