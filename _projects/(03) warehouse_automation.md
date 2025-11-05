---
name: Warehouse Automation Robot
tools: [ROS2, Nav2, Python, LIDAR]
image: https://kuralme.github.io/assets/warehouse_robot.gif
description: RB1, an AMR demonstrating robotics can streamline warehouse operations — autonomously localizing, navigating, and transporting shelves in both simulation and real environments
---

# Warehouse Automation Project

This project, developed as part of *Robotics Masterclass* ROS2 Navigation Course, demonstrates advanced autonomous navigation capabilities using the **RB1 mobile robot** by Robotnik. The system showcases a complete warehouse automation solution that leverages the **ROS 2 Nav2 stack** for robust autonomous navigation and task execution in both simulated and real environments.

## Key Features

- **Autonomous Localization & Navigation**: Powered by the ROS 2 Nav2 framework, the AMR achieves robust self-localization using AMCL and performs real-time path planning with dynamic obstacle avoidance. It follows precise trajectories and continuously replans routes in response to environmental changes, ensuring smooth and efficient movement throughout the warehouse.

- **Intelligent Task Management**: Integrates the *Nav2 Simple Commander API* to coordinate multi-step task sequences, such as navigating between zones, picking up or dropping shelves, and returning to the base station. The task manager also monitors execution progress and handles recovery behaviors autonomously.

- **Automated Warehouse Operations**: Executes warehouse workflows — including navigation to loading/unloading areas, shelf manipulation with the lift mechanism, and safe transport along designated paths. The robot performs all operations autonomously, reducing manual intervention and improving process consistency.

![Final demo]({{ site.url }}{{ site.baseurl }}/assets/rb1lift.gif)

- **Flexible Deployment**: Designed with a flexible ROS 2 modular structure, allowing for easy integration of new sensors, custom warehouse maps, and scalable expansion to multi-robot systems or larger facilities.

The project maintains two implementations:

- A thoroughly tested Gazebo simulation environment
- A real-world deployment setup in *The Construct*'s warehouse

Both setups utilize identical control logic while accounting for their specific environmental characteristics and constraints.
[![Final demo]({{ site.url }}{{ site.baseurl }}/assets/warehouse_robot.gif)](https://youtu.be/EtJWyMgCmgQ)
<img src="{{ site.url }}{{ site.baseurl }}/assets/warehouse_positions.png" width="70%">
