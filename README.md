## Pratyush Vatsa

**Software for machines and processes that have to work outside a demo.**

We build across four lines: robotics and control, simulation and testing, automation and
AI, and product. They are the same job at different layers, and the seams between them
are where projects usually break.

![ROS 2](https://img.shields.io/badge/ROS%202-Humble%20%7C%20Jazzy-22314E?style=flat-square)
![PX4](https://img.shields.io/badge/PX4-flight%20stack-1B95E0?style=flat-square)
![ArduPilot](https://img.shields.io/badge/ArduPilot-flight%20stack-0A6E4A?style=flat-square)
![Jetson](https://img.shields.io/badge/NVIDIA-Jetson-76B900?style=flat-square)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)

Most of our work starts the same way: a machine or a process is doing something wrong
and nobody can say why. So the work starts with diagnosis, not code.

We write software only — including the software that runs on hardware: firmware for your
flight controller, drivers, embedded C++, board bring-up in software terms, ROS 2 nodes,
MAVLink integration, perception. We do not build, wire, assemble or repair hardware, we
do not do PCB or mechanical design, and nothing has to be shipped to us.

---

## Robotics & control

ROS 2, PX4 and ArduPilot drone autonomy, MAVLink integration, LiDAR SLAM, control
systems and state estimation, real-time perception on Jetson and Raspberry Pi. Our code
runs on real vehicles, not just in simulation, so it has already met the failure modes
you are hitting.

| Project | What it does | Stack |
|---|---|---|
| [**px4-mavlink-companion**](https://github.com/Pratyush150/px4-mavlink-companion) | MAVLink bridge between a flight controller and a companion computer. Serial discovery by stable `by-id` name, baud probing confirmed by a real heartbeat, and a watchdog that tells a dead link, a dead stream, frozen contents, a backwards clock and an autopilot reboot apart. | Python, pymavlink, PX4, ArduPilot |
| [**drone-control-toolkit**](https://github.com/Pratyush150/drone-control-toolkit) | PID with anti-windup and filtered derivative, cascaded loops, discrete LQR without scipy, complementary / Madgwick / Kalman / EKF attitude estimation, motor mixing that gives up thrust to keep attitude, and a sim harness that injects latency, motor lag, quantisation and gyro bias. | Python, NumPy |
| [**jetson-realtime-detection**](https://github.com/Pratyush150/jetson-realtime-detection) | Edge detection and tracking: one-deep latest-frame buffer, adaptive frame skipping solved from measured timings, SORT tracking with Hungarian assignment written from scratch, and per-stage p50/p90/p99 profiling. | TensorRT, ONNX Runtime, Hailo, OpenCV, Python |
| [**flight-log-analyzer**](https://github.com/Pratyush150/flight-log-analyzer) | Reads PX4 ULog, ArduPilot dataflash and CSV exports and produces a ranked findings report — vibration spectra, pack internal resistance, control oscillation mapped to the gain that is too high, EKF innovations — ranked cause before symptom. | Python, NumPy, pyulog, pymavlink |
| [**lidar-slam-toolkit**](https://github.com/Pratyush150/lidar-slam-toolkit) | Diagnostics and annotated configs for LIO-SAM, Cartographer and RTAB-Map: extrinsics validation, time-sync recovery, z-drift split into ramp and step, and degeneracy analysis that says which axis the solver is free to slide along. | Python, NumPy, ROS 2, LIO-SAM, Cartographer |
| [**ros2-diffdrive-robot**](https://github.com/Pratyush150/ros2-diffdrive-robot) | A ROS 2 differential-drive robot end to end: Xacro description, Gazebo bringup, and a mutex-guarded serial driver with open-loop PWM and closed-loop rad/s modes reading encoders back. *Reference implementation; vendors `serial_motor_demo` from Josh Newans' Articulated Robotics project, BSD 3-Clause.* | ROS 2, Gazebo, Xacro, pyserial |
| [**robot-description-urdf-xacro**](https://github.com/Pratyush150/robot-description-urdf-xacro) | The same mobile robot written twice, plain URDF and Xacro, so the difference is visible rather than described — including the missing-inertial failure that makes a link fall through the world. *Reference repo.* | URDF, Xacro, ROS 2 |
| [**cpp-for-robotics**](https://github.com/Pratyush150/cpp-for-robotics) | C++ fundamentals through robotics examples: parsing a command off a serial line, handling a sensor that returns garbage, passing state without copying, fixed-precision telemetry output. One concept per file. *Reference repo.* | C++, Eigen |

---

## Simulation & testing

Gazebo, Isaac Sim and AirSim environments for testing robots before they exist in metal,
plus automated regression testing of robot behaviour.

| Project | What it does | Stack |
|---|---|---|
| [**ros2-drone-bringup**](https://github.com/Pratyush150/ros2-drone-bringup) | ROS 2 Humble bringup for a PX4 or ArduPilot multirotor with PX4 SITL and Gazebo launch files: geodesy, mission format with real scanline survey generation, a geofence that reports time to breach, and a guarded mission state machine. All flight logic lives in a core package that imports no ROS, enforced by a test. | ROS 2, MAVROS, PX4 SITL, Gazebo, Python |
| [**robot-sim-test-harness**](https://github.com/Pratyush150/robot-sim-test-harness) | Scenario-driven regression testing for robot behaviour: declarative YAML scenarios, byte-reproducible seeded traces, temporal assertions (`always`, `eventually`, `A until B`), failure-boundary bisection, trace diffing to the first divergent timestep, and JUnit output for CI. Gazebo, AirSim and Isaac Sim behind one interface. | Python, PyYAML, Gazebo, AirSim, Isaac Sim |

---

## Automation & AI

Industrial automation, workflow automation, AI chatbots and FAQ assistants, LLM
integrations, internal tools that remove manual work.

| Project | What it does | Stack |
|---|---|---|
| [**llm-faq-assistant**](https://github.com/Pratyush150/llm-faq-assistant) | Retrieval-grounded FAQ assistant: structure-aware chunking, hybrid dense + BM25 fused by reciprocal rank fusion, an explainable reranker, four named refusal guardrails, prompt-injection neutralisation of retrieved text, and an eval harness reporting recall@k, groundedness and refusal correctness. Stdlib only, no API key needed. | Python, stdlib only, RAG, BM25, RRF |
| [**workflow-automation-engine**](https://github.com/Pratyush150/workflow-automation-engine) | DAG workflow runner (`flowforge`): partial-failure semantics that separate failed, upstream_failed and skipped; retries that never repeat a permanent error; a circuit breaker; content-addressed idempotency with a three-state protocol; durable state and resume; DST-tested cron. Stdlib only. | Python, stdlib only, pytest |
| [**industrial-automation-suite**](https://github.com/Pratyush150/industrial-automation-suite) | Modbus/OPC-UA acquisition (`factorylink`): a validated tag database, register-range coalescing (38 tags to 7 requests), alarms with hysteresis and flood detection, a swinging-door historian on stdlib SQLite, OEE, a zero-build-step dashboard, and a write path that is shut by default. Codec tested against known byte patterns for all four word orders. | Python, Modbus TCP/RTU, OPC-UA, MQTT, SQLite |

---

## Product

Mobile apps and web applications, built by people who also write embedded real-time
code, so performance and reliability are not afterthoughts.

| Project | What it does | Stack |
|---|---|---|
| [**fleet-ops-dashboard**](https://github.com/Pratyush150/fleet-ops-dashboard) | Browser ground station for a mixed fleet: inline-SVG pan/zoom map with no tile server, ring-buffered trend charts, and alerts with enter/exit thresholds and dwell timers. Ships with a deterministic telemetry simulator — battery sag, RSSI path loss, GNSS degradation, five injected fault classes on a seed-derived schedule. | TypeScript, React, Vite, Tailwind, Vitest |
| [**ground-station-mobile**](https://github.com/Pratyush150/ground-station-mobile) | Phone-sized ground station that decodes MAVLink v1/v2 itself — CRC-16/MCRF4XX with CRC_EXTRA, resync after garbage, frames split across reads — ages every telemetry group separately so stale values never render as live, and runs a full simulated flight with no aircraft. | TypeScript, React Native, Expo, MAVLink |

---

## Measured against ground truth

Four repositories that exist to be checked rather than admired. Each one implements the
method from the protocol, then puts its own output next to an independent reference or a
public dataset's official metrics, and reports the gap.

| Project | The number, and what it is measured against | Stack |
|---|---|---|
| [**stereo-visual-slam**](https://github.com/Pratyush150/stereo-visual-slam) | Stereo VO and SLAM written from scratch — no ORB-SLAM, no g2o, no GTSAM, no Ceres. On KITTI raw drive `2011_09_30_drive_0027`, 1,106 frames over 694.7 m of OXTS ground truth: **1.256% translation error, 0.01092 deg/m rotation, ATE RMSE 1.276 m**, and 21 loop closures accepted out of 21 correct. Scored with the official KITTI metrics on a public dataset, so the figures are reproducible rather than asserted. | Python, NumPy, OpenCV, KITTI |
| [**pose-graph-slam**](https://github.com/Pratyush150/pose-graph-slam) | An SE(3) pose-graph optimiser with hand-derived Jacobians. On `sphere2500` — 2,500 poses, 4,949 constraints — **ATE goes from 27.93 m to 0.180 m in 10 iterations**, a 97.5% improvement. Cross-checked against a run of GTSAM 4.2 on the identical files; GTSAM appears exactly once, in an optional verification script. | Python, NumPy, SciPy (sparse solve only) |
| [**object-detection-benchmark**](https://github.com/Pratyush150/object-detection-benchmark) | COCO mAP implemented from the protocol — IoU sweep 0.50:0.05:0.95, crowd handling, area bands — and it **matches `pycocotools` bit for bit across 367,010 detections on 4,872 real val2017 images**, with `pycocotools` nowhere in the library path. Then the accuracy-versus-latency table that a single mAP number hides, across seven YOLOv8n variants on one CPU. | Python, NumPy, ONNX Runtime, COCO |
| [**swarm-path-planning**](https://github.com/Pratyush150/swarm-path-planning) | Multi-agent path finding on the standard MAPF benchmark maps: CBS, ECBS, and prioritised planning, with an independent validator that re-checks every plan and reports conflicts. Solutions are reported against a proven lower bound rather than against each other — 30 agents on `random-32-32-20` plan to sum-of-costs 637, **1.024x the lower bound**. | Python, NumPy |

---

## Capstones — one project, every decision

Longer builds whose point is the reasoning, not the result. Each carries a
`HOW_TO_THINK.md`, a decision journal recording at least one path that did not work, a
`DEBUG_PROTOCOL.md`, and an `INTERVIEW.md` answered from that repository's own code.
Every headline number is produced by code in the repo.

| Project | What it works through | Tests |
|---|---|---|
| [**object-detector-end-to-end**](https://github.com/Pratyush150/object-detector-end-to-end) | Data, training, evaluation, error analysis and deployment. A controlled leakage experiment worth **0.189 mAP50** — leaky test set 0.876, honest test set 0.687 — and a quantisation study where INT8 came out **slower**, because postprocess is 72% of the frame and inference only 17.5%. The naive version of the leakage experiment gave the wrong answer and is kept in the decision record. | 123 |
| [**camera-imu-rig-calibration**](https://github.com/Pratyush150/camera-imu-rig-calibration) | Intrinsics against known truth, the fronto-parallel confound, PnP degeneracy, and time-offset recovery from images and gyro alone (+30.000 ms injected, +28.258 ms recovered). Three results came out opposite to expectation and are documented as such — quaternion drift is the integrator, not float64. | 128 |
| [**monocular-visual-odometry**](https://github.com/Pratyush150/monocular-visual-odometry) | Tracking, scale, loop closure, filtering and a C++ port. Leads with the honest number: unit-scale monocular VO gives 30.34% KITTI translation error, and scale propagated from structure is *worse* than not scaling at all. Loop closure by appearance alone is **2.6% precise**; geometric verification takes it to 100%. | 116 |

---

## Learning in public

One chapter each, written to be read in order. Comments explain why a line exists, not
what it does.

[**cv01-pixels-to-edges**](https://github.com/Pratyush150/cv01-pixels-to-edges) ·
[**cv02-features-to-panorama**](https://github.com/Pratyush150/cv02-features-to-panorama) ·
[**cv03-backprop-to-cnn**](https://github.com/Pratyush150/cv03-backprop-to-cnn) ·
[**cv04-calibration-to-depth**](https://github.com/Pratyush150/cv04-calibration-to-depth)

---

## Tech stack

**Flight stacks** — PX4 · ArduPilot · Betaflight · MAVLink · MAVSDK · pymavlink · MAVROS · ULog · dataflash logs · QGroundControl · Mission Planner

**Robotics** — ROS 2 (rclpy, rclcpp) · ros2_control · TF2 · URDF / Xacro · Nav2 · rosbag2 · colcon

**Perception** — YOLO · TensorRT · ONNX Runtime · Hailo · OpenCV · multi-object tracking · Hungarian assignment · camera calibration

**SLAM & navigation** — LIO-SAM · Cartographer · RTAB-Map · point cloud processing · sensor extrinsics · time synchronisation · degeneracy analysis

**Control & estimation** — PID (anti-windup, filtered derivative) · cascaded loops · LQR · EKF · complementary and Madgwick filters · motor mixing · trajectory generation

**Simulation & testing** — Gazebo · PX4 SITL · AirSim · Isaac Sim · RViz2 · hardware-in-the-loop · scenario regression testing · pytest

**Industrial automation** — Modbus TCP / RTU · OPC-UA · MQTT · tag databases · alarm management · historians · OEE · SCADA dashboards

**Automation & AI** — RAG · hybrid retrieval · BM25 · vector search · embeddings · LLM APIs · eval harnesses · DAG orchestration · retries and idempotency

**Web & mobile** — TypeScript · React · React Native · Expo · Vite · Tailwind CSS · Node.js · Vitest · WebSocket · SQLite

**Languages** — Python · C++ · TypeScript · NumPy · Eigen · CMake · Linux · Docker

**Boards we write for** — NVIDIA Jetson · Raspberry Pi · Hailo-8 · STM32 · Pixhawk · Arduino · LiDAR · IMU integration · encoders

---

## Available for

- **Robotics & control** — ROS 2 and PX4/ArduPilot integration, MAVLink bridges, LiDAR SLAM, control and state estimation, edge perception on Jetson and Raspberry Pi
- **Simulation & testing** — Gazebo, Isaac Sim and AirSim environments, SITL setups, and scenario-driven regression suites that fail a build instead of surprising a pilot
- **Automation & AI** — Modbus/OPC-UA acquisition and dashboards, workflow engines with real retry and resume semantics, and retrieval-grounded assistants with an eval harness
- **Product** — React and TypeScript dashboards and React Native apps for machines in the field, with a typed domain model and a simulated backend so the UI is testable without the machine

Not available for: building, wiring, assembling or repairing hardware, PCB design,
component selection or mechanical work. We write the software that runs on your boards,
not the boards.

Every engagement starts with a paid diagnosis and a written root-cause report you can act
on whether or not we do the implementation.

---

## Contact

- Email: **pratyushvatsa2018@gmail.com**
- Portfolio: **https://pratyush150.github.io**
- LinkedIn: **www.linkedin.com/in/pratyush-vatsa-a03292372**
- Fiverr: **(https://www.fiverr.com/users/pratyush_vatsa1)**

Send the system, the versions, and the evidence — a log, a bag file, a register map, a
sample of the corpus, a photo of how it is wired. That gets you a useful answer, and it
is all we need: your hardware stays where it is.
