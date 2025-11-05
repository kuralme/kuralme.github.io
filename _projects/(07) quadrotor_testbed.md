---
name: Quadrotor Control
tools: [PID Controller, C, Embedded, STM32, ROS, Python]
image: https://kuralme.github.io/assets/aero.jpg
description: PID angle controller implementation on STM32 for quadrotor test system
---

# Quadrotor Control Testbed

My BSc graduation project: an embedded angle-control testbed for a 4-DOF quadrotor. The objective was to design and validate a real-time control stack that stabilizes and controls body angles (roll and pitch) of a fixed-position quadrotor platform.

Key implementation points:

- Real-time flight control implemented in C on an STM32F7 microcontroller.
- Sensor handling and attitude estimation from an IMU, control loop execution, and PWM output to ESCs for motor speed.
- Low-level PID controllers for attitude stabilization; gains tuned experimentally through bench tests.
- Ground-station integration using a Python + ROS script to provide joystick-based reference angles and to log telemetry during tests.
- Lightweight mechanical frame assembled from Makeblock components for rapid prototyping and validation.

[![Quad test]({{ site.url }}{{ site.baseurl }}/assets/quad.gif)](https://youtu.be/svHYbfm_wV0)
