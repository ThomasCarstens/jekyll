---
layout: single
title: "Sampling Environment Data with a Drone"
excerpt: "Analysis of a drone-sampled dataset."
header:
  teaser: ../assets/images/posts/braai-tongs/tongs-header.jpg
  overlay_image: assets/images/posts/braai-tongs/detail-open.jpg
categories: Project
tags:
- Electro-mechanical Product Design
- Solidworks
toc: true
toc_sticky: true
date: 2017-12-02
gallery:
  - image_path: /assets/images/posts/braai-tongs/left-attached.jpg
    alt: "Braai tongs attached"
    title: "Braai tongs attached"

  - image_path: /assets/images/posts/braai-tongs/left-detached.jpg
    alt: "Braai tongs detached"
    title: "Braai tongs detached"

---

# ![favicon](/assets/images/favicon.jpg){: .aligned-left} Environment Sampling and Evaluation

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
</style>
<div class="img-container">
<p><img src="../../assets/images/stage_system/stage_ref/factories_bw.jpg" style="width:5cm" alt="image" /></p>
</div>
<p>Environmental sensing usually requires substantial time for data collection or more distributed sensing systems. The use of atmospheric sensors is a major element in remote sensing {% cite vibrationmount_video%}<span class="citation" data-cites="metrology_survey"></span>. With a platform that can carry multiple types of sensors, a simple field scan can help understand the limitations of a drone task, and the potential for further operations. As an air monitoring solution, this demonstration can be extended to industrial-type solutions, such as air pollution monitoring {% cite metrology_survey%}<span class="citation" data-cites="sørensen_jacobsen_hansen_2017"></span>. All these factors show that drones form part of a trend towards service automation for industrial purposes.</p>
<p>We do remote sensing upon a UAV to simplify the task of environment sensing. A drone is equipped with remote sensors. It is flown in a field where it detects physical changes in the environment: lighting, humidity, and temperature. This data is then processed to determine the effectiveness of the survey. A presentation video is available (Google Drive) {% cite sørensen_jacobsen_hansen_2017%}<span class="citation" data-cites="fieldscan_video"></span>. The experiment data is available on Google Drive {% cite fieldscan_video%}<span class="citation" data-cites="fieldscan_dataset"></span>.</p>
<h3 id="daq-system-design">DAQ System Design</h3>
<p>This section documents the design of the Atmosphere Data Payload selected in Section <a href="#section:sensor_system" data-reference-type="ref" data-reference="section:sensor_system">1.3.1.3</a>. It is composed of three stages.</p>
<div class="img-container">
<p><span><img src="../../assets/images/stage_system/drone_setup/payload_onboard.png" style="width:8cm" alt="image" /></span></p>
</div>
<p>The payload is installed on the drone in Step 1. Flight procedures are designed in Step 2. The DAQ Activation is done in Step 3.</p>
<h4 id="section:msp_daq">System for Low-Cost Sensors</h4>
<div class="img-container">
<p><img src="../../assets/images/stage_system/nano_pic.jpg" style="width:3cm" alt="image" /></p>
</div>
<p>The Arduino sensor range is chosen for prototyping for its low-cost sensors. Using an Arduino Nano {% cite fieldscan_dataset%}<span class="citation" data-cites="arduino_docs"></span>, such sensors can be easily integrated. The Arduino Nano is sold as a small, complete, and breadboard-friendly board based on Arduino’s larger counterpart, the ATmega328. It only weighs 7g with minimal volume.</p>
<h4 id="module-design">Module Design</h4>
<div class="img-container">
<p><span><img src="../../assets/images/stage_system/drone_setup/payload_onboard1.png" style="width:5.5cm" alt="image" /></span></p>
</div>
<p>Two separate modules are designed for the Atmospheric Data and the Vibration Data. In each, an independent battery powers the logging unit, and the sensors attached to it. The Pixhawk board is included in the first system since some the GPS and luminosity sensor are logged via the Pixhawk board.</p>
<h4 id="daq-control-layer">DAQ Control Layer</h4>
<div class="img-container">
<p><span><img src="../../assets/images/stage_system/drone_setup/payload_onboard2.png" style="width:5.5cm" alt="image" /></span></p>
</div>
<p>The DAQ is configured to activate and deactivate the datalogging process on command. To achieve this, we use custom activation firmware on the PX4 operating system.</p>
<div class="table*">
<div class="flushleft">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Boards</th>
<th style="text-align: center;">Switch</th>
<th style="text-align: center;">Activation</th>
<th style="text-align: center;">Deactivation</th>
<th style="text-align: center;">Prior to Activation</th>
<th style="text-align: left;"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2. Arduino Nano</td>
<td style="text-align: center;">2-2</td>
<td style="text-align: center;">On boot</td>
<td style="text-align: center;">On shutdown</td>
<td style="text-align: center;">None</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">3. Pixhawk</td>
<td style="text-align: center;">2-1</td>
<td style="text-align: center;">On boot</td>
<td style="text-align: center;">On shutdown</td>
<td style="text-align: center;">None</td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>
</div>
</div>
<p>The data-logging activation file was coded in C++, and compiled into an executable via the MAVLink protocol. During operation, it toggles a pin (Pixhawk’s FMU Channel 6), which is then detected by the Arduino Nano in order to begin and end the logging on the Datalogger.</p>
<p>A separate custom logger detects Arduino activation and records its timestamp in the PX4 debug log.</p>
<h3 id="sensor-system-evaluation">Sensor System Evaluation</h3>
<h4 id="aim">Aim</h4>
<p>Using three separate atmospheric variables, we determine the accuracy of the drone sensing solution.</p>
<h4 id="prediction-1">Prediction</h4>
<p>Sunlit and shaded regions were scanned for relative humidity, luminosity and ambient temperature. The drone’s flightpath is changed randomly by the operator to create region overlaps. The trajectory plots demonstrate any inconsistencies in the readings. We determine the maximal variation per second and per meter as a measure of the fluctuations in lighting and in temperature.</p>
<h4 id="method">Method</h4>
<div class="img-container">
<p><span><img src="../../assets/images/stage_system/drone_setup/payload_onboard3.png" style="width:5.5cm" alt="image" /></span></p>
</div>
<p><em>Measurement Equipment Setup</em> Instruments that were used in the system are pictured in Figure <a href="#connections:arduino" data-reference-type="ref" data-reference="connections:arduino">[connections:arduino]</a>. These include the DH11 Temperature and Humidity sensor, as well as a 5mm LDR Luminosity Sensor, and finally, the companion GPS. A particularity is that the DH11 is attached to the Arduino Board, and Logged with the use of an Arduino Data Logger, while the 5mm LDR is connected to an ADC input on the Pixhawk board, containing a self-enclosed data logger.</p>
<p>The Pixhawk logger supports 100Hz data logging while the Arduino data logger averages at 10Hz logging. Both data loggers support Micro SD cards with a capacity of up to 64GB to store high-resolution video data, photos and flight telemetry.</p>
<p><em>Experiment Procedure</em> The flight takes place in an empty field of approximately 100x60m, identified for the differences in lighting between the tree shade and the sunlit field. The drone is piloted by hand. This requires a certain method:</p>
<ol>
<li><p>System checks (battery monitor, screws, etc.)</p></li>
<li><p>Activating the drone.</p></li>
<li><p>Drone takeoff and moving to an altitude of 2m.</p></li>
<li><p>Altitude lock.</p></li>
<li><p>Activating the Arduino data acquisition with a PX4 trigger application.</p></li>
<li><p>Piloted flight across the field, along sunlit and shaded regions.</p></li>
</ol>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/Flight_Drone.png" style="width:5cm" alt="image" /></p>
</div>
<p><em>Data collection</em> The data was collected on 24 August 2021, over an empty field of approximately 100x60m. Both the lighting and the GPS data are taken from the Pixhawk Log. They were both sampled at a frequency of 98 Hz. The Arduino Logger was activated 248s after the Pixhawk Logger. The Arduino Logger was active for a duration of 712 seconds, of which 464s are common to both boards. Both the temperature and the humidity are taken from the Arduino Datalogger. They were both sampled at a frequency of 11.7 Hz.<br />
<em>Dataset</em> A presentation video is available (Google Drive) {% cite arduino_docs%}<span class="citation" data-cites="fieldscan_video"></span>. The experiment data is available on Google Drive {% cite fieldscan_video%}<span class="citation" data-cites="fieldscan_dataset"></span>.</p>
<h4 id="results-1">Results</h4>
<p><strong>Timeline of Environment Sensor Readings</strong> There is a stark contrast between sunny and shady regions in the data.</p>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/arduino_plot.png" style="width:12cm" alt="image" /></p>
</div>
<p>This is a change of 20% of the luminosity range, where sunny regions saturate the sensor, and shady regions are marked by sudden drops.</p>
<p><strong>Trajectory Plot</strong> Figure <a href="#fig:lighting_field" data-reference-type="ref" data-reference="fig:lighting_field">[fig:lighting_field]</a> plots the lighting readings over the trajectory.</p>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/Temperature_field_plot.png" style="width:9cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/Humidity_field_plot.png" style="width:9cm" alt="image" /></p>
</div>
<p>This confirms that the data is very sensitive to lighting differences. The darker patches in the sunlit area might be explained by the passage of clouds during the procedure.</p>
<p><strong></strong> A first graph presents the magnitude of the changes in light and temperature, by computing their rates of change over time. The magnitudes are normalized by their operating ranges: 20-90% of Relative Humidity for the DHT11 sensor, 20-150mV of ADC voltage for the LDR sensor.</p>
<p><span class="math display">$${\frac{\Delta{r}}{{t}}} = 
{\frac{r_{f} - r_{i}}{r_{max}-r_{min}} * 100}$$</span></p>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/sensor_speeds.png" style="height:3.2cm" alt="image" /></p>
</div>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/changes_m2.png" style="height:3.2cm" alt="image" /></p>
</div>
<p>According to (a), the maximum values suggest that the LDR sensor records changes of vs the DHT11 sensor’s . The temperature and humidity vary less rapidly, and this is very apparent in the plots.</p>
<p><strong></strong> To better evaluate the sensing speed, we investigate the maximum fluctuations per second, and then per meter. This data recording speed is used in (b) in coordination with the drone velocity as recorded by the Pixhawk setup, in order to obtain fluctuations per meter, independent from speed. This is done with the following equations.</p>
<p><span class="math display">$${\frac{\Delta{r}}{{m}}} = 
{\frac{r_{f} - r_{i}}{t_{f} - t_{i}}}* {\frac{1}{\bar{v}}}$$</span></p>
<div class="img-container">
<p><img src="../../assets/images/stage_graphs/environment_results/lux_voltage.png" style="width:5cm" alt="image" /></p>
</div>
<p>The following equation is taken from {% cite fieldscan_dataset%}<span class="citation" data-cites="ldr_testing"></span>, whereas determines an empirical formula to convert the ADC voltage to lux for the Arduino’s Light Dependent Resistor module: <span class="math display">log (<em>L</em><sub><em>l</em><em>u</em><em>x</em></sub>) =  − 1.4 * log {max |<em>V</em><sub><em>a</em><em>d</em><em>c</em></sub>|} + 7.098</span></p>
<p>Whereas the LDR sensor records , the DHT11 detects . This shows the range of local changes over the field and it seems reasonable for stark changes in light vs more gradual changes in humidity.</p>
<h3 id="discussion">Discussion</h3>
<p>The proposed UAV architecture has proven itself effective at capturing fluctuating environment data. When examining the luminosity readings, the measurements are very consistent with shade/light regions, by changes of as much as 20% of the luminosity range. Sunny regions saturate the sensor, and shady regions are marked by sudden drops. This suggests a high accuracy, especially seen as the drone was piloted by hand.</p>
<p>The luminosity plot demonstrates very precise readings despite the drone’s velocity. This is facilitated by rapid data logging at 100Hz. The fact that the drone was piloted by hand, on an arbitrary path with region overlaps, illustrates plainly how mobile mapping is a worthwhile tool for rapid data collection.</p>
<p>There is much less of a correlation between the readings and their position in space. We suggest two potential issues with the DH11 sensor:</p>
<ul>
<li><p>Movement may affect the temperature and humidity. We recommend to further investigate how the readings vary with altitude, speed and acceleration.</p></li>
<li><p>Heat convection on the drone and the sensor itself may be recorded by the sensor instead of environment temperature. We recommend to further investigate how accumulated heat affect the readings.</p></li>
</ul>
<p>Additionally, this experiment demonstrates that a payload drone can be extended to other types of sensors for other applications. The data acquisition setup proves to be functional. This setup was developed prior to the experiment with the goal to integrate many other types of sensors.</p>
<p>The flight was quite smooth and simple to undertake. As opposed to conventional means of environmental sensing {% cite ldr_testing%}<span class="citation" data-cites="xiang_xia_zhang_2020"></span>, this flight requires no site preparation. This is largely due to the selected drone system, as well as the work done to automate the data acquisition procedures.</p>
<p>This procedure was greatly assisted by the datalogger, whereas GPS data and atmospheric data could be correlated without major issues. The correlation between different elements have uncovered a topography in an unexpectedly accurate manner. As we examine the systems that aid in practice, we note the importance of the drone as a platform for capturing scans of a 3 dimensional environment in a rapid, and timely manner. At the time of writing, Alliantech is compiling a marketing video for this environment sensing solution.</p>

<div class="table*">
<div class="flushleft">
<table>
<thead>
<tr class="header">
<th style="text-align: left;">Test Description</th>
<th style="text-align: left;">Findings</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><strong></strong></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">DHT11</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">DHT11</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">LDR</td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">LDR</td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong></strong></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Range of Vibration Sensing System</td>
<td style="text-align: left;">0-</td>
</tr>
<tr class="even">
<td style="text-align: left;">Margin of Error up to Natural Frequency</td>
<td style="text-align: left;">50% margin of error</td>
</tr>
</tbody>
</table>
</div>
</div>
