# Classification of Robots by Level of Autonomy

In addition to the classification by mechanical structure (manipulators vs. mobile), robots can be categorized by their **level of autonomy**, which defines the degree of independence in relation to a human operator. This classification also reflects the historical evolution of robotics.

It is important to understand that these levels are not rigid categories, but rather a **continuous spectrum**. The same robot can be classified in different ways depending on the context or the subjectivity of the analysis.

## 1. Control and Predefined Actions

This is the most basic level of automation.

-   **Operation**: The robot executes a sequence of pre-programmed actions continuously and repetitively.
-   **Dependence**: It requires a fully controlled environment and the constant supervision of a human operator. Any unexpected variation in the environment can lead to operational failures.
-   **Example**: Industrial robots on an assembly line that weld the same part in the same place repeatedly.

## 2. Teleoperated Robots

At this level, the robot acts as a remote extension of the operator.

-   **Operation**: All actions and decisions are made in real time by a human operator, who controls the robot at a distance through an interface (joystick, controls, etc.).
-   **Dependence**: The robot is 100% dependent on the operator. It requires a low-latency communication system (short response time).
-   **Example**: Bomb disposal robots, manually controlled inspection drones, and surgical robots where the doctor controls every movement.

## 3. Semi-autonomous Robots

This level represents a middle ground, where the robot and the human share control of the task.

-   **Operation**: The robot is capable of executing subtasks independently, but still depends on a human operator to make high-level decisions or define the main objectives.
-   **Dependence**: The operator defines "what" and "where," while the robot figures out "how" to execute parts of the task.
-   **Example**: A logistics robot in a warehouse that receives the command "go from point A to point B". The robot plans the route, avoids obstacles, and executes the displacement autonomously, but the initial decision to go from A to B was human.

## 4. Autonomous Robots

This is the highest level of independence, and the ultimate goal of many projects in robotics and AI.

-   **Operation**: The robot is capable of executing complex tasks from start to finish, making all necessary decisions without any human intervention.
-   **Dependence**: Ideally, none. The robot perceives its environment, plans its actions, deals with unforeseen events and failures, and learns from new situations to achieve its goal.
-   **Example**: a fully autonomous car (Level 5) that can take a passenger to any destination in any condition, or a Mars exploration robot that conducts its scientific mission independently.

## The Role of Artificial Intelligence in Autonomy

The search for higher levels of autonomy is directly linked to **Artificial Intelligence (AI)**. Robots considered **intelligent** use AI techniques to:

-   **Advanced Planning**: Generate complex sequences of actions to achieve a goal.
-   **Dealing with Uncertainties**: Operate in unstructured and dynamic environments, where not everything is known a priori.
-   **Learning and Adaptation**: Learn from experience to improve performance and make more effective decisions in the face of new situations or failures.

Quanto mais inteligente um robô, maior seu potencial para se aproximar da autonomia completa, tornando-se verdadeiramente independente da supervisão humana.
