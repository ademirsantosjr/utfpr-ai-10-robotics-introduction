# Actuators: Bringing Movement to Life

If sensors are the robot's "senses," then **actuators** are its "muscles." They are the ones that convert energy (usually electrical) into movement, allowing the robot to manipulate objects, move around, and physically interact with the environment. In modern robotics, **electric motors** are the predominant actuators.

Let's explore the three main types.

## 1. Direct Current (DC) Motors

DC motors are the most common choice for the locomotion of **wheeled robots**. They rotate continuously when a voltage is applied.

-   **Types:**
    -   **Brushed:** Older and lower-cost model, but with greater internal friction and wear, making it less efficient.
    -   **Brushless:** More modern, efficient, and with less wear, but at a higher cost. They are the preference in projects that demand higher performance and durability.

-   **Control:** DC motors are not connected directly to the processing unit. They require an intermediate circuit called an **H-Bridge** or a **motor driver**. This component allows for precise control of the **speed** (by varying the voltage) and the **direction of rotation** (by inverting the polarity).

## 2. Stepper Motors

This type of motor moves in discrete and precise "steps." Each electrical pulse sent to the motor corresponds to a fixed angular increment.

-   **How it works:** Control is done in an **open loop**, meaning it does not need a sensor to know its position. The position is inferred by counting the number of pulses sent from a known initial position.

-   **Characteristics:**
    -   **Pros:** Precise position control without the need for feedback (sensor).
    -   **Cons:** Can lose steps if the load is too high or the acceleration is too fast, leading to a position error that the system cannot detect.

-   **Applications:** They are not very common in mobile robots, but are often found in 3D printers, CNC machines, and sometimes in low-cost robotic manipulators.

## 3. Servomotors (Servos)

Servomotors are, perhaps, the most versatile and widely used actuators in robotics, from small projects to large industrial manipulators.

-   **How it works:** A servo is a complete **closed-loop** system. It is designed to move to a **specific angular position and hold it**. Internally, it consists of:
    1.  A motor (usually DC or AC for high loads).
    2.  A position sensor (an **encoder** or a potentiometer).
    3.  A control circuit.

-   **Position Control:** The control circuit compares the current position (read by the sensor) with the desired position (sent by a command). If there is a difference, it activates the motor to correct the error until the desired position is reached. Thanks to this continuous feedback, the servo actively resists external forces that try to move it from its position.

-   **Command (Small Servos):** Hobby servos are commonly controlled by **PWM (Pulse Width Modulation)** signals. The width of the pulse in a 20ms cycle determines the desired angular position (e.g., 1ms for 0°, 1.5ms for 90°, 2ms for 180°).

-   **Applications:**
    -   Rotary and prismatic joints of robotic arms.
    -   Grippers and end-effectors.
    -   Control surfaces in aircraft and aquatic vehicles (ailerons, rudders).

## Mechanical Energy Transfer: Torque vs. Speed

Electric motors typically operate at **high speed and low torque**. However, many robotic applications (such as lifting a heavy object) require the opposite: **low speed and high torque**.

To adapt the motor's characteristics to the application's needs, **mechanical transmission systems** are used:

-   **Gearboxes:** Increase torque and reduce speed. They are ubiquitous in robotics.
-   **Ball Screws:** Convert the motor's rotational motion into precise, high-force linear motion. They are the basis for the construction of **prismatic joints**.
-   **Belts and Chains:** Transfer motion from one axis to another, allowing flexibility in the positioning of motors in the robot's body.

Understanding the capabilities and limitations of actuators and transmission systems is fundamental to the design of a robot and to the decision-making of its control system, ensuring that the commands sent can, in fact, be executed in the real world.
