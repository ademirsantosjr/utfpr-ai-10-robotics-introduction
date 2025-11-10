
# Kinematic Control in Robotics: An Introduction

Motion control is a fundamental pillar of robotics, enabling robots to perform tasks autonomously and precisely. This document explores the introductory concepts of kinematic control, focusing on how robots plan and execute their movements.

## Control Architecture: The NHC Model

To understand how a robot moves, we can use the *Nested Hierarchical Controller (NHC)* architecture. It organizes the robot's functions into hierarchical layers:

- **Sensing:** Collects data from the environment through sensors, which update the robot's "world model"—its knowledge base.
- **Mission Planner:** Defines the high-level tasks the robot must accomplish.
- **Navigator:** Receives the tasks and translates them into physical displacement, determining the route to be followed.
- **Pilot:** Executes the route defined by the navigator, controlling the actuators to perform the movement.

Our study focuses on the **Pilot** layer, which is responsible for the motion control itself.

## Path vs. Trajectory

In motion planning, two concepts are essential, although often used as synonyms:

- **Path:** Refers to the sequence of positions the robot must follow. It is a purely **geometric** description of the course (e.g., a straight line followed by an arc).
- **Trajectory:** It is the path with the addition of the **temporal** dimension. It specifies *when* the robot should be at each point on the path, defining not only the position but also the necessary **velocity** and **acceleration**.

A trajectory is, therefore, a more complete and complex specification than a simple path.

## Control Challenges for Different Types of Robots

Motion control varies significantly depending on the robot's morphology and operating environment:

| Robot Type | Control Challenges |
| :--- | :--- |
| **Manipulators** | - Control the joints to position the end-effector.<br>- Limit the force in interactions with objects to avoid damage. |
| **Legged Robots** | - Manage different types of locomotion (walking, running, trotting).<br>- Maintain balance and stability during movement. |
| **Aerial and Aquatic** | - Operate in a 3D space, controlling orientation (Euler angles).<br>- Stay within stable flight or navigation conditions. |
| **Wheeled Robots** | - Control orientation and velocity to follow paths or trajectories.<br>- Control is simplified, as they generally operate on a plane and are already stable. |

Due to their relative simplicity and stability, **wheeled robots** are an excellent starting point for studying the fundamentals of motion control.

## Kinematics vs. Dynamics

Motion control can be approached in two ways:

1.  **Kinematic Control:** Focuses on the motion without considering the forces that cause it. It only takes into account the geometric and temporal properties (position, velocity, acceleration).
2.  **Dynamic Control:** Studies the forces and torques necessary to generate the motion. It is a more complex approach that considers the robot's mass, motor torque, and external forces like friction and drag.

To build a solid foundation in the main concepts of motion control, this study will focus on **kinematic control**, which offers a clear understanding of the essential principles in a more direct way.
