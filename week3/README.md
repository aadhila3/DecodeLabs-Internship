# Week 3 Project: Cloud-Connected Security Node (IoT Telemetry)

This repository contains the production-grade edge firmware and virtual circuit topology for a Cloud-Connected Security Node. The system utilizes an ESP32 microcontroller paired with an HC-SR04 ultrasonic distance sensor to perform real-time acoustic time-of-flight monitoring of physical boundaries, streaming telemetry to a centralized cloud dashboard.

## 🚀 Live Simulation Link
Click the link below to view, interact with, and execute the live virtual circuit architecture:
👉 **https://wokwi.com/projects/468095841084995585**

---

## 🛠️ Key Embedded Engineering Features Implemented

* **Blocking Bootup Network Handshake:** To prevent cascading telemetry dropouts during initialization, the firmware blocks the main execution loop until a local Wi-Fi connection and IP address lease are successfully established. A software safety threshold is implemented: if the node fails to connect within 150 consecutive attempts, it automatically invokes a hardware-level `ESP.restart()` to restore network stack stability.
* **Non-Blocking Temporal Processing (`millis()` over `delay()`):** Utilizing standard blocking delays like `delay(5000)` halts the entire CPU core, rendering the security boundary completely blind to intrusions for 5 seconds. This architecture replaces blocking delays with a background delta clock via `millis()`, allowing the local edge engine to continuously execute acoustic tracking while checking network status independently.
* **Deterministic Static Memory Allocation:** To safeguard the embedded system against long-term heap fragmentation and potential runtime memory crashes over extended deployment lifespans, the firmware completely avoids dynamic `String` objects. Floating-point sensor measurements are serialized into static character arrays via `dtostrf()`, ensuring zero-allocation memory stability.
* **Strict TTL Acoustic Time-of-Flight Ranging:** Physical boundary distance is determined through precise microsecond-level hardware triggers. The ESP32 drives a 10µs High TTL pulse to the HC-SR04 `Trig` pin, prompting an 8-cycle burst of 40kHz ultrasonic sound waves. The `Echo` pin return pulse duration is evaluated to compute the target distance using the sonic velocity mapping multiplier ($0.0343\text{ cm/\mu s}$).

$$\text{Distance } (d) = \frac{\text{Duration}}{2} \times 0.0343$$

---

## 📋 Virtual Pinout Layout Configuration

| Component Pin | ESP32 GPIO Pin | Wire Direction | Description |
| :--- | :--- | :--- | :--- |
| **VCC** | 5V / VIN | Input Power | Main 5V DC power bus rail |
| **Trig** | GPIO 18 | Output from MCU | Hardware trigger pulse line |
| **Echo** | GPIO 5 | Input to
