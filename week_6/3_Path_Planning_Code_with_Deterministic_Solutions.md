
# Implementing Deterministic Path Planning Solutions

In this section, we will explore the practical implementation of deterministic search algorithms (Dijkstra, A*, and D* Lite) for path planning for a wheeled robot. The reference code is available in a Google Colab notebook, and here we will break down the concepts and results.

## Model Simplifications

To facilitate implementation, some simplifications are adopted in the robot's configuration space:

1.  **Holonomic Robot:** It is assumed that the robot is omnidirectional, meaning it can move from one grid cell to any of its direct neighbors. Even if a real robot is not holonomic (like a car), this simplification is common in high-level planning. The complexity of executing the movements is delegated to the low-level kinematic controller.

2.  **Robot as a Point:** The robot is represented as a point in space, ignoring its orientation (`θ`). The configuration space is reduced to the `(x, y)` coordinates. The task of adjusting the robot's direction to follow the path is also left to the motion control.

These simplifications make the path planning calculation much more efficient.

## Code Structure

The provided code is modularized into classes for each search algorithm. The general structure is as follows:

-   **Main Class (e.g., `Dijkstra_Mobile_Robot`):**
    -   **`__init__`**: Initializes parameters, such as map resolution and robot radius. Most importantly, it creates the **obstacle map**. Instead of building an explicit graph in memory, the search builds the graph dynamically, checking at each step whether a neighboring node is an obstacle or not. The robot's radius is used to "inflate" the obstacles, ensuring that the generated path maintains a safe distance.
    -   **`Node` Class**: An internal structure to represent the graph's nodes, storing their position `(x, y)`, the `cost` to reach them, and the `parent_index` (to reconstruct the path at the end).
    -   **`planning`**: The main method where the logic of the search algorithm (Dijkstra, A*, etc.) is actually implemented.
    -   **Helper Functions**: Methods to check the validity of a node, calculate indices, positions, and the final path.

-   **Main Script:**
    -   Defines the scenario parameters: start and end positions, grid size, robot radius, and the location of obstacles.
    -   Instantiates the desired algorithm's class.
    -   Calls the `planning` method.
    -   Generates an animation of the search process and the final path found.

## Analysis of the Algorithms in Action

The same scenario (map, obstacles, start and end point) is used for all three algorithms, allowing for a direct comparison of their behavior.

-   **Start Point:** Green
-   **End Point:** Dark blue X
-   **Explored Nodes:** Light blue X
-   **Final Path:** Red line

### 1. Dijkstra

**Behavior:** Dijkstra's algorithm explores the search space radially and uniformly from the starting point. It visits all nodes in all directions, expanding a search "frontier" until the destination node is reached.

**Visual Result:**

<video width="640" height="480" controls autoplay loop>
  <source type="video/mp4" src="https://i.imgur.com/9k8o2g7.mp4">
</video>

As can be seen in the animation, a vast area of the map is filled with explored nodes (light blue X), showing that Dijkstra performs an exhaustive search. It guarantees the shortest path, but at a high computational cost, as it explores many areas irrelevant to the solution.

### 2. A* (A-Star)

**Behavior:** Guided by the Euclidean distance heuristic, A* focuses its search towards the goal. It prioritizes the exploration of nodes that are not only close to the start (`g(n)`) but also closer to the end (`h(n)`).

**Visual Result:**

<video width="640" height="480" controls autoplay loop>
  <source type="video/mp4" src="https://i.imgur.com/5bXJ3fC.mp4">
</video>

It is clear that A* explores a much smaller area than Dijkstra. The search is visibly directed towards the target. Even when a large obstacle forces it to deviate, the exploration remains more contained. This results in a much higher performance, finding the same optimal solution in less time.

### 3. D* Lite

**Behavior:** The implementation of D* Lite in the notebook does not show the exploration of the nodes in the same way, as its search process is different. It plans from the **end to the beginning** and is optimized to quickly replan when new obstacles are found. As the scenario is static (no new obstacles), we only see the final planning result.

**Visual Result:**

<video width="640" height="480" controls autoplay loop>
  <source type="video/mp4" src="https://i.imgur.com/sY4Y2fA.mp4">
</video>

The algorithm also finds an optimal path. The main advantage of D* Lite is not visible in this static example, but lies in its ability to efficiently update the path in dynamic environments without the need for a complete recalculation, making it ideal for real-world robotic applications.
