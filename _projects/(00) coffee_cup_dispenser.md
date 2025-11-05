---
name: Coffee Cup Dispenser
tools: [C++, Python, ROS2,  Moveit2, PCL, Opencv, Behavior-tree, Gazebo, Docker]
image: https://kuralme.github.io/assets/final_sim.gif
description: A 6-DOF robot arm programmed to manipulate cup from counter to delivery robot
---
# Starbots Coffee Dispenser Project

## Overview

This project is the final outcome of my work in The Construct’s Robotics Masterclass, featuring an advanced robotics application that demonstrates refined Pick-and-Place capabilities with the **UR3e robotic arm**. The Starbots Coffee Dispenser system is designed to automate a crucial step in robotic coffee service - transferring coffee cups from a counter to a delivery robot's tray.

[![Final demo]({{ site.url }}{{ site.baseurl }}/assets/final_sim.gif)](https://youtu.be/4XE2JNb8slM)

The project is structured into multiple ROS2 packages, each handling specific aspects of the automation:

- **Motion Planning & Control**: Utilizes **MoveIt2** framework for:
  - Sophisticated path planning with selected OMPL planners, considering environmental constraints
  - Real-time trajectory generation
  - Precise end-effector control for cup manipulation

- **Perception Pipeline**: Implements an object detection system using both RGB camera feeds and depth information. The system processes point cloud data to:
  - Detect and locate coffee cups on the counter
  - Identify available slots on the delivery robot's tray
  - Generate an OctoMap representation of the environment for collision-aware planning
  
- **Task Orchestration**: Employs a behavior tree architecture to manage the complete task sequence:
  - Pre-pick positioning
  - Cup grasping operations
  - Transfer movements involves carrying the cup upright
  - Precise placement on the delivery robot's tray
  - Return to home position

The project implemented in two separate branches:

- The main branch is optimized for real-world deployment with the physical UR3e robot
- A simulation branch that replicates the functionality in a Gazebo environment, allowing for safe testing and validation

Both implementations share core functionalities but are specifically tuned for their respective environments, ensuring optimal performance whether in simulation or real-world operation.

[![Final Gazebo demo]({{ site.url }}{{ site.baseurl }}/assets/final_sim.gif)](https://youtu.be/4XE2JNb8slM)
