# Exploration and Semantic Mapping in Robotics

The construction of maps by robots is not a manual process. For a robot to operate autonomously in a new environment, it must be able to build its own map. This process is known as **robotic mapping**, and the task of navigating the environment to gather the necessary information is called **exploration**.

## Exploration: Discovering the Environment

Exploration is the process by which the robot moves efficiently to build a complete map of the environment. For this, some premises are generally assumed:

- The robot has knowledge of its own location.
- There is an estimate of the maximum area to be mapped for the allocation of computational resources.

### Frontier-Based Exploration Strategy

The most common approach to exploration is **frontier-based exploration**. The frontier is the boundary between known, free space and unexplored space.

The process works as follows:

1.  **Initial Mapping:** The robot begins to map the area immediately around it, identifying free and occupied spaces.
2.  **Frontier Identification:** The areas at the edge of the known map are marked as frontiers.
3.  **Decision Making:** The robot chooses a frontier to explore. The choice can be based on criteria such as the nearest or the largest frontier (with the greatest potential for information gain).
4.  **Navigation and Update:** The robot moves to the chosen frontier, collects new information with its sensors, and updates the map.
5.  **Repetition:** The process is repeated until there are no more frontiers to explore, which indicates that the map is complete.

## Semantic Mapping: Adding Meaning to the Map

During exploration, the robot can go beyond the simple distinction between free and occupied by adding **semantic information** to the map. This means identifying and labeling objects and regions according to their category (e.g., "door," "table," "person"). This capability is crucial for the robot to interact intelligently with the environment.

**Semantic segmentation**, a computer vision task, is the technique used to classify the different regions of an image.

### Semantic Segmentation Techniques

#### Bag of Visual Words (BoVW)

A classic approach to object recognition. The process consists of:

1.  **Vocabulary Creation:**
    -   Extraction of features (descriptors like SIFT, ORB, SURF) from a large set of training images.
    -   Clustering (e.g., k-means) of these descriptors to form a "vocabulary" of "visual words" (representations of object features).
2.  **Object Recognition:**
    -   When the robot captures a new image, its features are extracted.
    -   These features are compared with the vocabulary to find the closest "visual word."
    -   A histogram of the image's visual words is created and compared with the histograms of known object categories to classify the object.

#### Deep Learning

Currently, deep learning techniques, especially **Convolutional Neural Networks (CNNs)**, dominate the field of semantic segmentation due to their high accuracy.

Some notable architectures include:

-   **SegNet:** A symmetric *encoder-decoder* architecture, relatively lightweight and suitable for robotic systems with limited hardware resources.
-   **PSPNet and DeepLab3:** More complex architectures that also use the *encoder-decoder* structure but incorporate context information, resulting in higher accuracy but with a higher computational cost (often requiring GPUs).
-   **SegFormer:** A more recent architecture based on *Transformers*, which stands out for being lightweight and efficient, with great potential for applications in robotics.
