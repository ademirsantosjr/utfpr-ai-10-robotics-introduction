
# Implementation of Kinematic Control in Python

This document details the implementation of a Proportional-Derivative (PD) controller for the kinematic control of a wheeled robot, along with an approach to optimize its gains using Genetic Algorithms (GA).

## 1. PD Controller Implementation

For this problem, a **PD** controller was chosen instead of a full PID. The **Integral (I)** part was omitted because the system, as modeled, does not exhibit steady-state error. Adding the integral term would only slow down the response without providing any benefits.

The control is divided into two parts: one for **position** and one for **orientation**.

### Controller Code

The `motion_control` function implements the control laws. It calculates the distance (`d`) and orientation (`alpha`) errors and applies the proportional and derivative actions to determine the output velocities (`v` and `w`).

```python
# Controller parameters (initial gains)
K_P_POS = 0.1 # Proportional gain for position
K_D_POS = 0   # Derivative gain for position
K_P_ORI = 0.1 # Proportional gain for orientation
K_D_ORI = 0   # Derivative gain for orientation

def motion_control(xTrue, xWaypoint, previous_errors):
  # Position error (Euclidean distance)
  d = math.sqrt((xWaypoint[0]-xTrue[0,0])**2 + (xWaypoint[1]-xTrue[1,0])**2)

  # Reference orientation (angle to the target)
  reference_orientation = math.atan2(xWaypoint[1]-xTrue[1,0], xWaypoint[0]-xTrue[0,0])

  # Stopping criterion
  if d > 0.05:
    # Orientation error
    alpha = angles_difference(reference_orientation, xTrue[2,0])

    # PD control laws
    v = K_P_POS*d + K_D_POS*(d - previous_errors[0])/DT
    w = K_P_ORI*alpha + K_D_ORI*angles_difference(alpha, previous_errors[1])/DT

    previous_errors = [d, alpha]
  else:
    v = 0
    w = 0

  return np.array([[v], [w]]), reference_orientation, previous_errors
```

### Simulation with Low Gains

When running the simulation with the initial gains (`Kp = 0.1`), the result is unsatisfactory. The robot moves slowly and fails to reach the target point within the simulation time because the actuation "force" is too low.

![Animation with Low Gains](https://i.imgur.com/0BxBM7K.gif)
*Result of the simulation with low gains. The robot does not reach the target.*

## 2. Gain Tuning with Genetic Algorithm (GA)

The process of manually tuning the gains (trial and error) is time-consuming. To automate this task, we use a **Genetic Algorithm (GA)** with the `pygad` library.

The GA searches for the best combination of gains (`Kp_pos`, `Kd_pos`, `Kp_ori`, `Kd_ori`) that optimizes a **fitness function**. Since the GA works to maximize fitness, we use the **negative error** as the metric—minimizing the error is equivalent to maximizing its negative value.

### Fitness Function

Different metrics were explored for the fitness function:

- **`sum`:** Sum of position errors over time. Tends to favor very fast responses to minimize accumulated error.
- **`mean`:** Average of the errors. Seeks good overall performance throughout the trajectory.
- **`min`:** Smallest error after the transient response. Focuses on minimizing overshoot.

### Optimization Results

The GA finds different sets of gains depending on the metric used, resulting in distinct behaviors:

- **`sum` metric:** The GA found high proportional gains (`Kp_pos=4.9`, `Kp_ori=4.9`). This results in a **very fast and aggressive** response, with the velocities saturating at their maximum limits. The robot reaches the target in less than 2.5 seconds.

- **`mean` metric:** The GA found lower gains (`Kp_pos=0.9`, `Kp_ori=0.7`). The behavior is **slower and more oscillatory**, with a visible overshoot, but it still reaches the objective.

![Animation with Optimized Gains (Mean)](https://i.imgur.com/0BxBkrb.gif)
*Result with gains optimized by the mean metric. The robot overshoots the target but converges.*

## 3. Simulation vs. Reality: The Sim-to-Real Gap

A crucial point is the difference between the simplified simulation model and a more realistic environment (like the CoppeliaSim simulator or a physical robot).

- **Simplified Model:** Assumes the robot can change its velocities `v` and `w` **instantaneously**. It ignores the system's **dynamics** (forces, torques, acceleration, inertia).
- **Realistic Model (CoppeliaSim):** Includes a physics simulation. The motors take time to accelerate and decelerate, and the dynamics of the movement introduce oscillations and delays not present in the simple model.

When applying the aggressive gains (found with the `sum` metric) in CoppeliaSim, the robot exhibits considerable oscillation that was not visible in the Python simulation. This happens because the controller tries to correct the error too abruptly, but the real robot's dynamics prevent it from responding instantly.

### Conclusion

The use of Genetic Algorithms is a powerful tool for obtaining an **excellent starting point** for the controller gains. However, due to the *gap* between the simplified simulation and reality, **manual fine-tuning** is often necessary to adapt the found gains to the dynamic characteristics of the real system, ensuring stable and efficient behavior.
