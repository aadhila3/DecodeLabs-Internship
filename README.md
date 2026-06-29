# Industrial IoT Engineering Portfolio: ESP32 Core tracks

This repository documents the systematic development of industrial-grade embedded systems utilizing the ESP32 microcontroller architecture. Over a three-week progression, the firmware evolved from basic localized input-process-output blocks to a fully decoupled, cloud-connected telemetry edge node.

---

## 📂 Repository Architecture

```text
├── week one/             # Core Architecture & Local Processing Baseline
│   ├── diagram.json      # Virtual Hardware Layout Configuration
│   └── week_one.ino      # Standalone Signal Acquisition Firmware
├── week two/             # Closed-Loop Actuation & Process Shielding
│   ├── README.md         # Automated Irrigation Controller Documentation
│   ├── diagram.json      # Virtual Hardware Layout Configuration
│   └── irrigation.ino    # Hysteresis State Machine Firmware
└── week three/           # Distributed Networks & Distributed SCADA Telemetry
    ├── README.md         # Cloud-Connected Security Node Specification
    ├── diagram.json      # Virtual Acoustic Barrier Circuit Topology
    └── telemetry_node.ino# Non-Blocking Network Stack Edge Firmware
