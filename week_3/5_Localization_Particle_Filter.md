# Localization with Particle Filter

The **Particle Filter** is another advanced and powerful technique for robot localization in non-linear systems. Like the EKF, it is a recursive algorithm that fuses data from multiple sensors, but its approach is fundamentally different and, in many cases, more flexible.

## The Core Idea: Tracking Probability with Particles

While the EKF assumes that the system's uncertainty can be well-represented by a Gaussian distribution (a single error ellipse), the Particle Filter is a **non-parametric** method. This means it makes no assumptions about the shape of the probability distribution.

Instead, it represents the belief about the robot's position using a set of **particles**. Each particle is a complete hypothesis of the robot's state (e.g., a pose `[x, y, θ]`). A dense cloud of particles in a certain region means that the filter believes there is a high probability that the robot is there.

<p align="center">
  <img src="https://i.imgur.com/b0gYf2L.png" alt="Particle Filter Concept" width="500"/>
</p>

This approach allows the filter to represent complex and multimodal probability distributions (for example, when a robot is in a long corridor and could be in several places at the same time).

## The Steps of the Particle Filter

The filter operates in a continuous four-step cycle:

1.  **Initialization:** A number `N` of particles are created. Initially, if the robot's position is unknown, the particles are spread uniformly across the map. Each particle starts with an equal weight.

2.  **Prediction (Motion):** Each particle is individually moved according to the robot's motion model (e.g., Dead Reckoning), with the addition of random noise. This simulates the uncertainty in the robot's movement and causes the particle cloud to spread out.

3.  **Update (Weighting):** This is the correction step. For each particle, the filter compares the expected measurement from that hypothesis with the actual measurement from the sensors (e.g., distance to a landmark, a laser reading). Particles that predict measurements closer to the real ones receive a **higher weight**. Those that are inconsistent with the measurements receive a lower weight.

4.  **Resampling:** After a few iterations, many particles may end up with near-zero weights, becoming useless. Resampling solves this: a new set of `N` particles is drawn from the old set, where the probability of a particle being chosen is proportional to its weight. This effectively eliminates bad hypotheses (low-weight particles) and concentrates the particles in high-probability areas (where the high-weight particles were).

## Particle Filter in Action

In the simulation, the particle filter fuses **Dead Reckoning** with measurements of **distance to landmarks** with known positions in the environment.

-   **Estimated Trajectory:** The Particle Filter's estimate (red line) tracks the real trajectory (blue) with very high precision, overlapping it most of the time. The drift of the Dead Reckoning (black) is clearly corrected.

<p align="center">
  <img src="https://i.imgur.com/YvW3j3G.png" alt="Trajectory with Particle Filter" width="500"/>
</p>

-   **Position Error Analysis:** The error graph confirms the method's effectiveness. The position error of the Particle Filter (blue) remains consistently close to zero, much lower than the growing error of the Dead Reckoning (black).

<p align="center">
  <img src="https://i.imgur.com/5aR3E0f.png" alt="Position Error with Particle Filter" width="600"/>
</p>

## Conclusion: EKF vs. Particle Filter

-   The **EKF** is computationally lighter and works very well for systems that are "almost" linear and have Gaussian uncertainties.
-   The **Particle Filter** is more robust and can handle any type of probability distribution and highly non-linear systems. Its main disadvantage is the computational cost, which increases with the number of particles needed for a good estimate.

Both are essential tools in modern robotics for solving the localization problem, allowing robots to navigate autonomously and reliably in complex environments.
