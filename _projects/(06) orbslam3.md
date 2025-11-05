---
name: ORB-SLAM3 Tests
tools: [Visual SLAM, ROS, Kitti, Pangolin]
image: https://kuralme.github.io/assets/orbslam3.gif
description: ORB-SLAM3 tested on Kitti dataset
---

# ORB-SLAM3 Testing

This is a testing implementation that runs ORB‑SLAM3 with ROS, on the KITTI dataset. Modifications are limited to ROS/package integration, dataset I/O, and logging; the core SLAM pipeline follows the original ORB‑SLAM3 design.

Algorithm features:

- **ORB feature extraction:** fast, rotation- and scale-invariant keypoints are detected and described.
- **Visual tracking:** features are matched frame-to-frame to estimate the camera pose relative to the map.
- **Map management:** selected frames become keyframes; 3D map points are created and refined by local bundle adjustment.
- **Loop closing & relocalization:** loop closures are detected, a pose‑graph optimization is run to remove drift, and full bundle adjustment refines the map.
- **Multi-sensor support:** ORB‑SLAM3 supports monocular/stereo/RGB‑D and optional IMU fusion to recover scale and improve robustness.

Demo video:

<iframe width="800" height="450" src="https://www.youtube.com/watch?v=uyDB0oSnJ2U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<br>
