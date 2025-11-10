
# Kinematic Control for Wheeled Robots

This document details the implementation of a kinematic controller for a mobile robot with a *differential drive* configuration. The objective is to move the robot from its current position to a target point (waypoint) autonomously.

## Robot Model and Variables

We assume a *differential drive* robot, where two independently controlled wheels allow for movement. If both wheels turn at the same speed, the robot moves in a straight line; different speeds result in curves.

### State and Actuation Variables

To design the controller, we define the following variables:

- **Current Robot Location:**
  - Position: `p = [x, y]`
  - Orientation: `θ` (angle around the Z-axis)

- **Target Point (Waypoint) Location:**
  - Desired Position: `p_d = [x_d, y_d]`

- **Actuation Commands (Controller Outputs):**
  - Translational Velocity: `v`
  - Rotational Velocity: `ω`

We assume that a low-level controller already present in the robot is capable of driving the motors to achieve the commanded velocities `v` and `ω`.

## Derivation of Errors for Control

The core of closed-loop control is the calculation of the error. For our robot, we need two distinct errors: one for position and one for orientation.

![Control Schematic](https://i.imgur.com/5aL3nAN.png)
*Illustration of the variables and errors involved in the robot's control.*

1.  **Position Error (`d`):**
    - It is the Euclidean distance between the robot's current position and the target point.
    - Calculated as: `d = sqrt((x_d - x)² + (y_d - y)¹)`.
    - This error will be the input to the translational velocity controller. The idea is that the greater the distance, the greater the velocity `v` should be.

2.  **Orientation Error (`α`):**
    - Simply moving forward does not guarantee that the robot will reach the target. It first needs to **orient itself** in the correct direction.
    - The **desired orientation (`θ_d`)** is the angle of the vector connecting the robot's current position to the target point.
    - The orientation error, `α`, is the difference between the desired orientation and the robot's current orientation: `α = θ_d - θ`.
    - This error will be the input to the rotational velocity controller. The robot will use the velocity `ω` to turn until `α` is zero, aligning itself with the target.

## Controller Structure with Two PIDs

Based on the defined errors, we can design a control architecture using two independent PID controllers:

1.  **Position PID:**
    - **Input:** Distance error `d`.
    - **Output:** Translational velocity `v`.
    - **Objective:** Reduce the distance to the target.

2.  **Orientation PID:**
    - **Input:** Orientation error `α`.
    - **Output:** Rotational velocity `ω`.
    - **Objective:** Align the robot with the target point.

Together, these controllers work so that the robot first aligns with the target and then moves towards it until it is reached. The process is continuous, dynamically correcting the route.

## Challenge: PID Gain Tuning

The system's performance critically depends on the tuning of the gains (Kp, Ki, Kd) of both PID controllers. Finding the ideal values can be a manual, time-consuming process based on trial and error.

A more systematic approach is to use **optimization algorithms** to find the best gains automatically. Bio-inspired techniques, such as **Genetic Algorithms (GA)**, are effective for this task, exploring the parameter search space to find a combination that optimizes the robot's performance (e.g., minimizing arrival time and error).
