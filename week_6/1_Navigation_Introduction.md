
# Robotic Navigation: An Introduction

Navigation is one of the fundamental tasks in robotics, allowing a robot to move autonomously from one point to another. This document covers the introductory concepts of navigation, its role within a robot's architecture, and the different challenges that arise based on the type of robot.

## The Role of Navigation in a Robot's Architecture

In a hierarchical control architecture, such as the **Nested Hierarchical Controller (NHC)**, navigation acts as a link between mission planning and the robot's low-level control.

- **Mission Planner:** Defines the robot's final objective (e.g., "go to the kitchen").
- **Navigator:** Receives the objective and determines the sequence of points (the path) that the robot must follow to reach that objective, avoiding obstacles.
- **Pilot:** Follows the sequence of points defined by the navigator, sending commands to the robot's actuators.

The navigator uses information from the **world model**, which is constantly updated by sensors, to understand the environment and plan a safe and efficient route.

## Types of Robots and Navigation Challenges

Path planning varies significantly depending on the robot's morphology and kinematics:

- **Manipulators and Legged Robots:** Require consideration of the **system's dynamics**. The forces and accelerations needed to move the joints and links are a critical factor in trajectory planning to avoid movements that the robot physically cannot perform.

- **Aquatic and Aerial Robots:** Planning is more complex due to operational constraints, such as maximum speeds for maneuvers and the need to maintain **attitude** (angular orientation) to ensure stability.

- **Wheeled Robots:** Generally, planning is simpler. They operate at lower speeds and have fewer restrictions. The main concern is the geometry of the path. However, it is crucial to differentiate between:
    - **Holonomic (Omnidirectional) Robots:** Can move in any direction from any position, which simplifies planning.
    - **Non-Holonomic Robots:** Have movement restrictions (e.g., a car cannot move sideways), which adds complexity to path planning.

## The Configuration Space

To solve the navigation problem systematically, we use the concept of **Configuration Space (C-Space)**.

The C-Space represents all possible states (configurations) that a robot can assume. A "configuration" is a set of values that describes the position of each part of the robot.

### Example: Manipulator Arm

Imagine a robotic arm with two rotating joints (`θ1` and `θ2`) that needs to move its end effector from a starting point to a final one, avoiding obstacles.

- **In the workspace (X, Y):** It is difficult to find a systematic solution, as the movement of one joint affects the position of the entire arm in a non-linear way. An intuitive solution can lead to collisions.

- **In the Configuration Space (C-Space):** The problem is transformed. Instead of thinking about the (X, Y) coordinates of the end effector, we think about the angles (`θ1`, `θ2`) of the joints.
    - The obstacles from the workspace are mapped to "forbidden regions" in the C-Space. These are the combinations of angles that would result in a collision.
    - The navigation problem is reduced to finding a continuous path from the starting point to the final point in the **free configuration space** (the area that does not contain obstacles).

### Advantages and Disadvantages

- **Advantage:** Simplifies the planning problem by transforming it into a search for a path in a new space.
- **Disadvantage (The Curse of Dimensionality):** The increase in the number of "degrees of freedom" (joints, in the example) increases the dimension of the C-Space. This can make the problem computationally expensive, with solutions that grow exponentially in complexity.

For learning purposes, we generally work with a reduced number of states to visualize and understand how planning algorithms work.
