# Ego-motion Estimation From Wheel Speeds & Steering Angle
[detailed design document link](./1_ego_motion_from_wheel_speed.pdf)


## Introduction
Here the ego-motion estimation is performed from the **wheel speeds** and **steering angle**. It is assumed that the **vehicle is car-like with 4 wheels & is a 2-Wheeled Drive**.The results are validated using **[NuScenes](https://www.nuscenes.org/)** mini dataset.


## Table of Contents <a name="t0"></a>

   - [Inputs Considered and Required Outputs](#t1)
   - [High Level Architecture](#t2)
   - [Results, Plots and Some Observations regarding Plots](#t3)
   - [Conclusion](#t4)

<br>


### 1. Inputs Considered and Required Outputs  <a name="t1"></a>
![](./readme_artifacts/12_inputs_outputs.PNG)
<br>

[Back to TOC](#t0)
<br>

### 2. High Level Architecture  <a name="t2"></a>
   - **Wheel Speed Conversion** : Convert wheel speed input signals from rpm to m/s
   - **Wheel Coordinates Computation** : Compute wheel locations w.r.t the vehicle wheel base center. Ideally these should be determined from some calibration procedure
   - **Wheel Steer Angle Computation** : Compute Front Left and Front Right wheel steer angles from raw inpute steering signal
   - **Valid Wheel Speed Selection by Gating** : Due to road conditions and other environmental effects some wheels might be prone to skidding and slipping. Hence a gating procedure is introduced here to ensure that the wheel speed signal that are most likely corrupted are ignored for further processing. 
   - **Vehicle Ego-motion estimation** : Compute ego-motion w.r.t the wheel base center. Here it is assumed that the lateral velocity component is 0 ( vy = 0 )
<br><br>
![](./readme_artifacts/1_architecture.PNG)
<br>

[Back to TOC](#t0)
<br>

### 3. Results , Plots and Some Observations regarding Plots ( NuScenes mini - scene 0916 )  <a name="t3"></a>
   - **Input Signal Plot** : It can be observed that the wheel speed signals are significantly more noisy than the steering signal. Hence in this project, the wheel speeds are treated as stochastic inputs which are assumed to be uncorrelated and normally distributed. The steering angle which is almost noiseless is treated as a control parameter. Under these considerations the problem of ego-motion estimation reduces to the linear least squares problem.
![](./readme_artifacts/3_input_signals.PNG)
   - **Ego motion estimation output Plot** : The estimated yaw-rate seems to be more noisy than the estimated velocities. Optionally the estimations can be made smoother by Kalman Filtering.
![](./readme_artifacts/4_estimated_outputs.PNG)
   - **Comparing estimated velocities and the input wheel speeds** : The variation of the estimated vx w.r.t time is as expected. Since the ego-motion is estimated w.r.t the wheel base center, at each time the value would be somewhere in the middle of all the wheel speed values. Additionally it can be concluded that the estmated output appears to be less noisy than the input wheel speed signals.
![](./readme_artifacts/5_velocity_comparison.PNG)
![](./readme_artifacts/6_velocity_comparison.PNG)
<br>

[Back to TOC](#t0)
<br> 


### 4. Conclusion  <a name="t4"></a>
Overall the presented approach for ego-motion estimation looks promising and also computationally efficient.
<br>

[Back to TOC](#t0)
<br>
