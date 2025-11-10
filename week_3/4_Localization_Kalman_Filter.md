# Sensor Fusion with the Extended Kalman Filter (EKF)

As we've seen, Dead Reckoning suffers from error accumulation, making it unreliable in the long run. The solution to this problem is **sensor fusion**, a technique that combines readings from multiple sensors to obtain a more accurate and robust estimate than would be possible with a single sensor.

One of the most classic and powerful tools for this is the **Kalman Filter**.

## The Kalman Filter: An Overview

The Kalman Filter is a recursive algorithm that estimates the state of a dynamic system from a series of incomplete or noisy measurements. It is considered **optimal** for **linear** systems with Gaussian noise, as it provides the best possible estimate under these conditions.

The filter operates in a two-step cycle:

1.  **Prediction:** The filter uses the system model (similar to Dead Reckoning) to predict the next state and its uncertainty. This is the *a priori* estimate.
2.  **Update (Correction):** The filter receives a new measurement from an external sensor (like a GPS) and its respective uncertainty. It then calculates the **Kalman Gain**, which acts as a weight to decide how much to trust the prediction and how much to trust the new measurement. Finally, it corrects the prediction to generate a new, more accurate *a posteriori* estimate.

### The Challenge: Non-Linear Systems

The problem is that most robotic systems, especially robot motion, are **non-linear** (involving sines, cosines, etc.). This prevents the direct application of the standard Kalman Filter.

## The Solution: The Extended Kalman Filter (EKF)

The **Extended Kalman Filter (EKF)** is the most common variant of the filter, designed specifically for non-linear systems. The core idea of the EKF is to **linearize** the system at each time step, approximating the non-linear function with a straight line (using Jacobians, which are first-order derivatives) around the current estimate. Once the system is approximated as linear, the Kalman Filter's prediction and update cycle can be applied.

## EKF in Action: Correcting Dead Reckoning with GPS

Let's visualize the power of the EKF with the simulation example, where the goal is to fuse data from two types of sensors:

-   **Proprioceptive Sensors (Dead Reckoning):** Provide a high-frequency estimate, but with accumulating error.
-   **Exteroceptive Sensor (GPS):** Provides an absolute position measurement, which does not accumulate error but is noisy and has a lower frequency.

The result of the fusion with the EKF is remarkable:

-   **Estimated Trajectory:** The red line (EKF) stays very close to the real trajectory (blue), successfully correcting the drift of the Dead Reckoning (black) using the noisy GPS measurements (green dots).

<p align="center">
  <img src="https://i.imgur.com/YvW3j3G.png" alt="Trajectory with EKF" width="500"/>
</p>

-   **Position Error Analysis:** The error graph clearly shows the superiority of sensor fusion.
    -   The error of the **Dead Reckoning (black)** grows continuously over time.
    -   The error of the **GPS (green)** is noisy but remains bounded (it does not accumulate).
    -   The error of the **EKF (blue)** is significantly smaller than that of either sensor alone and remains low and stable over time.

<p align="center">
  <img src="https://i.imgur.com/5aR3E0f.png" alt="Position Error with EKF" width="600"/>
</p>

### Conclusion

The Extended Kalman Filter is a fundamental technique in robotics for achieving accurate and reliable localization. By fusing the high-frequency, drift-prone estimates from Dead Reckoning with the absolute, noisy measurements from sensors like GPS, the EKF manages to get the best of both worlds, resulting in a state estimate far superior to what either sensor could provide alone.
