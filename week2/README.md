# Week 2 Project: Automated Irrigation Controller (Actuator Logic)

This repository contains the firmware and virtual hardware layout for an industrial-grade, closed-loop automated irrigation system. It translates continuous environmental data into reliable mechanical action while implementing safety shielding to prevent hardware failure.

## 🚀 Live Simulation Link
Click the link below to view, interact with, and run the live circuit simulation:
👉 **[click here to view the live wokwi simulation](https://wokwi.com/projects/468095841084995585)**

---

## 🛠️ Key Embedded Engineering Features Implemented

* **Active-LOW Bootup Protection:** Real opt-isolated relays often default to an Active-LOW state. During microcontroller bootup or reset, GPIO pins can float or stay LOW, causing an accidental system flood every time power cycles. This code enforces a safe initialization sequence by forcing the pump control pin `HIGH` (Pump OFF) *before* declaring it as an output pin.
* **Exponential Moving Average (EMA) Digital Filter:** Microcontrollers like the ESP32 generate high-frequency switching noise from their internal CPU and wireless operations, causing fluctuating analog sensor values. The code rejects these fast transients by passing raw ADC data through an EMA smoothing filter using a smoothing factor ($\alpha = 0.2$).
* **Data Normalization & Constrain Protection:** Raw ADC values vary by soil type and cable lengths. The logic uses calibrated anchors (`ADC_dry` and `ADC_wet`) to map the filtered voltage values cleanly to a 0%–100% moisture range. This mapping is wrapped in a `constrain()` function to eliminate out-of-bounds math errors from unexpected noise spikes.
* **Dual-Threshold Hysteresis State Machine:** Simple single-threshold logic triggers a dangerous real-world bug called "relay chattering" when soil moisture levels hover right on the threshold limit (e.g., 29.9% to 30.1%). This fast clicking can thermally damage pump motors and weld mechanical relay contacts shut. This project solves this by creating a deadband zone: the pump turns ON only when moisture drops below 30%, and turns OFF only when moisture rises past 45%. Between 30% and 45%, it holds its previous state.

---

## 📋 Virtual Pinout Layout

| Component Pin | ESP32 GPIO Pin | Description |
| ------------- | -------------- | ----------- |
| Potentiometer (SIG) | GPIO 34 (D34) | Analog input simulating the Soil Moisture Sensor |
| Relay Module (IN) | GPIO 23 (D23) | Digital output driving the Active-LOW relay actuator |
| Relay Module (VCC) | 5V / VIN | 5V logic supply power rail |
| Relay Module (GND) | GND | Common reference ground rail |

---

## 🔒 Industrial Note: True Galvanic Isolation
To protect sensitive microcontroller silicon from the massive high-voltage reverse inductive spikes (Back EMF) generated when a pump motor shuts off, this system architecture is designed for true galvanic isolation. In a physical build, the **JD-VCC jumper cap must be completely removed** from the relay board. This ensures that the MCU only drives the low-power internal optocoupler LED using light across a non-conductive physical gap, breaking any common electrical connection or ground loop with the high-voltage actuator side.
