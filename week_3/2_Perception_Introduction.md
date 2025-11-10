# Perception in Robotics: The Challenge of Localization

**Perception** is the function that allows a robot to collect and process information about itself and its surrounding environment. This capability is the foundation for any intelligent and autonomous action. Perception involves two main stages:

1.  **Sensor Selection:** Choosing the appropriate sensors for the robot's task (cameras, sonars, LIDAR, encoders, etc.).
2.  **Signal Processing:** Developing algorithms to extract useful information from raw sensor data.

The information extracted by perception is used for various purposes:

-   **Updating the knowledge base:** Transforming data into symbols so the robot can "understand" the environment.
-   **Recognizing objects:** Identifying items with which the robot needs to interact.
-   **Triggering reflex actions:** Such as dodging an obstacle.
-   **Determining its own state:** Knowing its position, orientation, and velocity.

## The Fundamental Problem: Localization

Among all perception tasks, **localization** is one of the most critical for any mobile robot. Without knowing where it is, a robot cannot navigate autonomously, plan routes, or perform tasks reliably.

> **Localization** is the process of determining the position and orientation of a robot at a given moment in time, usually in relation to a reference coordinate system (inertial).

### Representing Position and Orientation (Pose)

A robot's "pose" is the combination of its position and orientation. The way we represent it depends on the environment in which the robot moves.

#### 2D Motion (Plane)

For robots moving on a flat surface, such as wheeled robots, the pose is defined by:

-   **Position (Translation):** A vector `p = [px, py]` representing the robot's coordinates on the X and Y axes.
-   **Orientation (Rotation):** An angle `θ` (theta), also known as *heading*, which indicates the direction the robot is pointing, measured in relation to one of the axes.

<p align="center">
  <img src="https://i.imgur.com/yq5xU3b.png" alt="2D Pose" width="400"/>
</p>

#### 3D Motion

For robots moving in three-dimensional space, such as drones or robotic arms, the representation is more complex:

-   **Position (Translation):** A vector `p = [px, py, pz]` with the coordinates on the X, Y, and Z axes.
-   **Orientation (Rotation):** Usually represented by **Euler Angles**, which are three rotation angles around the robot's own body axes:
    -   **Roll:** Rotation around the X-axis.
    -   **Pitch:** Rotation around the Y-axis.
    -   **Yaw:** Rotation around the Z-axis (equivalent to *heading* in 2D).

<p align="center">
  <img src="https://i.imgur.com/c5hF1fW.png" alt="3D Pose" width="450"/>
</p>

Solving the localization problem is the first step for a robot to navigate intelligently. The next sections will cover the techniques used to estimate the robot's pose, such as:

-   **Dead Reckoning (Odometry)**
-   **Kalman Filter**
-   **Particle Filter**
