---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* **PhD, Robotics and 3D Computer Vision**, University of Waterloo, Waterloo, Canada (2022.01 – 2026.08)
  * Research focus: Multi-Modal Robotic Perception, 3D Computer Vision, Neural Rendering
  * CGPA: 88/100
* **B.Eng, Internet of Things (Double Degree)**, Beijing University of Posts and Telecommunications, Beijing, China (2017.09 – 2021.07)
  * CGPA: 85.8/100
* **B.Eng, Internet of Things (Double Degree)**, Queen Mary University of London, Beijing, China (2017.09 – 2021.07)
  * CGPA: 85.8/100

Work experience
======
* **Graduate Student, Localization, 3D Mapping and Reconstruction**, CViSS, University of Waterloo, Waterloo, Canada (2023.01 – 2026.08)
  * 3D Mapping, Localization & Reconstruction: Developed LiDAR–camera 3D reconstruction and neural rendering methods, including LiDAR-guided 3D Gaussian Splatting and dense SLAM priors for metric and high-fidelity scene reconstruction. Developed robust 6-DoF visual localization and pose-refinement methods using 3D Gaussian Splatting, feature matching, nonlinear optimization, pose graph optimization, and multi-view geometric constraints for robotics and autonomous systems.
  * Hardware Integration & Multi-Sensor Perception: Worked extensively with LiDAR, RGB cameras, IMUs, GNSS, and motion-capture systems for multi-sensor calibration, LiDAR–camera registration, and cross-modal sensor fusion. Hardware sensor synchronization and custom scanner platforms, including a handheld scanner and a vehicle-based scanner platform.
  * Research & Collaboration: Led and contributed to research projects spanning robotics, 3D computer vision, autonomous UAV inspection, mixed reality, and deep learning, resulting in publications at ICRA, IROS, RA-L, ISPRS, CRV, ICCCBE, and peer-reviewed journals.

* **SLAM/3D Algorithm Engineer, Localization and Mapping, Autonomous Driving Department**, Horizon Robotics, Beijing, China (2021.07 – 2021.12)
  * High-Definition Mapping: Contributed to large-scale autonomous driving localization and mapping projects; developed map-engine APIs for lane-level speed limit validation and supported in-vehicle ADAS testing.
  * Path Planning: Implemented a real-time route planning module by optimizing A\* and Dijkstra algorithms, integrated with ROS rviz for visualization and vehicle navigation experiments.

* **Software Development Intern**, Leizhi Technology Inc., Beijing, China (2021.02 – 2021.06)
  * 3D Point Cloud Processing: Developed PCL-based matching algorithms for randomly placed aerospace bolts using RANSAC and clustering methods (region growing, Euclidean cluster extraction).
  * RANSAC Enhancement: Improved RANSAC robustness in complex scenarios by incorporating bounding-box constraints for more reliable geometric detection.

* **Research Intern**, Tsinghua University IVip Laboratory, Beijing, China (2019.11 – 2020.10)
  * Literature Review: Investigated state-of-the-art SLAM frameworks (SE2LAM, ORB-SLAM2, VINS-Mono) to identify innovation opportunities in lifelong multi-sensor fusion.
  * SE(2) Odometry Optimization: Integrated SE(2) odometry with IMU and vision-based data through graph optimization using G2O and Ceres for improved local mapping accuracy.

Skills
======
* **Programming:** C/C++, Python, PyTorch, MATLAB, Shell, Bash
* **Tools:** Git, Linux, Conda, CUDA, ROS, LaTeX, SolidWorks, 3D Printing
* **Frameworks & Libraries:** PyTorch, OpenCV, PCL, Ceres, G2O, Sophus, Eigen, SQL, NoSQL, Cloud platforms
* **Robotics & Perception:** Visual/LiDAR SLAM, Multi-Sensor Calibration and Fusion (Camera, LiDAR, IMU, GNSS), 3D Reconstruction (3DGS, NeRF, SfM), Camera Re-localization, Bundle Adjustment, Sensor hardware-trigger synchronization
* **Deep Learning & Computer Vision:** Neural Rendering (Gaussian Splatting, NeRF), Vision-Language Navigation (VLN), Vision-Language-Action (VLA), 3D Deep Learning (PointNet++), 2D Vision ML tasks, Representation Learning

Publications
======
{% for category in site.publication_category %}
**{{ category[1].title }}**
  <ul>{% for post in site.publications reversed %}{% if post.category == category[0] %}
    {% include archive-single-cv.html %}
  {% endif %}{% endfor %}</ul>
{% endfor %}
