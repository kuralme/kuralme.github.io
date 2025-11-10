---
name: Coffee Cup Dispenser
tools: [C++, Python, ROS2,  Moveit2, PCL, Opencv, BT, Gazebo, Docker]
image: https://kuralme.github.io/assets/final.gif
description: A 6-DOF robot arm programmed to manipulate cup from counter to delivery robot tray cup hole using Moveit2 planning
---
# [Starbots Coffee Dispenser Project](https://github.com/kuralme/starbots_coffee_dispenser)

The final outcome of my work in The Construct’s Robotics Masterclass, featuring an advanced robotics application that demonstrates refined Pick-and-Place capabilities with the **UR3e robotic arm**. The Starbots Coffee Dispenser system is designed to automate a crucial step in robotic coffee service - transferring coffee cups from a counter to the delivery robot's tray.

[![Final demo]({{ site.url }}{{ site.baseurl }}/assets/final.gif)](https://youtube.com/shorts/2kQtupTTEGs?feature=share)

The project is structured into multiple ROS2 packages, each handling specific aspects of the automation:

- **Motion Planning & Control**: Utilizes **MoveIt2** framework for:
  - Well defined robot kinematics
  - Sophisticated path planning with selected OMPL planners
  - Real-time, collision aware trajectory generation
  - IK Kinematic solving
  - Precise end-effector control for cup manipulation

- **Perception Pipeline**: Implements an object detection system using both RGB camera feeds and depth information. The system processes point cloud data to:
  - Detect and locate coffee cups on the counter
  - Identify available slots on the delivery robot's tray
  - Generate an OctoMap representation of the environment for collision-aware planning
  
- **Task Management**: Employs a behavior tree architecture to oversee the complete task sequence:
  - Pre-pick positioning
  - Approach/Retreat, Cup grasping operations
  - Transfer movements involves carrying the cup upright
  - Precise placement to goal cup holder on the delivery robot's tray
  - Return to home position

The project maintains two implementations:

- A simulation branch that replicates same functionality in a Gazebo environment, allowing for safe testing and validation
- A real-world deployment, ran remotely connected to the *The Construct*'s Starbots Coffee UR3E robot

Both implementations share core functionalities but are specifically tuned for their respective environments, ensuring optimal performance whether in simulation or real-world operation.

[![Final Gazebo demo]({{ site.url }}{{ site.baseurl }}/assets/final_sim.gif)](https://youtu.be/4XE2JNb8slM)
