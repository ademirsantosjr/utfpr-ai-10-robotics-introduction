
# Path Planning with Deterministic Solutions

After understanding what navigation is, let's explore how robots plan their paths. The first approaches were purely **reactive**, where the robot simply reacted to sensor data (e.g., "move forward until an obstacle is found, then turn right"). This strategy works for simple, local tasks but is not efficient for complex, global navigation.

For truly autonomous navigation, we need **deliberative** solutions that use a map of the environment to plan the best path. Deterministic techniques, based on Artificial Intelligence and optimization, are fundamental for this.

## Graph Construction from Maps

The most common approach is to represent the environment as a **graph**. Using an **occupancy grid** map (where the environment is divided into free or occupied cells), we can build a graph as follows:

- **Nodes:** Each **free** cell on the map becomes a node in the graph.
- **Edges:** Nodes corresponding to neighboring cells are connected by edges. The weight of each edge usually represents the distance between the cells.

![Representation of an occupancy grid map as a graph](https://i.imgur.com/3Y2gY8g.png)

**Representation Challenges:**

- **Occlusion:** A cell can be marked as "occupied" even if only a small part of it contains an obstacle. This can block viable paths.
- **Resolution:** Using smaller cells increases the map's accuracy but also increases memory consumption and the processing time of search algorithms, as the graph becomes much larger.

With technological advances, it is possible to use high-resolution grids, mitigating the occlusion problem in most scenarios.

## Graph Search Algorithms for the Shortest Path

Once the graph is built, the problem becomes finding the **shortest path** between a starting node and an ending node. For this, we use classic search algorithms.

### 1. Dijkstra's Algorithm

Invented by Edsger W. Dijkstra in 1956, this algorithm is a classic and **optimal** solution for finding the shortest path from a source node to **all** other nodes in a graph.

**How it works:**

1.  **Initialization:** All nodes are marked as "unvisited". The distance from the starting node to itself is 0, and to all others is infinite.
2.  **Selection:** Choose the unvisited node with the smallest known distance to the origin.
3.  **Update:** For each neighbor of the current node, calculate the distance by passing through it. If this new distance is less than the one already recorded, the update is made.
4.  **Repetition:** The current node is marked as "visited" and the process is repeated from step 2, until all nodes are visited (or until the destination node is reached).

**Advantage:** Guarantees the optimal solution (the shortest path).
**Disadvantage:** Explores a large part of the graph, which can be slow on very large maps.

### 2. A* (A-Star) Algorithm

Proposed in 1968 specifically for a robotic navigation problem (the Shakey robot), A* is an evolution of Dijkstra that finds the shortest path from a source node to a **single** destination node much more efficiently.

**How it works:**

The great innovation of A* is the use of a **heuristic** to guide the search. The cost function of each node `f(n)` is calculated as:

`f(n) = g(n) + h(n)`

- `g(n)`: The actual cost of the path from the starting node to node `n` (the same as what Dijkstra calculates).
- `h(n)`: The **estimated** cost from node `n` to the destination node. In navigation, the most common heuristic is the **Euclidean distance** (the straight-line distance), ignoring obstacles.

The search prioritizes nodes with the lowest `f(n)` value, which intelligently directs it towards the goal, pruning large parts of the search space.

**Advantage:** Much faster than Dijkstra, as it explores fewer nodes. With a good heuristic, it also guarantees the optimal solution.
**Disadvantage:** In dynamic environments, if a new obstacle appears, the entire path needs to be recalculated from scratch.

### 3. Incremental Algorithms: D* and D* Lite

To deal with dynamic environments where new obstacles can be discovered, incremental algorithms were created.

#### D* (Dynamic A*)

Invented by Anthony Stentz in 1994, D* is an incremental version of A*. Its main feature is that it plans the path **from the destination to the origin**.

When a new obstacle is detected in the robot's path, D* does not need to recalculate everything. It only updates the costs of the graph nodes that were affected by the new obstacle and "fixes" the path from that point. This makes it much more efficient in changing environments.

#### D* Lite

Proposed in 2002, D* Lite is an even more efficient version, based on another algorithm (LPA*). It achieves the same result as D*, but with a faster and more optimized implementation. It is considered the state of the art for path planning on occupancy grids and is used in real-world applications, such as on NASA's Mars exploration rovers.

These algorithms form the basis of deterministic path planning, allowing robots to navigate intelligently and efficiently in complex environments.
