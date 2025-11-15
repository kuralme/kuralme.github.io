---
name: Coffee Cup Dispenser
tools: [C++, Python, ROS2,  Moveit2, PCL, Opencv, BT, Gazebo, Docker]
image: https://kuralme.github.io/assets/final.gif
description: A 6-DOF robot arm programmed to manipulate cup from counter to delivery robot tray cup hole using Moveit2 planning
---
# [Starbots Coffee Dispenser Project](https://github.com/kuralme/starbots_coffee_dispenser)

The final outcome of my work in The Construct’s Robotics Masterclass, featuring an advanced robotics application that demonstrates refined Pick-and-Place capabilities with the **UR3e robotic arm**. The Starbots Coffee Dispenser system is designed to automate a crucial step in robotic coffee service - transferring coffee cups from a counter to the delivery robot's tray.

The project has two implementations:

- A simulation branch that replicates same functionality in a Gazebo environment, allowing for safe testing and validation
- A real-world deployment, ran remotely connected to the *The Construct*'s Starbots Coffee UR3E robot

Both implementations share core functionalities but are specifically tuned for their respective environments, ensuring optimal performance whether in simulation or real-world operation.

The project is structured into multiple ROS2 packages, each handling specific aspects of the automation:

### Motion Planning & Control

Utilized **MoveIt2** C++ API for:

- Well defined robot kinematics and accurate modeling of the UR3e arm
- Advanced path planning with selected OMPL planners (primarily KPIECE)
- Real-time, collision-aware trajectory generation using OctoMap and dynamic scene updates from the perception pipeline
- IK kinematic solving with customized constraints to maintain the cup upright and avoid unwanted wrist rotations during transport
- Precise end-effector control for grasping and placement, including approach and retreat motions

### Perception Pipeline

Implemented a python object detection system using D415 RGB-D camera's color and depth images. After the conversion from images to pointcloud, the perception system includes two separate detection pipelines for identifying the cup holders on the delivery robot's tray:

- **Hough Circle Detection (Image-Based)**:
Uses classical image processing on the RGB image to detect circular shapes corresponding to the tray's cup holders. This outputs 2D circle centers and radii in image space.

- **Pointcloud-Based Detection**:
Processes the pointcloud with PCL to locate the cup holder regions directly in 3D. Includes filtering, RANSAC, K-means clustering, segmentation, and geometric checks to identify the circular depressions on the tray.

After running both pipelines, a sensor fusion step combines their outputs. The image-based detections are projected into 3D, matched with the pointcloud detections, and then merged using a weighted average to generate a more stable and accurate 3D pose for each cup holder.

Additional perception features include:

- Detection and localization of coffee cups on the counter (Simulation only)

- Identification and tracking of available slots on the delivery robot's tray

- Generation of an OctoMap representation of the environment for collision-aware planning using pointcloud
  
### Task Management

Employed a behavior tree architecture to oversee the complete task sequence. The BT structure organizes the logic into modular, reusable nodes that manage both high-level decision making and low-level robot actions:

- Pre-pick positioning with orientation constraints to align the end-effector for a reliable approach
- Approach/Retreat sequences that dynamically adjust based on the detected cup or slot position
- Cup grasping operations including gripper open/close control and height adjustments
- Transfer movements that ensure the cup is carried upright, using waypoint-based motion to avoid collisions and maintain stability during transport
- Precise placement into the goal cup holder on the delivery robot's tray, relying on the fused perception output and aligned approach vectors
- Return to home position and ready state for the next service call, resetting the planning scene and BT context

### Visualization & Monitoring Tools

Used Foxglove throughout the project to monitor system behavior, visualize data streams, and interact(service calls only) with the robot during both simulation and real-world execution.

- **Foxglove Desktop (Simulation):**
Utilized for high-bandwidth monitoring of ROS2 topics, visualizing pointclouds, camera images, TF frames, and MoveIt planning scenes in real time. Also used for sending service calls during debugging and validating perception outputs before running full task sequences.

- **Foxglove WebApp (Real Robot):**
Connected remotely to The Construct’s UR3e setup to observe live sensor data, track behavior tree status, verify planning results, and monitor the D415 camera feed. Enabled safe remote operations and system checks without direct access to the robot hardware.

Foxglove provided a unified interface for inspecting the entire system — perception, motion planning, and task execution — assisting greatly in tuning parameters, debugging failures, and validating final robot behavior.

## System Overview

![System]({{ site.url }}{{ site.baseurl }}/assets/system_overview.png)

## Real Robot Demo

[![Final demo]({{ site.url }}{{ site.baseurl }}/assets/final.gif)](https://youtube.com/shorts/2kQtupTTEGs?feature=share)

## Simulation Demo

[![Final Gazebo demo]({{ site.url }}{{ site.baseurl }}/assets/final_sim.gif)](https://youtu.be/4XE2JNb8slM)
