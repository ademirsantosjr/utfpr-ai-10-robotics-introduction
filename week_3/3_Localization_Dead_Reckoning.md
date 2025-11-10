# Localization with Dead Reckoning

**Dead Reckoning** is one of the most fundamental techniques for robot localization. The core idea is simple: starting from a known initial position, the new position is estimated based on speed, direction, and elapsed time.

> **In essence:** If you know where you were, where you went, and at what speed, you can calculate where you are now.

This technique relies on **proprioceptive sensors**, which measure the internal state of the robot, such as:

-   **Wheel Encoders:** Measure the rotation of the wheels to calculate the distance traveled.
-   **Inertial Measurement Unit (IMU):** A combination of:
    -   **Accelerometers:** Measure linear acceleration.
    -   **Gyroscopes:** Measure angular velocity (rate of rotation).

## The Problem: Uncertainty and Error Accumulation

The main weakness of Dead Reckoning is the **accumulation of errors**. Both the sensors and actuators of a robot are imperfect and suffer from noise and inaccuracies:

-   **Sensor Noise:** Small fluctuations in the readings from encoders or the IMU.
-   **Actuator Imprecision:** An order for the motor to turn at a certain speed may not be executed perfectly (e.g., the robot may slip).

Since Dead Reckoning calculates the current position based on the previous estimate, these small errors are summed up at each step. Over time, the accumulated error grows without bounds, and the robot's estimated position drifts further and further away from its actual position.

### Illustration of the Problem

Imagine a robot programmed to move in a circle. The blue line represents the actual (true) trajectory, and the red line represents the trajectory estimated using only Dead Reckoning.

-   **At the beginning:** The estimate (red) is very close to reality (blue).

<p align="center">
  <img src="https://i.imgur.com/Lp7G0w5.png" alt="Start of Dead Reckoning" width="500"/>
</p>

-   **Over time:** The error accumulates. The estimated trajectory deviates significantly from the actual trajectory. The robot "thinks" it is in one place, but it is actually in another, and this difference only increases.

<p align="center">
  <img src="https://i.imgur.com/9z7x08Y.png" alt="End of Dead Reckoning" width="500"/>
</p>

## Conclusion: A Necessary but Insufficient Tool

Dead Reckoning is essential for estimating the robot's position over short time intervals, providing a continuous, high-frequency estimate. However, due to its cumulative and unbounded error, **it can never be used alone** for long-term localization.

The solution is to periodically correct the Dead Reckoning estimate using data from **exteroceptive sensors** (which measure the environment), such as GPS, cameras, LIDAR, or sonars. This combination of different data sources is known as **sensor fusion**, and it is the subject of more advanced techniques, such as the Kalman Filter and the Particle Filter.
