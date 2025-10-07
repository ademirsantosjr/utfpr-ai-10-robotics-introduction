# Proprioceptive Sensors: The Robot's Self-Perception

Proprioceptive sensors are those that measure the internal parameters of the robot, providing crucial information about its own state, such as position, orientation, and velocity. Let's explore the most common ones.

## 1. Odometers and Optical Encoders

**Optical encoders**, often called odometers in mobile robots, are devices that estimate the angular displacement of a motor.

-   **How they work:** They use a disk with opaque and transparent sections attached to the motor shaft. A photoemitter sends light through the disk, and a photoreceiver on the other side detects the light pulses. Counting these pulses allows the rotation angle to be calculated.

-   **Applications:**
    -   **Manipulator Robots:** They measure the displacement of rotary joints, allowing the configuration of the robotic arm to be calculated.
    -   **Mobile Robots:** Attached to the wheel motors, they measure their rotation to estimate the distance traveled.

-   **Limitation:** In mobile robots, the distance estimate can accumulate errors over time due to skidding or slipping. Therefore, it is only accurate for short displacements and is often corrected with data from other sensors.

## 2. Gyroscopes

**Gyroscopes** measure the angular velocity of a body. In robotics, they are essential for determining the robot's orientation.

-   **Coordinate Frames:**
    -   The measurements are made in relation to a **coordinate system fixed to the robot's body** (which moves with it).
    -   This rotation measurement is calculated in reference to an **inertial coordinate system**, which is fixed in relation to the Earth.

-   **Rotation Angles (Attitude):** The rotations around the X, Y, and Z axes of the robot's body are called, respectively, **Roll**, **Pitch**, and **Yaw**.
    -   In planar robots (like cars), the main interest is in the **Yaw**, also called **Heading**, which indicates the direction the robot is pointing.

-   **Calculation of Angular Position:** By integrating the angular velocity measured by the gyroscope over time, it is possible to obtain the change in the robot's angular position (orientation).

-   **Limitation (Drift):** Small measurement errors (bias) from the gyroscope, when integrated, accumulate, generating a growing error in the orientation estimate. This phenomenon is known as *drift*.

## 3. Accelerometers

**Accelerometers** measure linear acceleration. However, they measure the sum of all forces acting on the body, which includes both the acceleration of the robot's movement and the **acceleration of gravity**.

-   **How they work:** To obtain the actual acceleration of the movement, it is first necessary to know the robot's orientation (obtained by a gyroscope) in order to subtract the gravity vector from the total measurement.

-   **Calculation of Velocity and Position:** Once the acceleration of the movement is isolated, it can be integrated once to obtain the velocity and a second time to obtain the position.

-   **Limitation:** As with gyroscopes, the double integration amplifies measurement errors, causing the position estimate to degrade rapidly.

## The Integrated Solution: IMU (Inertial Measurement Unit)

The most common way to find these sensors is on a single board called an **IMU (Inertial Measurement Unit)**. An IMU combines:

-   **3 Gyroscopes:** One for each orthogonal axis (X, Y, Z), measuring angular velocity omnidirectionally.
-   **3 Accelerometers:** One for each orthogonal axis, measuring acceleration in the same way.

This combination allows for a more robust estimate of the robot's **attitude (orientation)**, **velocity**, and **position**. The system that processes this data to provide a complete navigation solution is called an **INS (Inertial Navigation System)**.

### Complementarity with GPS

Due to the *drift* problem, IMUs are often used in conjunction with **GPS** sensors:

-   **IMU:** Provides data at a high frequency (100-300 Hz), but with cumulative error.
-   **GPS:** Provides absolute position data at a low frequency (1-5 Hz), without cumulative error.

The fusion of data from both sensors (using algorithms such as the Kalman Filter) allows combining the high update rate of the IMU with the absolute precision of the GPS, obtaining an accurate and high-frequency location and orientation estimate.

### MEMS Technologies

The miniaturization of gyroscopes and accelerometers was made possible by **MEMS (Micro-Electro-Mechanical Systems)** technology, which integrates mechanical and electrical components on a microscale, making these sensors cheap and ubiquitous in smartphones, drones, and robots.
