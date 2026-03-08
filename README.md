# VAMP-Guard
> AI + DSP powered energy vampire detection system for institutional infrastructure using NILM, TinyML, and AIoT

![Status](https://img.shields.io/badge/Status-In%20Development-yellow)
![License](https://img.shields.io/badge/License-MIT-blue)
![SDG](https://img.shields.io/badge/SDG-7%20%7C%2012%20%7C%2013-green)

---

## Overview

Energy conservation is increasingly recognized as a more sustainable and cost-effective strategy than energy generation, particularly in developing economies where transmission and generation losses can exceed 20–30%, and average end-use efficiency remains low.

In institutional environments such as colleges and hostels, a significant portion of electricity wastage arises from **"energy vampires"** — devices such as mobile chargers, laptop adapters, air conditioners, and computers that remain powered ON without active usage. While individual standby losses are small (typically 0.1–5 W per device), aggregated across hundreds of users and extended over time, the cumulative loss becomes substantial, resulting in avoidable financial and environmental costs.

VAMP-Guard is a dynamic AI-powered energy monitoring and intervention system that combines **Digital Signal Processing (DSP)** and **Artificial Intelligence/Machine Learning (AI/ML)** to detect, analyze, and mitigate phantom and unauthorized energy consumption in institutional settings.

---

## The Two Core Problems

| Problem | Description |
|---|---|
| Energy Vampires | Devices ON with no active load, consuming standby power silently |
| Unauthorized Usage | Devices fully active but running outside permitted hours (ACs, PCs after hours) |

---

## Core Features

### 1. Signal-Based Appliance Differentiation Using DSP
Electrical load signatures are analyzed using DSP techniques to detect spike patterns and waveform characteristics, enabling differentiation between:
- Active device usage
- Standby consumption
- Switch-ON but no-load conditions

### 2. AI-Based Appliance Identification and Anomaly Detection
- Model pretrained on the **UCI Machine Learning Repository Household Power Consumption Dataset**
- Classifies appliance usage patterns from electrical signals
- Performs time-aware anomaly detection based on institution-specific permitted hours to identify:
  - AC units left ON outside permitted hours
  - Computers powered unnecessarily
  - Switches activated without load
  - Unauthorized activity in institutional spaces
- Automated alerts sent to responsible individuals upon detection

### 3. Behavioral Incentivization System
- Hostel rooms with the lowest verified power wastage are rewarded (e.g., vouchers)
- Encourages competitive and sustained energy conservation behavior

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python |
| Data | UCI Household Power Consumption Dataset |
| Signal Processing | DSP-based load signature analysis |
| Machine Learning | NILM / NILMTK, scikit-learn |
| Anomaly Detection | Time-aware ML models |
| Alert System | Automated notifications to responsible personnel |
| Hardware (Future) | Smart Electric Meters, STM32 |
| Edge Deployment (Future) | TinyML, TensorFlow Lite |


---

## System Architecture
```
Smart Meter / UCI Dataset
        ↓
DSP Signal Processing
(Load signature extraction)
        ↓
NILM-based Device Classification
        ↓
Time-Aware Anomaly Detection
(Vampire load / Unauthorized usage)
        ↓
Alert System → Responsible Individual
        ↓
(Future) TinyML on Smart Meter → Autonomous Socket Control
```

---

## Project Roadmap

### Software Phase
- [ ] UCI dataset exploration and preprocessing
- [ ] NILMTK integration
- [ ] Vampire load detection model
- [ ] Unauthorized usage detection (time-aware)
- [ ] Admin event override mode
- [ ] Scheduled exception windows
- [ ] Alert system implementation
- [ ] Web dashboard (Flask)

### Hardware Phase (Future)
- [ ] TinyML model compression and deployment
- [ ] Smart meter embedded inference
- [ ] Autonomous socket control
- [ ] Real institutional data collection and fine-tuning

---

## Known Limitations and Solutions

### Plug Detection in Powered-Off Sockets

**Limitation**
When the system autonomously cuts power to a socket, NILM becomes blind to any device subsequently plugged in — no current flows, so no signature can be detected.

**Solution**
A low-cost capacitive sensor IC (e.g., TTP223) integrated directly inside the switch box detects plug insertion through capacitive change at the socket terminals, independent of current flow. Upon detection, the system briefly restores power, NILM classifies the device, and autonomously decides whether to allow or cut power again.

**Why this works**
- Capacitive sensor operates passively without current flow
- Bare IC footprint is negligible — easily fits on a custom PCB inside standard Indian switch boxes
- Cost per socket is approximately ₹20–50, justified in high-value lab environments
- Maintains full system awareness and control integrity

**Phased Deployment Note**
Initial deployment targets computer labs and AC labs where:
- Device loads are high value and easily measurable
- Permitted hours are clearly defined
- Sensor cost is justified by energy savings per socket
- Clean labeled data is available for model fine-tuning

---

## Future Scalability

- **Smart Meter Integration** — Embedding TinyML directly into smart electric meters for real-time autonomous socket control
- **Lift Sleep Mode** — Automated switching of lifts into S2 sleep mode using ultrasonic sensor feedback and predictive wake intelligence
- **Smart Street Lights** — Weather and sunrise/sunset based dynamic street light control
- **City-Level Analytics** — Integration with municipal energy management infrastructure

---

## Technological Relevance

With AI-enabled smart grids, IoT-based monitoring, and edge computing becoming mainstream, integrating DSP-based signal analysis with anomaly detection aligns with modern smart infrastructure design.

According to global energy reports, standby power can contribute up to **5–10% of total building electricity consumption**. In large institutions, even a 5% reduction translates into significant annual savings and measurable carbon footprint reduction.

VAMP-Guard moves beyond static monitoring by implementing a dynamic, adaptive, self-learning model capable of:
- Continuous behavioral analysis
- Time-aware anomaly detection
- User-level accountability
- Automated or semi-automated intervention

---

## SDG Alignment

| Goal | Contribution |
|---|---|
| 🌍 SDG 7 – Affordable and Clean Energy | Improves energy efficiency and reduces unnecessary electricity demand |
| 🌱 SDG 12 – Responsible Consumption and Production | Introduces measurable accountability and incentive systems |
| 🌡 SDG 13 – Climate Action | Reduces carbon emissions indirectly by lowering energy demand |

---

## Research Foundation

This project is grounded in **Non-Intrusive Load Monitoring (NILM)** — an established field of electrical load disaggregation research. The approach extends NILM specifically toward:
- Institutional energy vampire detection
- Time-context anomaly detection
- AIoT edge deployment on smart meters

---

## Impact Statement

VAMP-Guard transforms energy conservation from passive awareness into active, intelligent intervention. By combining DSP signal intelligence, AI-based anomaly detection, behavioral economics, and scalable embedded systems, the project provides a practical pathway toward institutional energy sustainability in the era of smart technology.

This is not merely a monitoring tool — it is a **self-evolving energy governance ecosystem** designed for present infrastructure and scalable to future smart cities.

---

## Author

**Jaivant R**
1st Year ECE Student
Rajalakshmi Institute of Technology, Chennai
*Project conceptualized and developed independently*
*If you find this work useful, please star the repository and cite appropriately.*

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
