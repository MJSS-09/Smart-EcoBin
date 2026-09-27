# 🗑️Smart EcoBin — IoT-Based Smart Waste Segregation Dustbin

An Arduino Uno–based dustbin that opens its lid automatically when waste is presented, senses whether the waste is wet or dry, and mechanically diverts it into the correct compartment — while continuously monitoring how full each compartment is and raising a distinct beep-coded alert when service is needed.

Designed and simulated end-to-end in **Cirkit Designer**.

---

## Overview

Manually sorting household and public waste is inconsistent, and bins are usually emptied on a fixed schedule rather than when they're actually full. Smart EcoBin solves both problems at the source:

- Segregates waste automatically the moment it's dropped in
- Reports fill status with an unmistakable, compartment-specific beep pattern
- Gives constant real-time feedback on an onboard OLED display

---

## Features

- **Touch-free lid** — opens automatically when waste is presented, closes on its own
- **Automatic wet/dry segregation** — a capacitive moisture sensor classifies the waste and a servo-actuated flap routes it to the correct compartment
- **Independent fill-level monitoring** — two dedicated ultrasonic sensors watch the dry and wet compartments separately
- **Beep-coded alerts** — 1 beep (dry full), 2 beeps (wet full), 3 beeps (both full), each firing once per event
- **Live OLED status** — shows system state at every stage, from startup to alerts

---

## Hardware Components

| Component | Qty | Function |
|---|---|---|
| Arduino Uno R3 | 1 | Central controller |
| HC-SR04 Ultrasonic Sensor | 3 | Lid trigger + dry/wet compartment fill-level sensing |
| Capacitive Soil Moisture Sensor | 1 | Classifies waste as wet or dry |
| SG90 Micro Servo Motor | 2 | Lid actuation + diverter flap |
| Piezo Buzzer | 1 | Fill-level alert tones |
| 0.96" OLED Display (SSD1306, I2C) | 1 | Real-time status display |

---

## Pin Mapping

| Signal | Arduino Pin | Role |
|---|---|---|
| Bottom Ultrasonic — Trig / Echo | D2 / D3 | Detects an object near the main lid |
| Dry-Side Ultrasonic — Trig / Echo | D4 / D5 | Monitors dry compartment fill level |
| Wet-Side Ultrasonic — Trig / Echo | D6 / D7 | Monitors wet compartment fill level |
| Buzzer | D8 | Audible fill-level alerts |
| Diverter Flap Servo | D9 | Routes waste to wet or dry side |
| Lid Servo | D10 | Opens/closes the main lid |
| Moisture Sensor | A0 | Wet vs. dry classification |
| OLED Display | SDA / SCL (I2C) | Status display, address 0x3C |

---

## Working Principle

### 1. Initialization and Ready State
On power-up, the OLED shows a startup message while the servos move to default positions. The system then settles into an idle "ready for waste" state.


### 2. Waste Detection and Lid Operation
The bottom ultrasonic sensor detects an object within its trigger distance, the lid opens, stays open briefly, then closes automatically.

### 3. Automatic Waste Segregation
The moisture sensor reading is compared against a threshold. Wet waste swings the flap one way, dry waste the other, with the OLED confirming the classification.

### 4. Compartment Fill-Level Monitoring and Alerts
The two top-mounted ultrasonic sensors independently track fill level. Crossing the threshold triggers a beep pattern unique to that condition, plus a persistent OLED message — firing once per event rather than repeating continuously.


---

## Design and Simulation Tool

Built and validated entirely in **Cirkit Designer** — every component was placed and wired, and the design was run to confirm the lid, segregation, and alert logic behaved as intended before finalizing.

---

## Advantages

- Touch-free lid operation reduces contact with a potentially unhygienic surface
- Segregation happens automatically, removing reliance on correct manual sorting
- Distinct beep codes tell a caretaker which compartment is full without inspection
- Constant OLED feedback aids everyday use and troubleshooting
- Built entirely from low-cost, widely available components

---

## Applications

- Households and residential complexes
- Offices, cafeterias, and common areas
- Educational institutions and hostels
- Public spaces and parks as part of a smart-city waste initiative

---

## Limitations

- Operates standalone; no wireless reporting of fill status to a remote dashboard or municipal staff
- Waste is classified using a single moisture reading at the point of drop, which may reduce accuracy for borderline items
- Mechanical wear on the SG90 servos over extended, high-frequency use would need monitoring in a long-term deployment

---

## Future Scope

- Add a Wi-Fi module (e.g. ESP8266/ESP32) for remote monitoring and notifications
- Add additional sensing (e.g. weight, or multiple moisture readings) to improve classification accuracy
- Add solar or battery-backed power for outdoor or off-grid deployment
- Build a mobile app or web dashboard for remote fill-level tracking and collection history
- Add GPS and cellular connectivity for fleet-level tracking across multiple bins in a smart-city routing system

---

## 👨‍💻 Author

**Mallampally Jayantha Siva Srinivas** | **B.Tech | Electronics and Communication Engineering (ECE)**
ESSCI-Certified Embedded Fullstack & IoT Analyst , SRM University(AP)
---
