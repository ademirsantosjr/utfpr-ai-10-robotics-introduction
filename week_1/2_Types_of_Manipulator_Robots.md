# Types of Robots: Manipulators

Robots can be classified based on their mechanical structure, resulting in two main categories: **manipulator robots** and **mobile robots**. This document focuses on manipulators.

It is important to note that, although this classification is useful for study, there are hybrid robots that combine characteristics of both categories.

## Manipulator Robots

Manipulator robots, also known as robotic arms, are characterized by having a **fixed base** from which they extend to interact with the environment. All robot movement occurs around this base.

### Structure

The structure of a manipulator is composed of three main elements:

1.  **Links**: Rigid bodies that form the structure of the arm.
2.  **Joints**: Connections that unite the links and allow relative movement between them.
3.  **End-Effector**: The tool attached to the end of the arm, designed to perform the robot's specific task.

The movement of the manipulator is the result of the coordinated action of the joints, which move the links to position the end-effector at the desired location.

### Types of Joints

There are several types of joints, but the two most common are:

-   **Rotational (or Revolute) Joint**: Allows a **rotation** between two links, similar to the articulation of an elbow or shoulder.
-   **Prismatic (or Sliding) Joint**: Allows a linear **translation** movement between two links, where one slides over the other.

### End-Effector

The effector is the "hand" of the robot and varies drastically depending on the application. Examples include:

-   Grippers (to pick up and move objects)
-   Welding torches
-   Electromagnets
-   Painting or drilling tools

## Classification of Manipulators

Manipulators are subdivided based on their connection architecture, known as a kinematic chain.

### 1. Serial Manipulators

-   **Open Kinematic Chain**: They have a single sequence of links and joints connecting the base to the end-effector.
-   **Structure**: Imagine a single path from the base to the tip of the arm. Most common industrial robots follow this model.
-   **Example**: A robotic arm with multiple revolute joints, where each link is connected to the next in a line.

### 2. Parallel Manipulators

-   **Closed Kinematic Chain**: They have multiple "arms" (sequences of links) that connect the base to a single platform where the effector is mounted. This creates loops or closed circuits in the structure.
-   **Structure**: There are multiple paths from the base to the end-effector.

#### Comparison: Serial vs. Parallel

| Characteristic | Parallel Manipulators | Serial Manipulators |
| :--- | :--- | :--- |
| **Stiffness** | Higher (due to the multi-support structure) | Lower |
| **Speed** | Generally faster and with greater acceleration | Generally slower |
| **Workspace** | Smaller and more complex | Larger and simpler to calculate |
| **Accuracy** | Potentially higher | Lower (errors accumulate along the chain) |
| **Payload** | Higher in relation to its weight | Lower in relation to its weight |

A disadvantage of parallel manipulators is that the movement of one link chain can restrict the movement of the others, limiting the total range of motion (reach) compared to serial manipulators.
