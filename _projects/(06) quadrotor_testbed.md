---
name: Quadrotor Control
tools: [C, Embedded, PID Controller, STM32, ROS, Python]
image: https://kuralme.github.io/assets/aero.jpg
description: PID angle controller implementation on STM32 for quadrotor test system
---

# [Quadrotor Control Testbed](https://github.com/kuralme/Quadrotor_testbed)

This BSc graduation project focuses on developing an embedded angle-control testbed for a 4-DOF quadrotor. The main goal was to design and validate a real-time control stack that stabilizes and controls the euler angles of a fixed-position quadrotor platform.

## Key Implementation Points

- **Real-Time Control:** Implemented in **C** on an **STM32F7 microcontroller**, ensuring high-speed control loop execution.  
- **Sensor Handling:** Integrated **BNO055 IMU** data for real-time orientation feedback, enabling precise control calculations.  
- **PID-Based Stabilization:** Low-level PID controllers regulate roll and pitch; gains were tuned experimentally through bench tests.  
- **Ground-Station Integration:** Python + ROS scripts provide joystick-based reference angles and log telemetry for monitoring and analysis.  
- **Rapid Prototyping:** Lightweight mechanical frame assembled from Makeblock components for quick testing and validation.

[![Quad test]({{ site.url }}{{ site.baseurl }}/assets/quad.gif)](https://youtu.be/svHYbfm_wV0)
