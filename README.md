<!-- MAIN TITLE -->
<h1 align="center">
   <b>IN-SPACe CanSat 2024–25</b> 🛰️
</h1>

<!-- HEADER -->
<h1 align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Orbitron&size=36&color=00C4FF&center=true&vCenter=true&width=900&height=100&duration=4500&lines=CanSat+Avionics+and+Sensor+Subsystem" />
</h1>

<h3 align="center"> <b>Avionics Team</b> | <b>PSIT Vyomnauts</b></h3>

<p align="center">
  <img src="https://github.com/user-attachments/assets/8d160b36-acae-44d0-b3cd-ac17c9cdaa77" width="350" alt="CanSat PCB"/>
</p>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/Onboard Controller-Raspberry%20Pi%20Pico%202-orange?style=for-the-badge"></a>
  <a href="#"><img src="https://img.shields.io/badge/Secondary Controller-Arduino%20Nano%2033%20BLE%20Sense%20REV%202-lightpink?style=for-the-badge"></a>
  <a href="#"><img src="https://img.shields.io/badge/Designed%20With-EasyEDA-blue?style=for-the-badge"></a>
  <a href="#"><img src="https://img.shields.io/badge/Communication-XBee3%20Pro%20,%20LoRa%20SX1262-lightgreen?style=for-the-badge"></a>
  <a href="#"><img src="https://img.shields.io/badge/Category-CanSat%20Avionics-red?style=for-the-badge"></a>
</p>

---

##  Project Overview

The **CanSat Avionics and Sensor Subsystem** was designed for the **IN-SPACe CanSat 2024–25** competition as a fully integrated, robust, and efficient onboard electronics system.  
It performs **telemetry**, **data logging**, **sensor fusion**, and **power management**, forming the **core intelligence** of our CanSat.

---

##  Component Summary

| Component | Function |
|------------|-----------|
| **Raspberry Pi Pico 2** | Main flight controller |
| **BMP390** | Altitude / Pressure / Temperature |
| **BNO085** | IMU – Orientation and motion |
| **INA219** | Power / Current / Voltage monitoring |
| **DS1307** | Real-time clock |
| **SD Card Module** | Data logging (Silicon casing Black-box protected) |
| **BharatPi NavIC GPS** | Position and navigation |
| **MQ135 / MQ2** | Gas and smoke sensing |
| **Quectel EC200U** | Cellular telemetry backup |
| **XBee 3 Pro, LoRa SX 1262** | RF telemetry |
| **Li-ion Battery** | Power source |
| **Level Shifters** | I²C/UART voltage matching |
| **LEDs & Buzzer** | Indicators and feedback |

---

##  System Architecture

<p align="center">
  <img width="1000" height="600" alt="Blank diagram (9)" src="https://github.com/user-attachments/assets/74a6bf0a-0a04-4b18-99ff-b3eeb8283efb" />
</p>
---

## Hardware Development

### *Schematic Design*
<p align="center">
  <img src="https://github.com/user-attachments/assets/b2f62daa-2211-4e16-8783-952fc3e8d39e" width="700" alt="Schematic Layout">
</p>

---

### *PCB Layout*
<p align="center">
<img width="400" height="400" alt="PCB_PCB_PCB_RAHUL_CANSAT_PCB_2_2025-09-04_2025-11-08 1" src="https://github.com/user-attachments/assets/08e27158-68d5-4bde-8f69-fb1a5759b8e7" />
</p>
<p align="center">
 <img width="400" height="400" alt="PCB_PCB_PCB_RAHUL_CANSAT_PCB_2_2025-09-04_2025-11-08k 1" src="https://github.com/user-attachments/assets/28c439d8-ff0a-4026-b84d-81e8be975d75" />
</p>

---

### *Final Assembly*
<p align="center">
<img src="https://github.com/user-attachments/assets/4235ef58-31bc-4e22-acd1-9bff17dca7be" width="400">
<img src="https://github.com/user-attachments/assets/5fffc7b6-dd2c-4c55-9b93-07767f6a5072" width="400">

</p>


---

##  Power and Signal Management

- **Input Voltage:** 7.4V Li-ion Battery  
- **Output Rails:** Regulated 5V and 3.3V  
- **Signal Conversion:** Integrated bidirectional level shifters for I²C & UART  
- **Indicators:** Status LEDs and buzzer alerts  
- **Protection:** Kapton Tape for insulation, Fused power lines & reverse polarity safety  

---

## Communication and Telemetry

- **Primary Link:** XBee3 Pro RF (2.4 GHz), LoRa SX 1262 (433MHz) 
- **Secondary Link:** Quectel EC200U (4G LTE Sends SMS of satellite's Coordinates)  
- **Telemetry Data:** Altitude, pressure, GPS coordinates, IMU, voltage, temperature, gaseus data (smoke,CO2,NH3,Benzene etc.) 
- **Protocol:** UART serial communication and SPI communication

---

##  Data Logging System

- High-speed SPI interface with SD card module  
- Logs environmental, motion, and telemetry data at fixed intervals  
- Enclosed in **impact-resistant silicon black-box casing**  
- Timestamping through DS1307 RTC  

---


## Sensor Role and Functionality in Mission Logic

The **BMP390** (barometric sensor) and **BNO085** (IMU) work together to compute altitude through **pressure and acceleration fusion**.  
This data feeds the **flight state logic**, allowing the onboard computer to autonomously detect **ascent**, **apogee**, and **descent** phases of flight.

The **MQ series sensors (MQ135 and MQ2)** measure **gaseous concentrations** like CO₂, NH₃, and methane.  
These readings are used as part of an **experimental payload** to study atmospheric gas variation during flight.

The **BharatPi NavIC GPS** continuously provides **real-time coordinates** for position tracking, which is crucial for **recovery operations** after landing.

The **secondary controller (Arduino Nano 33 BLE Sense REV 2)** acts as a **failsafe** for recovery operations, ensuring critical systems like telemetry and parachute deployment remain operational even if the primary controller fails.

Similarly, the **LoRa SX1262** functions as a **secondary telemetry module**, maintaining long-range communication redundancy alongside the primary XBee3 Pro module.

---

## Testing and Validation

1. ✅ **Power Test:** Verified voltage and current stability through INA219  
2. ✅ **I²C Scan:** All sensors detected (BMP390, BNO085, INA219, DS1307)  
3. ✅ **Calibration:** BNO085 and BMP 390 auto-calibration completed successfully  
4. ✅ **Gas Sensors:** MQ2 and MQ135 calibrated for clean-air baselines  
5. ✅ **GPS Test:** NavIC GPS fix and tracking verified under open sky  
6. ✅ **Telemetry:** Dual-link (XBee) data verified during range  test and drop test
7. ✅ **Pressure Chamber Test:** The entire avionics module was successfully tested in a **custom pressure chamber** to simulate **high-altitude low-pressure conditions**.  
   Sensor data (BMP390 pressure-altitude readings) were verified for accuracy and consistency, confirming the system’s **altitude measurement reliability** under simulated flight conditions.

---

## Design Platform

- Designed and simulated in **EasyEDA**  
- Verified using **JLCPCB DRC** and **DFM checks**  
- 2-layer circular PCB optimized for **CanSat structure integration**  
- Supports direct stacking with payload and recovery modules  

---

<!-- 🏆 AWARD SECTION -->
<h2 align="center">🏆 Achievements</h2>

<h3 align="center">
   <img src="https://readme-typing-svg.herokuapp.com/?font=Orbitron&size=25&color=FFD700&center=true&vCenter=true&width=850&height=70&duration=5000&lines=🏅+Awarded+Best+Design+Award+🏅;Recognized+for+Best+Telemetry+and+GPS+Data" />
</h3>

<h3 align="center">
  <b>At IN-SPACe CanSat Student India Competition 2024–2025</b>
</h3>

---

## 👨‍🚀 Developed By

**Avionics Team — PSIT Vyomnauts**

- Arya Mishra (https://www.linkedin.com/in/arya-mishra-43307525a)
- Rahul Kumar (https://www.linkedin.com/in/rahul-kumar-rk212004)
- Riya Verma (https://www.linkedin.com/in/riya-verma-641230317)
- Lavitra Sahu (http://techarcanist.com)
- Shikha (https://www.linkedin.com/in/shikha2006)

---

<h1 align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Orbitron&size=28&color=00FFAA&center=true&vCenter=true&width=850&height=70&duration=4500&lines=Innovation+in+Every+Orbit+🛰️;Precision+in+Every+Design+⚙️;Excellence+in+Every+Launch+🚀" />
</h1>
