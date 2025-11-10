# Architectures for Robotic Systems

In robotics, a software architecture defines the fundamental components of a system and the interactions between them. This structuring is crucial for organizing the complexity inherent in autonomous robots, dividing their functionalities into smaller, more manageable parts.

## The Classic Model of a Robotic System

The fundamental model of a robotic system is composed of three essential parts:

- **Sensors:** Responsible for capturing information from the environment (perception).
- **Control:** The "brain" of the robot, which processes sensor information and makes decisions.
- **Actuators:** The components that execute actions in the environment (movement).

<p align="center">
  <img src="https://i.imgur.com/937G4hB.png" alt="Robotic System Model" width="500"/>
</p>

To develop more intelligent robots with greater autonomy, we need to expand the "Control" block, detailing its functions through more sophisticated architectures.

## Hybrid Architecture: Reactive, Deliberative, and Interactive

This architecture combines the **reactive** and **deliberative** paradigms, which emerged at different times in the history of robotics, taking advantage of the strengths of each. It is structured in three hierarchical layers:

### 1. Reactive Layer

- **Function:** Handles reflex and fast-execution behaviors that respond directly to sensor stimuli, without planning.
- **Example:** A robot that dodges an obstacle as soon as its ultrasonic sensor detects proximity. The dodging action is an immediate reflex to the stimulus.
- **Characteristics:**
  - High-speed response.
  - Does not involve memory or complex planning.
  - Essential for safety and for the robot's immediate reactions.

### 2. Deliberative Layer

- **Function:** Responsible for tasks that require planning, use of memory, and past information to make more complex decisions.
- **Example:** After exploring an environment (using reactive behaviors to navigate), the robot receives the goal to "return to the starting point." For this, it needs to:
    1. Access its memory to know where it started.
    2. Plan a route from its current location to the start.
    3. Execute the route, while the reactive layer remains active to dodge unexpected obstacles.
- **Characteristics:**
  - Slower processing.
  - Uses internal world models and symbolic information (e.g., "starting point").
  - Allows the robot to achieve long-term goals.

Artificial Intelligence techniques are mainly applied in this layer, in functions such as:

- **Goal generation:** Defining what needs to be done.
- **Planning:** Selecting the best way to achieve the goals.
- **Execution:** Implementing the planned actions.
- **Monitoring:** Tracking the execution and replanning if something unexpected occurs.

### 3. Interactive Layer

- **Function:** Manages the robot's interaction with other agents, such as humans, other robots, or computational systems.
- **Example:**
    - **Social Robots:** An educational robot that interacts with a child, needing to understand speech, interpret emotions, and respond appropriately.
    - **Swarm Robotics:** A group of robots that collaborates to perform a task, exchanging information to coordinate their actions.
- **Characteristics:**
  - Involves communication and social intelligence.
  - It is a more recent research area with many open challenges.

<p align="center">
  <img src="https://i.imgur.com/G5sF8mC.png" alt="Hybrid Architecture" width="400"/>
</p>

## Functional Architecture for Mobile Robots (NHC)

The **Nested Hierarchical Controller (NHC)** architecture is a functional model designed for mobile robots, but its principles can be applied to other systems, such as manipulator arms. It divides the system into three main blocks: **Sensing**, **Planning**, and **Actuation**.

<p align="center">
  <img src="https://i.imgur.com/23i3g2W.png" alt="NHC Architecture" width="600"/>
</p>

### Components of the NHC Architecture

1. **Sensing:**
   - The **sensors** collect data from the environment and the robot itself.
   - This information feeds a **World Model (or Knowledge Base)**, which centralizes everything the robot "knows." This model can contain everything from raw sensor data to pre-defined maps and symbolic information.

2. **Planning (Hierarchical):**
   - **Mission Planner (High Level):** Defines the general goals of the application. Ex: "Navigate to object X."
   - **Navigator (Intermediate Level):** Receives the goal from the planner and builds an obstacle-free trajectory to reach it, using the World Model to know the environment.
   - **Pilot (Low Level):** Receives the trajectory from the navigator and transforms it into movement commands for the actuators. This is where reactive behaviors (like dodging an immediate obstacle) are implemented, as it requires a quick response.

3. **Actuation:**
   - **Low-Level Control:** Receives commands from the pilot (e.g., "rotate the left wheel at 10 rpm") and converts them into electrical signals for the **actuators** (motors), ensuring that the movement is executed correctly.

This cycle (perception -> planning -> action) repeats continuously, but each component operates at its own frequency. The pilot, for example, needs a much faster execution cycle than the mission planner, ensuring quick reactions to unexpected events.
