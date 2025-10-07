# Exteroceptive Sensors (Part 2): Light-Based Sensors

Continuing our exploration of exteroceptive sensors, we will now focus on those that use light to perceive the environment: LiDAR and cameras.

## 1. LiDAR (Light Detection and Ranging)

**LiDAR** is an active sensor that, analogous to sonar, measures the distance to obstacles. However, instead of sound, it uses laser pulses.

-   **How it works:** It emits a laser pulse and measures the time it takes for the light to return after being reflected by an object. Since the speed of light is constant and known, the distance is calculated with high precision.

-   **Advantages over Sonar:**
    -   **Field of View:** The laser beam is extremely focused, resulting in a practically infinitesimal field of view. This means that it measures the distance of an exact point, unlike the uncertainty cone of the sonar.
    -   **Point Cloud:** Modern LiDARs have multiple emitters/receivers and rotate at high speed (5-15 Hz), performing a 360° scan of the environment. The result is a dense and precise **point cloud**, which allows the 3D environment around the robot to be reconstructed with millions of points per second.
    -   **Range and Accuracy:** It has a much greater range (tens or hundreds of meters) with centimeter accuracy.

-   **Disadvantage:** The cost is significantly higher than that of sonars.

![Velodyne LiDAR Example](https://i.imgur.com/YJ4xG6g.png)

## 2. Cameras

**Cameras** are passive sensors (in most cases) that capture the light reflected by objects to form an image. They are one of the most information-rich sensors in robotics, allowing tasks such as object recognition, landmark identification, navigation, and distance measurement.

-   **Sensor Technology:** Light is captured by a matrix of pixels. The two most common image sensor technologies are:
    -   **CCD (Charged-Coupled Device):** Stores the electrical charge in an analog way and converts it to digital in a specialized circuit. It produces high-quality, low-noise images, but consumes more power and has a higher cost.
    -   **CMOS (Complementary Metal-Oxide Semiconductor):** Uses transistors in each pixel to convert light into a digital signal directly. Historically, it had lower quality, but advances in image processing integrated into the chip have made CMOS sensors competitive, offering lower cost and power consumption. Today, they dominate the market.

### Types of Cameras

-   **RGB Cameras:** The most common, they capture color images in the visible spectrum, representing each pixel with Red, Green, and Blue components.

-   **Infrared Cameras (NIR and FIR):** Capture light outside the human visible spectrum.
    -   **NIR (Near Infrared):** These are usually **active** cameras. They emit infrared light (invisible to us) and capture its reflection. They are the basis for most **night vision** systems.
    -   **FIR (Far Infrared) / Thermal Cameras:** These are **passive** cameras that detect the thermal radiation (heat) naturally emitted by bodies. They allow you to "see" living beings in the dark or identify heat sources.

-   **Depth Cameras (RGB-D or Stereo):** Provide, in addition to the color image (RGB), depth information (D) for each pixel, generating a depth map.
    -   **Stereo Vision:** Uses two cameras (receivers) separated by a known distance. By analyzing the disparity (difference) between the two images, just as our eyes do, it is possible to triangulate the position of each point in space and calculate the depth.
    -   **Time of Flight (ToF):** They work in a similar way to a LiDAR. The camera emits a flash of light (usually infrared) and measures the time it takes for the light to return to each pixel, calculating the distance from this time.
