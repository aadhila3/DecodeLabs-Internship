# Industrial IoT Engineering Portfolio: ESP32 Core Tracks

This repository documents the systematic development of industrial-grade embedded systems utilizing the ESP32 microcontroller architecture. Over a three-week progression, the firmware evolved from basic localized input-process-output blocks to a fully decoupled, cloud-connected telemetry edge node.

---

## 📂 Repository Architecture

```text
├── week1/                # Core Architecture & Local Processing Baseline
│   ├── task1/
│   ├── task2/
│   ├── task3/
│   ├── task4/
│   └── task5/            # Standalone Signal Acquisition Tasks
├── week2/                # Closed-Loop Actuation & Process Shielding
│   ├── README.md         # Automated Irrigation Controller Documentation
│   ├── automated_irrigation_control.ino # Hysteresis State Machine Firmware
│   ├── diagram.json      # Virtual Hardware Layout Configuration
│   └── wokwi-project.txt # Wokwi Project Metadata Tracking
└── week3/                # Distributed Networks & Cloud SCADA Telemetry
    ├── README.md         # Cloud-Connected Security Node Specification
    ├── sketch.ino        # Non-Blocking Network Stack Edge Firmware
    ├── diagram.json      # Virtual Acoustic Barrier Circuit Topology
    └── wokwi-project.txt # Wokwi Project Metadata Tracking
└── README.md             # Master Portfolio Directory & System Overview
