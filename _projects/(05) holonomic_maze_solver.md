---
name: Holonomic Maze-Solver
tools: [C++, ROS2, PID Control, Gazebo, Holonomic Robot, LiDAR]
image: https://kuralme.github.io/assets/rosbotxl.gif
description: A maze solver robot project. The robot navigates using PID controller to follow waypoints, and sensor feedback for wall avoidance and course correction
---

# [Holonomic Maze-Solver Project](https://github.com/kuralme/holonomic_robot_project)

In this project, implemented **PID**-based controller for the ROSBot XL, a holonomic (omni-directional) mobile robot by Husarion, enabling navigation in both simulation and real-world maze environments. The system runs in *Gazebo simulation* as well as on the real robot within the *Cyberworld Lab*, a remote robotics testing environment provided by *The Construct*.

The robot navigates through mazes under defined constraints, combining **waypoint-based path planning**, **holonomic motion control**, and **real-time sensor feedback** from its **LIDAR** and onboard odometry. The approach uses **C++ and ROS2** to continuously calculate control commands, ensuring accurate positioning, smooth trajectory tracking, and efficient movement through each waypoint toward the final goal.

[![Maze-reverse]({{ site.url }}{{ site.baseurl }}/assets/maze_solver.gif)](https://youtu.be/6SGL1RXAGmI)

## Key Features

- **Holonomic Motion Control:** Uses PID controllers to achieve precise movement in all directions, leveraging the robot’s omni-directional wheels for agile maneuvers.

- **C++ and ROS2 Integration:** The control algorithm is implemented in **C++** with ROS2 nodes, enabling modular, real-time operation.

- **Waypoint-Based Navigation:** Navigates through pre-defined waypoints in the maze both normal and reverse directions, doing simple motions in each step. The video demonstrates reversed version.

- **Real-Time Sensor Feedback:** Integrates LIDAR data to detect walls, maintain accurate positioning, and adjust control commands dynamically.

The project has several implementation steps:

- An empty world for testing basic functionality - robot makes a figure 8
- A similar Gazebo simulation environment for testing maze solving
- A real-world setup, ran remotely connected to the *The Construct*'s *Cyberworld Lab*

![Maze-sim]({{ site.url }}{{ site.baseurl }}/assets/maze_solver_sim.gif)

![Figure8]({{ site.url }}{{ site.baseurl }}/assets/figure8.gif)
