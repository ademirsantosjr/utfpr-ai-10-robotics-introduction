# Mapping in Robotics: An Overview

Mapping is an essential function for mobile robots, allowing them to create a representation of the environment in which they operate. Just as humans use maps for navigation and route planning, robots rely on maps to understand the space around them, plan their actions, and perform tasks autonomously.

## The Importance of Maps for Mobile Robots

- **Environment Representation:** Maps serve as an internal representation of the environment, recording information about obstacles, free navigation areas, and the location of objects of interest.
- **Planning and Navigation:** With a map, the robot can plan efficient and safe trajectories, avoiding collisions and reaching its goals.
- **Localization:** The map is fundamental for the robot to estimate its own position and orientation in the environment, a process known as localization.
- **Human-Robot Interaction:** Maps facilitate communication between humans and robots, allowing operators to visualize the robot's location, trajectory, and the state of the environment.

## Types of Maps

There are two main categories of maps used in robotics: **metric** and **topological**.

### Metric Maps

Metric maps provide a detailed spatial representation of the environment, capturing the geometry and dimensions of objects and free space.

- **Occupancy Grid:** The most common form of a metric map is the occupancy grid. In this model, the environment is divided into a grid of regular cells (in 2D or 3D), where each cell stores the probability of being occupied by an obstacle.
    - **Advantages:**
        - Faithful and easy-to-visualize representation of the environment.
    - **Disadvantages:**
        - High memory consumption, especially in large environments or with high resolution.

To optimize memory usage, other representations can be used, such as extracting geometric features (lines, planes) to describe the environment more concisely.

### Topological Maps

Topological, or relational, maps offer a higher level of abstraction, focusing on the relationships between different locations or landmarks in the environment.

- **Graphs:** They are generally represented by a graph, where the **nodes** correspond to places of interest (e.g., rooms, corridors) and the **edges** indicate connectivity or the possibility of moving between these locations.
    - **Advantages:**
        - Low memory consumption.
        - Efficient for high-level planning tasks.
    - **Disadvantages:**
        - Less geometric detail of the environment.

The edges of the graph can contain additional information, such as the distance between nodes or navigation instructions ("turn left," "go straight for 10 meters").

## Hybrid Approaches

It is common to find systems that combine both approaches. For example, a robot might use an occupancy grid map for local navigation and obstacle avoidance in its immediate vicinity, while a topological map is used for large-scale route planning.

The choice of map type depends on the specific application of the robot, the available computational resources, and the level of detail required for the execution of its tasks.
