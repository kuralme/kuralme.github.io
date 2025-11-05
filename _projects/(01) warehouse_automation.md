---
name: Warehouse Automation Robot
tools: [ROS2, Nav2, Python, LIDAR]
image: https://kuralme.github.io/assets/warehouse_robot.gif
description: Warehouse logistics with AMR
---

# Warehouse Automation Project

This project, developed as part of The Construct's ROS2 Navigation Course, demonstrates advanced autonomous navigation capabilities using the **RB1 mobile robot**. The system showcases a complete warehouse automation solution that leverages the **ROS 2 Nav2 stack** for robust autonomous navigation and task execution in both simulated and real environments.

<iframe width="800" height="450" src="https://youtu.be/EtJWyMgCmgQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<br>
<img src="{{ site.url }}{{ site.baseurl }}/assets/warehouse_positions.png">

The project implements a comprehensive warehouse automation system with several key components:

- **Navigation System**: Utilizes the **Nav2 framework** for:
  - Autonomous localization using AMCL
  - Dynamic path planning with obstacle avoidance
  - Precise trajectory following
  - Real-time replanning capabilities

- **Task Management**: Implements the **Nav2 Simple Commander API** to:
  - Coordinate complex sequences of actions
  - Handle operations
  - Monitor task execution

- **Warehouse Operations**: Automates core logistics tasks including:
  - Initial pose estimation and localization
  - Navigation to loading/unloading zones
  - Shelf manipulation with robot's lift mechanism
  - Safe transport through designated pathways
  - Autonomous return to home position

The project maintains two implementations:

- A thoroughly tested Gazebo simulation environment
- A real-world deployment setup in The Construct's warehouse

Both setups utilize identical control logic while accounting for their specific environmental characteristics and constraints.

## Key Features

- **Automatic Localization**  
  Robust pose estimation using AMCL localization

- **Precision Navigation**  
  Advanced path planning with dynamic obstacle avoidance

- **Shelf Operations**  
  Automated shelf pickup and placement with precise positioning

- **Safety-First Design**  
  Comprehensive obstacle detection and avoidance systems

- **Flexible Architecture**  
  Modular design allowing easy adaptation to different warehouse layouts
