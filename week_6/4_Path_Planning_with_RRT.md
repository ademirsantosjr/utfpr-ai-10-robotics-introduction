
# Path Planning with RRT (Rapidly-Exploring Random Trees)

When a robot's configuration space becomes very large or multidimensional (for example, in a robotic arm with many degrees of freedom), deterministic search algorithms like Dijkstra and A* become impractical. They would take too long to find a solution.

For these complex scenarios, sampling-based and randomized approaches, such as **RRT (Rapidly-Exploring Random Trees)**, are much more efficient.

## The Concept of RRT

RRT is an algorithm that incrementally and randomly builds a search tree to quickly explore a configuration space. The idea is to expand the tree towards random points, efficiently filling the free space.

**How it works:**

1.  **Initialization:** The tree starts with a single node, the robot's initial position (`q_start`).
2.  **Iteration:** The algorithm repeats the following steps for a defined number of iterations or until a solution is found:
    a.  **Generate Random Point (`q_rand`):** A random point is generated within the configuration space.
    b.  **Find Nearest Node (`q_near`):** The algorithm finds the node in the tree that is closest to the generated random point.
    c.  **Expand the Tree:** From `q_near`, the tree is expanded in the direction of `q_rand` by a fixed distance (a step `ε`). This creates a new node, `q_new`.
    d.  **Check for Collision:** If the path between `q_near` and `q_new` is free of obstacles, `q_new` is added to the tree as a child of `q_near`.

3.  **Conclusion:** The process continues until a `q_new` is generated close enough to the destination node (`q_goal`). When this happens, the destination is connected to the tree and the path is found by tracing the route from the destination back to the origin through the parent nodes.

![RRT Tree Expansion](https://i.imgur.com/YJ0Qv8c.png)

### RRT Characteristics

-   **Advantage:** It is extremely efficient for exploring large, high-dimensional search spaces, finding a solution (a viable path) very quickly.
-   **Completeness:** The algorithm is considered "probabilistically complete," which means that if a path exists, RRT will find it, given enough iterations.
-   **Non-optimality:** The first path found by RRT is rarely the shortest or smoothest path. The random nature of the search usually results in "jagged" and inefficient paths.

See the difference in space exploration with few and many iterations:

![RRT Exploration with 45 and 2345 iterations](https://i.imgur.com/3Y2gY8g.png)

## Improvements and Optimizations

To accelerate convergence and improve path quality, several extensions of RRT have been proposed:

1.  **Bidirectional RRT:** Two trees are built simultaneously, one from the start and one from the end. They grow towards each other. When the two trees meet, a path is established. This can drastically speed up the search, as exploring two halves of the space is much faster than exploring the entire space from a single point.

2.  **Goal-Biasing Heuristic:** Instead of always choosing a completely random point, the algorithm, with a certain probability (e.g., 5% of the time), chooses the destination node itself as `q_rand`. This "pulls" the tree's growth towards the goal, working similarly to the A* heuristic, but without getting stuck in local minima, as most of the exploration is still random.

3.  **RRT* (RRT-Star):** A popular variation that adds an optimization step. After adding a new node, RRT* checks if there is a better (shorter) path to it from other nodes in the vicinity and also checks if the presence of this new node can create a shorter path for its neighbors. With enough iterations, RRT* converges to the optimal path, combining the exploration speed of RRT with the optimality of algorithms like A*.

## RRT in Action

In the same scenario as the previous algorithms, we see the chaotic, yet effective, behavior of RRT.

**Visual Result:**

<video width="640" height="480" controls autoplay loop>
  <source type="video/mp4" src="https://i.imgur.com/sY4Y2fA.mp4">
</video>

The video shows the tree expanding randomly until it finds the destination. The final path (red line) is functional, but visibly not the shortest. Each time the algorithm is run, a different path is generated due to its stochastic nature.

Although not ideal for simple 2D problems (where A* is superior), RRT and its variants are powerful and essential tools for path planning in complex real-world robotic problems.
