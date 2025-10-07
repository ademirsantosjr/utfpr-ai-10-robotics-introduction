# Sensors and Actuators: An Introduction

In a robotic system, interaction with the environment and self-perception are fundamental. The components that make this interaction possible are, in essence, the **sensors** and **actuators**, orchestrated by a **control system**.

## The Control Cycle in Robotics

A robot's operation can be understood through a continuous control cycle:

1.  **Sensing:** Sensors collect data about the robot's internal state (e.g., joint position, velocity) and/or the external environment (e.g., presence of obstacles, temperature).
2.  **Control:** The information from the sensors is sent to a control system. This system processes the data, makes decisions based on its programming and the task's objectives.
3.  **Actuation:** Based on the decisions made, the control system sends commands to the actuators.
4.  **Action:** The actuators (motors, grippers, etc.) execute the commands, resulting in movement or some form of interaction with the environment.

This cycle repeats continuously, allowing the robot to perceive, decide, and act autonomously.

![Robotic Control Cycle](https://i.imgur.com/G5fAS1B.png)

## Deepening into Sensors

Sensors are devices that allow a robot to extract information about itself and its surrounding environment. They are also known as **transducers**, as their main function is to convert one form of energy (such as light, heat, or pressure) into another, usually an electrical signal that the control system can interpret.

### Sensor Classification

To better understand the vast range of existing sensors, we can classify them in two main ways:

#### 1. Regarding Energy Emission

-   **Active Sensors:** Emit a pulse of energy (like sound or light) and measure the signal that returns after interacting with the environment.
    -   **Examples:** Sonar, LASER (LIDAR).

-   **Passive Sensors:** Do not emit their own energy. They only measure the energy already available in the environment.
    -   **Examples:** Cameras (which capture ambient light), temperature sensors.
    > _Note: A camera with a flash can be considered active at the moment the flash is fired._

#### 2. Regarding the Measurement Object

-   **Proprioceptive Sensors:** Perform measurements of the robot's own internal parameters. They report on the state of the robot.
    -   **Examples:** *Encoders* (measure the rotation of a shaft/motor), accelerometers, gyroscopes (which make up an IMU - *Inertial Measurement Unit*).

-   **Exteroceptive Sensors:** Perform measurements of the external environment of the robot.
    -   **Examples:** Cameras, GPS receivers, microphones.

The ability to make decisions, from the simplest to the most complex, depends directly on the quality and relevance of the information collected by these sensors.

## References

-   ROMERO, R. et al. **Robótica Móvel**. 1 ed., 2014.
-   SICILIANO, B. et al. **Robotics: Modelling, Planning and Control**. 2009.
-   SIEGWART, R. et al. **Introduction to Autonomous Mobile Robots**. 2 ed., 2004.
