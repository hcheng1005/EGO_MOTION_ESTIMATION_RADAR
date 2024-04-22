# Ego-motion Estimation by Radar Sensor - nuScenes dataset
[detailed design document link](./1_radar_ego_motion_cartesian.pdf)


## Introduction
Here we use the filtered measurements that are in cartesian (px, py, vx, vy). It is assumed that the **vehicle is car-like and 2WD**.

## Table of Contents <a name="t0"></a>

- [Introduction](#introduction)
- [Table of Contents ](#table-of-contents-)
  - [1. Sensor Setup and Layout ](#1-sensor-setup-and-layout-)
  - [2. Inputs Considered and Required Outputs ](#2-inputs-considered-and-required-outputs-)
  - [3. Radar Scan Visualization in Ego Vehicle frame ](#3-radar-scan-visualization-in-ego-vehicle-frame-)
  - [4. High Level Architecture ](#4-high-level-architecture-)
  - [6. Results \& Plots ](#6-results--plots-)
  - [7. Conclusion ](#7-conclusion-)

<br>


### 1. Sensor Setup and Layout <a name="t1"></a>
In this project [nuScenes](https://www.nuscenes.org/) dataset is used for validating and generating results. The sensors are not synchronized and the sensor layout has a full 360&deg; coverage. The dataset is considered here because it is from a comercially available radar which gives measurements in cartesian coordinates.
<br>
![](./readme_artifacts/1_sensor_setup.PNG)
<br>

[Back to TOC](#t0)
<br><br>


### 2. Inputs Considered and Required Outputs <a name="t2"></a>
A detailed summary of all the required inputs and the outputs are as follows.![](./readme_artifacts/2_inputs_outputs.PNG)
<br>

[Back to TOC](#t0)
<br><br>


### 3. Radar Scan Visualization in Ego Vehicle frame <a name="t3"></a>
The below animation is a brief sequence of radar frames where the velocity has both the components. Since the velocity vector has both components ( unlike range-rate ), from the animation we can guess when the vehicle is turning, wobbling and moving approximately in a straight line.
![](./readme_artifacts/radar_range_rate1.gif)
<br>

[Back to TOC](#t0)


### 4. High Level Architecture <a name="t4"></a>
Since the measurements are filtered and each measurement has information regarding its dynamic status, the architecture is relatively simplier than the architecture for [ego-motion estimation from raw radar point cloud project](https://github.com/UditBhaskar19/EGO_MOTION_ESTIMATION/tree/main/2_egomotion_radar_polar). The main components are as follows:
   - **Coordinate Transformation of measurements from sensor frame to vehicle frame** : The measurements are first transformed from sensor frame to vehicle frame.<br> 
   - **Stationary Measurement Identification** : The measurements are compared with the predicted measurements computed from previous state estimate of the ego-motion. Only the gated measurements are considered for further processing.<br> 
   - **Vehicle Ego-motion estimation** : Next the ego motion is computed w.r.t the wheel base center where it is assumed that the lateral velocity component is 0 ( vy = 0 )<br><br>
![](./readme_artifacts/4_architecture.PNG)
<br>

[Back to TOC](#t0)
<br><br>

### 6. Results & Plots <a name="t5"></a>
   - **estimation output plot for scene - 0061** : <br>
![](./readme_artifacts/5_1_0061_all_plots.PNG)
<br>

[Back to TOC](#t0)


### 7. Conclusion <a name="t6"></a>
Overall the presented approach for ego-motion estimation looks promising. Further details can be found in the [document](./1_radar_ego_motion_cartesian.pdf)
<br><br><br>

[Back to TOC](#t0)


