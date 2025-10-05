# Types of Robots: Mobile

Continuing the classification of robots based on mechanical structure, this document addresses **mobile robots**, characterized by a base that moves in space, carrying all its components.

Locomotion is the main criterion for subclassifying them:

-   **Terrestrial**: Wheeled and legged vehicles.
-   **Aerial**
-   **Aquatic**

## 1. Terrestrial Vehicles

### Wheeled Vehicles

These are robots with a rigid base and a system of wheels in constant contact with the ground. They are very efficient on flat and uneven surfaces, such as floors and asphalt.

#### Wheel and Locomotion Configurations

-   **Differential Drive**: Two wheels on the same axle, controlled by independent motors. It allows going forward (same speed) and making turns (different speeds). It is a simple and popular configuration.
-   **Ackermann Steering**: Configuration analogous to that of a car, with two fixed rear wheels and two steerable front wheels. It allows for greater load capacity and speed, but has maneuvering restrictions (it is not omnidirectional).
-   **Omnidirectional Locomotion**: The ability to move in any direction at any time, regardless of the robot's orientation. This eliminates the need for complex maneuvers. It can be achieved with:
    -   **Three Caster Wheels**: Wheels that can be steered independently, allowing rotation on its own axis and movement in any direction.
    -   **Mecanum (Swedish) Wheels**: Wheels with passive rollers at 45°, which, when used together (usually four), allow lateral, diagonal, and rotational movement.
-   **Tracks**: Ideal for uneven terrain, as they increase the contact area with the ground, offering greater traction. However, they are less efficient on smooth surfaces and have difficulty making turns.

### Legged Vehicles

Inspired by living organisms, they are formed by multiple rigid bodies (links) and articulations (joints), similar to manipulators. They require more sophisticated control to maintain stability during movement.

#### Advantages over Wheeled Vehicles

-   **Terrain Versatility**: Capable of overcoming obstacles such as steps, crevices, holes, and sandy terrain.
-   **Self-Recovery**: Some models can get up on their own after a fall.
-   **Load Stability**: They can keep a platform (load) level even on inclined terrain.
-   **Less Environmental Impact**: The point contact of the "paws" with the ground causes less damage to the environment compared to wheels or tracks.

#### Classification by Number of Legs

-   **Monopod (1 leg)**: Stable only dynamically (needs to be in motion, usually jumping, to not fall).
-   **Biped (2 legs)**: Inspired by humans. Stability is challenging; often, the movement of the arms is used to counterbalance the movement of the legs.
-   **Quadruped (4 legs)**: Inspired by mammals. It is statically stable, that is, it can stand still in balance without effort.
-   **Hexapod (6 legs)**: Inspired by insects. It offers great stability and the ability to move several legs simultaneously, allowing high speeds.

## 2. Aerial Vehicles

Also known as **UAVs** (Unmanned Aerial Vehicles) or **RPAs** (Remotely Piloted Aircraft).

-   **Fixed Wings**: Similar to airplanes, they use the lift generated on the wings by a high flight speed. They are efficient for covering large areas, but need a runway or impulse to take off and cannot hover in the air.
-   **Rotary Wings (Multirotors)**: Drones and helicopters that use the rotation of propellers to generate lift. They can take off and land vertically and hover at a fixed point, which makes them ideal for inspection and filming.
-   **Balloons and Airships**: They use a gas less dense than air to float. They are slower, but can remain in the air for long periods.
-   **Flapping Wings**: Bio-inspired robots that mimic the flight of birds and insects. They are usually small and are still in the research and development phase.

## 3. Aquatic Vehicles

They use thrusters or buoyancy variation to move in the water.

-   **Surface**: They move on the water, like autonomous boats.
-   **Underwater**: They operate below the waterline, like autonomous submarines (AUVs - Autonomous Underwater Vehicles), used for seabed mapping, cable inspection, and research.
