---
name: Robot Control Webapp
tools: [ROS2, Nav2, Gazebo, JS]
image: https://kuralme.github.io/assets/webapp.gif
description: A web application that connects to a ROS2 robot system, allowing users to control and monitor a simulated robot through an interactive interface
---

# [Robot Control Webapp](https://github.com/kuralme/fastbot_webapp)

Project aims to create a web application that communicates with a ROS2 system, allowing users to send commands and receive data from a robot and the connection to the webapp is enabled via *Rosbridge server*. The goal is to provide a user-friendly interface for controlling FastBot robot within Gazebo environment, enabling seamless interaction for both manual control and autonomous navigation. The webapp features various tools and visualizations to help users effectively manage and monitor the robot.

## Key Features

The following key features are implemented in the web application:

- **Interactive Map:** Displays the robot's current environment in real-time. The map is updated as the robot moves, providing users with a visual representation of its surroundings.

- **3D Robot Model**: A 3D visualization of the robot is included on the interface. This model updates in real-time to reflect the robot's orientation and movement, offering users a clear representation of the robot's position and attitude.

- **Camera View**: A live camera feed showing the view the robot sees from its front-facing camera. This helps users understand the robot's perspective and navigate more intuitively.

- **Virtual Joystick**: The app features a virtual joystick for manual control. This allows users to drive the robot using the arrow keys or a graphical joystick on the web interface, providing real-time control over movement and speed.

- **Current Speed**: The current speed of the robot is displayed in real-time. This gives the user immediate feedback on the robot’s movement velocity.

- **Position & Orientation**: The app provides the current position and orientation of the robot. This is essential for autonomous navigation or precise control.

- **Waypoint Buttons**: Users can set predefined waypoints on the map. With the waypoint buttons, users can command the robot to autonomously navigate to specific locations within the environment.

![Webapp demo]({{ site.url }}{{ site.baseurl }}/assets/webapp.gif)
