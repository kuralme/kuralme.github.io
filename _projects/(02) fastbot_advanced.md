---
name: "Fastbot Advanced: From Embedded Control to Visual SLAM"
tools: [ESP32, ESP-IDF, C, FreeRTOS, micro-ROS, ROS 2, Stella-VSLAM, OAK-D Lite, Docker]
image: https://kuralme.github.io/assets/fastbotadv_run.gif
description: Custom ESP32 motor-control firmware, fault protection, and ROS 2 stereo visual SLAM working together on a differential-drive robot.
---
# [Fastbot Advanced: From Embedded Control to Visual SLAM](https://github.com/kuralme/fastbot_advanced)

Fastbot Advanced is a mixed-criticality differential-drive robot project: an ESP32 handles the motor-control and safety path while a Raspberry Pi 4 runs the higher-compute ROS 2 perception stack. My work spans both levels, from the embedded C firmware for closed-loop wheel control, encoder odometry, and fault handling to integrating and deploying stereo visual SLAM, joystick control, and sensor logging.

The split keeps motor safety independent of the computational load and availability of visual SLAM. The firmware communicates with the companion computer through micro-ROS over UART, receiving velocity commands and returning odometry and status telemetry.

## 🚀 Project Goals

* **Mixed-Criticality Execution:** Separating safety-critical tasks (Tier 1) from computationally intensive SLAM (Tier 2).
* **Deterministic Motion Control:** Ensuring the PID loop and safety monitors are never interrupted by communication overhead.
* **System Reliability:** Self-healing communication loops and latching hardware fault states.
* **Advanced Navigation:** Implementing *Stella-SLAM* for visual localization and high-level trajectory control on a high-performance Linux environment.
* **SLAM & Fusion:** Stereo camera based SLAM fused with high-frequency wheel odometry and IMU.

---

## System Architecture

The project is organized as a monorepo containing both the low-level firmware and the high-level ROS2 SLAM stack.

![Fastbot hardware and software overview]({{ site.url }}{{ site.baseurl }}/assets/overview.png)

## ESP32 firmware: real-time control and safety

The ESP-IDF firmware separates the hard real-time control path from the ROS communication task, leveraging ESP32's dual core architecture. A 50 Hz timer callback updates encoder odometry, filters measured wheel speeds, runs an independent feed-forward PID controller for each wheel, checks for stalls, and writes PWM outputs. The micro-ROS task handles agent discovery, ROS entities, subscriptions, services, and telemetry asynchronously on the other core.

| Task | Priority | Core | Input | Output | Destination | Criticality role |
| --- | --- | --- | --- | --- | --- | --- |
| PID timer callback | High | 0 | Encoder ticks, wheel setpoints | PID outputs and PWM | Motor driver | Periodic wheel-speed regulation |
| Command watchdog | High | 0 | `cmd_vel` timestamp | Zero motor output and cleared setpoints | Motor driver | Stops safely when commands become stale |
| Stall monitor | High | 0 | PWM effort and measured wheel velocity | Latched fault status | Shared system state | Cuts power when commanded motion is not detected |
| micro-ROS task | Medium | 1 | Agent status, `/fastbot/cmd_vel` | Odometry and heartbeat | ROS 2 via UART agent | Asynchronous command and telemetry bridge |
| Fault-reset service | Medium | 1 | `/fastbot/reset_fault` request | Cleared fault state | Shared system state | Explicit recovery from a latched stall |

The controller uses C11 atomic system status to communicate fault state safely between tasks. Command timeout stops the motors and resets the wheel controller state; a detected stall latches a fault until the reset service is called. The micro-ROS task pings the agent, initializes its ROS entities when the agent is available, and cleans up and retries after a connection loss. This lets the firmware recover its ROS link without handing control-loop timing to the communications task.

The firmware subscribes to `/fastbot/cmd_vel`, publishes encoder odometry on `/fastbot/encoder_odom` and a system-state heartbeat on `/fastbot/heartbeat`, and provides `/fastbot/reset_fault`. It computes differential-drive odometry from quadrature encoder interrupts and reports planar pose and wheel-derived velocity to the ROS system.

### 🛡️ Reliability & Static Analysis

To ensure execution safety and deterministic behavior, the firmware is validated against industry-standard rule sets:

* **MISRA C:2012 / CERT C Compliance:** Using `cppcheck` and `clang-tidy` (via `cppcoreguidelines-*`), the codebase is audited for undefined behavior, pointer safety, and integer overflows.
* **Zero-Allocation Principle:** Post-initialization, the Tier 1 control loops (PID, Safety Watchdog) avoid dynamic memory allocation (`malloc/free`) to prevent heap fragmentation and non-deterministic timing.
* **Type Safety:** Strict enforcement of fixed-width integers (`uint32_t`, etc.) and `const`-correctness to ensure cross-platform predictability between the ESP32 and Raspberry Pi.

## ROS2 Stereo Visual SLAM and sensors

On the Raspberry Pi 4, a Dockerized ROS 2 environment runs Stella-VSLAM (ROS2) with stereo imagery from the OAK-D Lite. The visual SLAM system tracks visual features to estimate camera motion and maintain a sparse map. Wheel odometry from the ESP32 and data from the BNO085 IMU are available alongside the camera stream as complementary motion and inertial measurements.

The companion computer runs a micro-ROS agent that bridges the ESP32's UART transport to ROS 2. This carries velocity commands to the embedded controller and delivers firmware odometry and heartbeat data back to ROS. The communication and task split is shown below.

![ESP32 dual-core and micro-ROS communication architecture]({{ site.url }}{{ site.baseurl }}/assets/architecture.png)

The BNO085 driver publishes orientation, angular velocity, and linear acceleration on `/fastbot/imu`. Its I2C polling is gated by the sensor's data-ready interrupt, and it attempts sensor reinitialization if updates stall.

## Mapping workflow and data

The current tested workflow is joystick-driven mapping, not autonomous navigation. Manual driving lets the operator control the route while Stella-VSLAM estimates localization and builds a sparse 3D map.

- **Online mapping:** Process live rectified stereo images from the OAK-D Lite while driving. The resulting map can be saved as a MessagePack database.
- **Offline processing:** Record sensor and SLAM topics into MCAP bags for repeatable inspection and offline localization experiments on a workstation.
- **Recorded data:** The provided recording configuration includes stereo image streams, TF data, camera odometry, keyframes, and map points; wheel odometry and IMU data are part of the robot telemetry workflow.

## Full-stack demo

The demo shows the robot running the full stack while being joystick-driven:

[![Full-stack demo]({{ site.url }}{{ site.baseurl }}/assets/fastbotadv_run.gif)](https://youtu.be/jFU--0QsWlE)
