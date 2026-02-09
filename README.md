# Smart Power Distribution & Monitoring Unit ⚡

## 📖 Overview
This project is an industrial-grade **Power Distribution and Monitoring Unit** designed to manage high-voltage DC inputs (up to 40V) for robotic or automotive applications. 

Unlike standard power distribution boards, this unit features **active intelligent monitoring**. It is centered around an **STM32F103 (ARM Cortex-M3)** to sample current and temperature data, providing a hardware platform capable of proactive system shutdown before thermal runaway or over-current events occur.

### 🎯 Key Capabilities
* **Wide Input Range:** Designed to handle **12V–40V DC** input with dedicated surge protection.
* **Smart Protection:** Features **Reverse Polarity Protection** using a P-Channel MOSFET (IRF4905) to minimize voltage drop compared to traditional diode-based solutions.
* **High-Power Switching:** Capable of driving high-current external loads via an **IRFP4468 MOSFET** and a dedicated **TC4427 Gate Driver**.
* **Integrated Telemetry:** Supports power consumption monitoring via a **1mΩ Shunt + INA180 Amplifier** and thermal tracking through a **6-zone NTC matrix**.

---

## ⚙️ System Architecture
The hardware architecture is divided into four main functional stages: **Protection, Regulation, Control, and Actuation**.

### 1. Power Stage
* **Input Protection:** Includes an automotive blade fuse and TVS Diode (D3) to clamp voltage spikes.
* **Reverse Polarity:** Implemented via **IRF4905** (Q1) for high-efficiency protection.
* **Regulation Logic:** Two-stage step-down architecture:
    1.  **Buck Converter (U1 - LM2596S-ADJ):** Steps 40V down to 12V for the Gate Driver.
    2.  **LDO (U2 - AMS1117-3.3):** Steps 12V down to 3.3V for the MCU and sensor suite.

### 2. Control & Sensing
* **Microcontroller:** Powered by an **STM32F103C8Tx** (U5).
* **Current Monitoring:** High-side sensing using an **INA180A1** (U3) amplifier across a **1mΩ shunt resistor** (R10).
* **Thermal Monitoring:** Features **6x NTC Thermistors** (TH1-TH6) placed at critical points for system-wide temperature tracking.

---

## 🔌 Hardware Specifications

| Parameter | Value | Component |
| :--- | :--- | :--- |
| **Input Voltage** | 12V - 40V DC | XT60 / Terminal Block |
| **Logic Voltage** | 3.3V | AMS1117-3.3 |
| **Gate Drive Voltage** | 12V | TC4427VOA |
| **Main Switch** | 100V / 195A (Max) | IRFP4468PbF |
| **Current Sense** | High-Side, Analog | INA180 + 1mΩ Shunt |
| **Protection** | Reverse Polarity, Fuse, TVS | IRF4905, SMBJ43A |

---

## 🛠️ PCB Design (KiCad)
The PCB design focuses on high-current integrity and thermal management.

### Design Considerations:
* **Trace Width:** Critical high-current paths utilize **polygons and copper pours** to handle high amperage without excessive heat generation.
* **Thermal Management:** Integrated thermal vias under the LDO and MOSFETs to facilitate heat dissipation to the ground plane.
* **Noise Reduction:** Optimized placement of decoupling capacitors (C2, C3, C11) near the STM32 and high-speed driver pins to minimize switching noise.

---

## 📂 Repository Structure
