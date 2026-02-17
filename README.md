
---

# 🚗 DF Robot Differential Drive Platform (ROS 2)

## 📌 Overview

A differential drive mobile robot built on the DF Robot platform.

* **Main computer:** Raspberry Pi 4 Model B (2GB RAM, 32GB MicroSD)
* **Operating system:** Ubuntu Server 22.04 (aarch64)
* **Middleware:** ROS 2 Humble Hawksbill

<img width="1328" height="1770" alt="image" src="https://github.com/user-attachments/assets/8c37ac07-7c1d-4411-bb66-a43c0705f334" />

---

## 📁 Repository Structure

```
DF_Robot/
│
├── l298n_ros2_control/              # ROS 2 hardware_interface plugin
│   ├── CMakeLists.txt
│   ├── package.xml
│   ├── include/
│   │   └── l298n_hardware/
│   │       └── l298n_system.hpp
│   ├── src/
│   │   └── l298n_system.cpp
│   └── plugin_description.xml       # ros2_control plugin description
│
├── l298n_bringup/                   # Robot bringup package
│   ├── CMakeLists.txt
│   ├── package.xml
│   ├── launch/
│   │   └── bringup.launch.py
│   ├── config/
│   │   │   └── diff_drive.yaml
│   └── urdf/
│       └── robot.urdf.xacro
│
└── README.md
```

---

## 🏗 Architecture

```
/diff_drive_controller
        ↓
ros2_control (controller_manager)
        ↓
L298NSystem (hardware_interface::SystemInterface)
        ↓
pigpio (daemon mode)
        ↓
GPIO (PWM + direction pins)
        ↓
L298N motor driver
```

---

## 🚀 Features

* Velocity command interface
* Position and velocity state interfaces
* Full compatibility with `diff_drive_controller`
* PWM control via pigpio daemon
* Designed for aarch64 (Raspberry Pi 4/5)

---

## 📦 Requirements

* ROS 2 Humble Hawksbill
* ros2_control
* ros2_controllers
* pigpio (built from source for aarch64)

---

## ⚠ Notes

* No wheel encoders → position is estimated by integrating velocity (open-loop control)
* Requires pigpio daemon running
* `diff_drive_controller` subscribes to `TwistStamped`

---



