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

<h2 id="section:hardware">Hardware Environment</h2>
<h3 id="drone-selection-process">Drone Selection Process</h3>
<p>Several drones were compared using custom criteria for drone development. These custom criteria are based on ease of use and programmability. The Dimensions criterion aims to minimize the drone size and weight. The Reconfigurable criterion investigates the modularity of the hardware layout. The Programmable criterion looks at the available interfaces for communicating with the firmware. The Autonomous Flight criterion looks at the compatibility of state estimation and trajectory planning algorithms.</p>
<div class="table*">
<div class="flushleft">
<table>
<tbody>
<tr class="odd">
<td style="text-align: left;">Criteria</td>
<td style="text-align: center;">Snapdragon</td>
<td style="text-align: center;">Bitcraze</td>
<td style="text-align: center;">Tello</td>
<td style="text-align: center;">Custom Flight</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: center;">Flight Pro</td>
<td style="text-align: center;">Crazyflie</td>
<td style="text-align: center;">Drone</td>
<td style="text-align: center;">Controller</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Dimensions</td>
<td style="text-align: center;">&#9678; &#9673; &#9673; &#9673; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9678;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9673; &#9673; &#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Reconfigurable</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: center;">&#9678; &#9673; &#9673; &#9673; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Programmable</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9673; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9673; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9673; &#9673; &#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Autonomous Flight</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9673; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: center;">&#9678; &#9678; &#9678; &#9678; &#9673;</td>
<td style="text-align: center;">&#9678; &#9673; &#9673; &#9673; &#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Selection</td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
</div>
</div>
<p>The Crazyflie Drone has several advantages over other drones.</p>
<ul>
<li><p><strong>Autonomous Flight</strong>. State estimation and trajectory planning are managed by the Crazyflie firmware. The operating procedure is simplified to sending setpoint commands from a remote PC. {% cite chaari_cheikhrouhou_koubâa_youssef_hmam_2021%}<span class="citation" data-cites="crazyflie_docs"></span></p></li>
<li><p><strong>Programmability</strong>. At the moment of writing, there are two APIs known to send high-level commands to the drone. {% cite crazyflie_docs%}<span class="citation" data-cites="crazyflie_docs"></span></p></li>
<li><p><strong>Dimensions</strong>. Due to our space constraints, a small, light drone is preferable. Our payload of motion-capture markers brings the Crazyflie’s mass to 33 grams.</p></li>
<li><p><strong>Reconfigurability</strong>. The Crazyflie is easily assembled and maintainable. It is compatible with a range of sensor modules for different activities. {% cite crazyflie_docs%}<span class="citation" data-cites="crazyflie_docs"></span></p></li>
</ul>
<h3 id="flight-arena-and-spatial-localization">Flight Arena and Spatial Localization</h3>
<div class="img-container">
<p><img src="../../assets/images/testbed/platform.jpg" style="width:2cm" alt="image" /> <img src="../../assets/images/testbed/camera_layout/cork_material.png" style="width:2cm" alt="image" /></p>
</div>
<p>The Flight Area (Figure <a href="#fig:flight_arena" data-reference-type="ref" data-reference="fig:flight_arena">[fig:flight_arena]</a>) measures 3 x 2 meters, with a table-to-ceiling distance of 1.3m. In order to dampen the impact of falling drones, the table is layered with anti-vibration cork material (Figure <a href="#fig:cork" data-reference-type="ref" data-reference="fig:cork">[fig:cork]</a>).</p>
<p>Optitrack {% cite crazyflie_docs%}<span class="citation" data-cites="optitrack"></span> was adopted as the Motion Capture since the equipment was available in the laboratory. It is compatible with the swarm management solution of Section <a href="#section:swarm" data-reference-type="ref" data-reference="section:swarm">1.5.5</a>. Optitrack uses a Point Cloud reconstruction engine {% cite optitrack%}<span class="citation" data-cites="optitrack_docs"></span>. That is, it triangulates two-dimensional points from camera images into coordinates in a three-dimensional space. For this purpose, four Flex 13 cameras are set up on the Flight Arena (as seen in Figure <a href="#fig:flight_arena" data-reference-type="ref" data-reference="fig:flight_arena">[fig:flight_arena]</a>).</p>
<p>The Flex 13 cameras {% cite optitrack_docs%}<span class="citation" data-cites="optitrack_docs"></span> are infrared cameras, and so they must have an unobstructed view of any tracked object.</p>
<p>The exact positions of the cameras give a certain coverage of the Flight Arena. The next section determines how much of the Flight Arena is localized by the cameras.</p>
<h3 id="lightray-coverage-study">Lightray Coverage Study</h3>
<p>We investigate how much of the flight arena is localized by the motion capture. The drones can only be flown in a space covered by the infrared cameras, therefore we perform a design study to maximize this flight space.</p>
<h4 id="lightray-simulation">Lightray Simulation</h4>
<p>A model is designed in Solidworks {% cite optitrack_docs%}<span class="citation" data-cites="solidworks"></span> to simulate the coverage of our cameras. Figure <a href="#fig:45" data-reference-type="ref" data-reference="fig:45">[fig:45]</a> simulates the camera coverage on a table the size of the Flight Arena. A key factor is the camera’s pitch angle down from the horizontal. Figure <a href="#fig:45" data-reference-type="ref" data-reference="fig:45">[fig:45]</a> compares an orientation at 45° from the horizontal to one at 30 degrees.</p>
<div class="img-container">
<p><img src="../../assets/images/testbed/camera_layout/45_iso.PNG" style="width:5cm;height:4cm" alt="image" /> <img src="../../assets/images/testbed/camera_layout/30_iso.PNG" style="height:4cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/testbed/camera_layout/intersection/firstray.PNG" style="height:2cm" alt="image" /> <img src="../../assets/images/testbed/camera_layout/intersection/allrays.PNG" style="height:2cm" alt="image" /><br />
<img src="../../assets/images/testbed/camera_layout/intersection/intersection.PNG" style="height:2cm" alt="image" /> <img src="../../assets/images/testbed/camera_layout/intersection/final.PNG" style="height:2cm" alt="image" /></p>
</div>
<p>The coverage percentage is determined as the volume of space localized by the flight cameras over the total usable volume above the Flight Arena. Figure <a href="#fig:intersection_procedure" data-reference-type="ref" data-reference="fig:intersection_procedure">[fig:intersection_procedure]</a> shows the modelling process of ray coverage volumes. The design requirements are as follow:</p>
<ul>
<li><p>The cameras are placed above the table corners. within the net region so as to have a clear view of the drones when the net is lowered</p></li>
<li><p>There are a total of 4 cameras available during motion capture installation. The flight space measures 3×2×1.3 m.</p></li>
<li><p>Flex 13 cameras have a 56° field of view, and this is replicated in simulation (Figure <a href="#fig:intersection_procedure" data-reference-type="ref" data-reference="fig:intersection_procedure">[fig:intersection_procedure]</a>).</p></li>
<li><p>In order to triangulate a position, the motion capture requires a minimum of 2 rays to intersect {% cite solidworks%}<span class="citation" data-cites="optitrack_docs"></span>.</p></li>
</ul>
<p>These volumes can then be determined in Solidworks using its Volumetric Tool {% cite optitrack_docs%}<span class="citation" data-cites="solidworks_docs"></span>. For a pitch angle of 30<span class="math inline"><sup><em>o</em></sup></span>, The volumes of the flight space and of the intersection area above, are respectively of 7.8 <span class="math inline"><em>m</em><sup>2</sup></span> and 6.134 <span class="math inline"><em>m</em><sup>2</sup></span>. As a result, we determine that the usable region for flight is 78.64% of the 3×2×1.3 m flight space. This demonstrates that 20% of the flight space is unusable. This is not surprising, considering that 4 cameras are directly above the table and constrained by the netting.</p>
<h4 id="coverage-optimisation-study">Coverage Optimisation Study</h4>
<p>The camera’s pitch angle is varied to determine the point of optimal coverage. Figure <a href="#fig:volumes" data-reference-type="ref" data-reference="fig:volumes">[fig:volumes]</a> shows the volumes generated during the study.</p>
<div class="img-container">
<p><img src="../../assets/images/testbed/camera_layout/corner_20deg.PNG" style="height:3.8cm" alt="image" /> <img src="../../assets/images/testbed/camera_layout/corner_25deg.PNG" style="height:3.8cm" alt="image" /><br />
<img src="../../assets/images/testbed/camera_layout/corner_30deg.PNG" style="height:4cm" alt="image" /> <img src="../../assets/images/testbed/camera_layout/corner_35deg.PNG" style="height:4cm" alt="image" /><br />
</p>
</div>
<p>The study has two parts. The first study varies by increments of 5<span class="math inline"><sup><em>o</em></sup></span>, in order to determine the range of volume maxima. The second study finetunes by increments of 1<span class="math inline"><sup><em>o</em></sup></span>, with the help of a Solidworks Design Study {% cite solidworks_docs%}<span class="citation" data-cites="solidworks_docs"></span>. This simulation tool is used to generate volumes automatically. It has trouble generating volumes if the angle increments are too large, therefore the first study is done manually.</p>
<div class="table*">
<table>
<tbody>
<tr class="odd">
<td style="text-align: left;">Pitch</td>
<td style="text-align: center;">Volume</td>
<td style="text-align: center;">%</td>
<td style="text-align: center;">Max</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">(deg)</td>
<td style="text-align: center;">(<span class="math inline"><em>m</em><em>m</em><sup>3</sup></span>)</td>
<td style="text-align: center;">Covered</td>
<td style="text-align: center;">Range</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">10</td>
<td style="text-align: center;">6 607 805 800.35</td>
<td style="text-align: center;">84.7154</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">15</td>
<td style="text-align: center;">6 970 142 481.03</td>
<td style="text-align: center;">89.3608</td>
<td style="text-align: center;">&#9678;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: center;">7 014 173 181.97</td>
<td style="text-align: center;">89.9253</td>
<td style="text-align: center;">&#9678;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">25</td>
<td style="text-align: center;">6 804 720 310.30</td>
<td style="text-align: center;">87.2400</td>
<td style="text-align: center;">&#9678;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">30</td>
<td style="text-align: center;">4 855 500 995.33</td>
<td style="text-align: center;">62.2500</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">35</td>
<td style="text-align: center;">5 006 693 602.87</td>
<td style="text-align: center;">64.1884</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">40</td>
<td style="text-align: center;">3 747 076 773.66</td>
<td style="text-align: center;">48.0394</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
<p><br />
</p>
<table>
<tbody>
<tr class="odd">
<td style="text-align: left;">Pitch</td>
<td style="text-align: center;">Volume</td>
<td style="text-align: center;">%</td>
<td style="text-align: center;">Max</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">(deg)</td>
<td style="text-align: center;">(<span class="math inline"><em>m</em><em>m</em><sup>3</sup></span>)</td>
<td style="text-align: center;">Covered</td>
<td style="text-align: center;">Range</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">16</td>
<td style="text-align: center;">7007549683.27</td>
<td style="text-align: center;">89.8404</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">17</td>
<td style="text-align: center;">7034381844.70</td>
<td style="text-align: center;">90.1844</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">18</td>
<td style="text-align: center;">7050625519.44</td>
<td style="text-align: center;">90.3926</td>
<td style="text-align: center;">&#9678;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">19</td>
<td style="text-align: center;">7056144612.83</td>
<td style="text-align: center;">90.4634</td>
<td style="text-align: center;">&#9678;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">20</td>
<td style="text-align: center;">7014172714.71</td>
<td style="text-align: center;">89.9253</td>
<td style="text-align: center;">&#9678;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">21</td>
<td style="text-align: center;">6999358686.15</td>
<td style="text-align: center;">89.7354</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">22</td>
<td style="text-align: center;">6972124192.42</td>
<td style="text-align: center;">89.3862</td>
<td style="text-align: center;">&#9673;</td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
</div>
<p>Through these studies, the coverage volume was increased from 78.64% by % up to 89.95%, and by % to . This demonstrates that about 10% of the flight space is still out of reach. While the netting constraint forces the cameras to have this inconvenience, the study could be further optimised by varying the yaw angle of the cameras and moving them away from the corners.</p>
<h3 id="flight-stability-tests">Flight Stability Tests</h3>
<p>Tests of the stability of robotic systems are routinely performed to measure their robustness to external forces. This is a key challenge in drone development {% cite solidworks_docs%}<span class="citation" data-cites="crazyflie_docs"></span>, where a drone maintains dynamic stability by counterbalancing six directions of freedom, as opposed to two for wheeled systems in static stability.</p>
<div class="img-container">

<img src="../../assets/images/testbed/controlloop_bw.png" style="width:6cm" alt="image" /><figcaption>Drone Selection Matrix.</figcaption>

</div>
<p>The Crazyswarm ecosystem {% cite crazyflie_docs%}<span class="citation" data-cites="crazyflie_docs"></span> makes use of a position and rate controller for each drone in its swarm. This means that a setpoint is sent to each drone separately, each correcting their current pose towards the setpoint. The streaming setpoints are broadcasted from one or more antennas. As the number of drones in the swarm increases, they receive less frequent broadcasts from the antenna {% cite crazyflie_docs%}<span class="citation" data-cites="preiss_hönig_sukhatme_ayanian_2017"></span>.</p>
<p>The purpose of this test is to determine the response of the drone’s position and angle controllers to the natural disturbance during hovering. This experiment investigates the effect of antenna distance and interference on drone flight. With multiple drones to a single antenna, we evaluate if the system demonstrates any performance limits.</p>
<h4 id="hypothesis">Hypothesis</h4>
<p>The hypothesis is as such: the error in drone pose will correlate with the distance of the drones from the antenna.</p>
<h4 id="prediction">Prediction</h4>
<p>A hover stability test is a good measure of system performance since it requires quick readjustments of the drone to counter natural disturbances during hovering. In {% cite preiss_hönig_sukhatme_ayanian_2017%}<span class="citation" data-cites="experimental_tuning"></span>, determine the performance of their flight controller by comparing the attitude of the drone in relation to the demanded null value of angular rotations. In contrast, our input is a setpoint. The output is a set of translation and rotational angles relative to a demanded null value for translation and rotation. This output is graphed as a deviation over time. The shape of the response charts are associated with flight stability over time.</p>
<h4 id="experiment-methodology">Experiment Methodology</h4>
<div class="img-container">

<img src="../../assets/images/chore_pictures/3drones/pic.png" style="width:5cm" alt="image" /><figcaption>The Crazyflie 2.1 miniature quadcopter with four motion-capture markers, expansion boards (not visib</figcaption>

</div>
<p>Hover stability is examined on the Flight Arena. The telemetry recording and external video cameras are programmed to launch with the swarm control interface. Three drones are hovered in the Flight Arena at an altitude of around 1 m. It was possible to record a 20-s long autonomous flight during which the flight controller attempted to stabilize the quadcopter. During that time, the quadcopter remained within a radius of two meters from its takeoff location.</p>
<p><strong>Constraints</strong>: In preparation for the flight, each of the three drones are inspected for minimal positional displacement of less than (1cm + 0.01 rad). This ensures fully functional position controllers for the drones.</p>
<h4 id="results">Results</h4>
<p>The flightpaths of the three drones are plotted alongside . The topview and the sideview are featured below.</p>
<div class="img-container">
<p><img src="../../assets/images/chore_pictures/3drones/x_translations_ann.png" style="width:6cm" alt="image" /> <img src="../../assets/images/chore_pictures/3drones/y_translations_ann.png" style="width:6cm" alt="image" /><br />
<img src="../../assets/images/chore_pictures/3drones/z_translations_ann.png" style="width:6cm" alt="image" /> <img src="../../assets/images/chore_pictures/3drones/anglerates_ann.png" style="width:6cm" alt="image" /></p>
</div>
<div class="img-container">

<img src="../../assets/images/chore_pictures/3drones/3dplot_paths_inv.png" style="width:4.5cm" alt="image" /><figcaption>Overview of Selection Process.</figcaption>

</div>
<p>The flightpaths are smooth and generally show very minimal jerking. There are very little discontinuities, attesting to a continuous localization process.</p>
<div class="table*">
<table>
<tbody>
<tr class="odd">
<td style="text-align: left;"><strong>Criteria</strong></td>
<td style="text-align: center;"><strong>Drone 1</strong></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><strong>Drone 2</strong></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: center;">Min</td>
<td style="text-align: center;">Max</td>
<td style="text-align: center;">Range</td>
<td style="text-align: center;">Min</td>
<td style="text-align: center;">Max</td>
<td style="text-align: center;">Range</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">X</td>
<td style="text-align: center;">-0.84</td>
<td style="text-align: center;">-0.80</td>
<td style="text-align: center;">0.04</td>
<td style="text-align: center;">0.44</td>
<td style="text-align: center;">0.48</td>
<td style="text-align: center;">0.04</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">y</td>
<td style="text-align: center;">-0.0272</td>
<td style="text-align: center;">-0.0228</td>
<td style="text-align: center;">0.0044</td>
<td style="text-align: center;">-0.0289</td>
<td style="text-align: center;">-0.0255</td>
<td style="text-align: center;">0.0034</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Z</td>
<td style="text-align: center;">0.31</td>
<td style="text-align: center;">0.37</td>
<td style="text-align: center;">0.06</td>
<td style="text-align: center;">0.28</td>
<td style="text-align: center;">0.34</td>
<td style="text-align: center;">0.06</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Roll</td>
<td style="text-align: center;">-0.018</td>
<td style="text-align: center;">0.009</td>
<td style="text-align: center;">0.027</td>
<td style="text-align: center;">0.009</td>
<td style="text-align: center;">0.017</td>
<td style="text-align: center;">0.008</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Pitch</td>
<td style="text-align: center;">-0.020</td>
<td style="text-align: center;">0.036</td>
<td style="text-align: center;">0.056</td>
<td style="text-align: center;">-0.003</td>
<td style="text-align: center;">0.026</td>
<td style="text-align: center;">0.029</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Yaw</td>
<td style="text-align: center;">-0.034</td>
<td style="text-align: center;">0.039</td>
<td style="text-align: center;">0.073</td>
<td style="text-align: center;">-0.014</td>
<td style="text-align: center;">0.021</td>
<td style="text-align: center;">0.035</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Selection</td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;">\ding{55}</td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;">&amp;#1000;</td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
</div>
<p>&amp;#9675; &#9673; &amp;#1000; &amp;#x02A2F; Drone 2 has less variation in both translations and rotations than Drone 1. This is confirmed in Table <a href="#tab:stability_comparison" data-reference-type="ref" data-reference="tab:stability_comparison">[tab:stability_comparison]</a>. Drone 2 is more stable in this test than Drone 1. The sample hover error is .</p>
<p>The discrepancy between the two drones could be attributed to a number of factors. This work may be improved with a second test, where the two drones’ positions are inversed. All in all, the flight is substantially accurate, with a peak translation of 6cm.</p>
<h4 id="conclusion-of-test">Conclusion of Test</h4>
<p>Drone 2 is further from the arena and exhibits more stability. The drone that is furthest from the antenna does not have more pose error, and the hypothesis is rejected.</p>
