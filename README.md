# NV-Optical-Readout-TIA

This repository documents the development of an **optical readout system for NV-diamond sensors** using a **BPW34 photodiode**, a **MCP607-based transimpedance amplifier (TIA)**, and both **ESP32** and **ADS1115** ADCs for signal acquisition.

The goal is to explore **magnetic-field-induced fluorescence quenching** without microwave excitation, and to develop a robust, low-noise analog readout chain for future integration with ODMR and lock-in techniques.

---

## 📐 Project Overview

### Hardware
- **Photodiode:** BPW34, reverse-biased.
- **Op-Amp:** MCP607, low-noise rail-to-rail operational amplifier.
- **Feedback Network:** Configurable Rf (220kΩ–1MΩ) and Cf (3.3pF–10nF) for gain/bandwidth tuning.
- **ADC:** 16-bit ADS1115 via I²C (ESP32 interface).
- **Magnet setup:** 3D-printed holder with M4 screw for variable magnetic field control (up to 1T).

### Firmware
Implemented in **PlatformIO (Arduino framework)** for both:
- **ESP32 internal ADC** testbench.
- **ADS1115 high-resolution readout**, with:
  - noise calculation (`σ = sqrt(E[v²] - (E[v])²)`)
  - exponential filtering
  - CSV data logging for Python analysis

### Data Analysis
- Real-time noise comparison between ADCs
- Field-dependent fluorescence intensity (ΔI/I vs B)
- RMS noise tracking and SNR computation

---

## 🧮 Example result

| Parameter | ESP32 ADC | ADS1115 |
|------------|------------|----------|
| Resolution | 12-bit | 16-bit |
| RMS Noise | ~6.6 mV | ~0.34 mV |
| SNR | – | +26 dB |
| Dynamic Range | 0–2.6 V | 0–4.096 V |

---

## 🧰 Repository Contents
| Folder | Description |
|--------|--------------|
| `hardware/` | TIA schematics, PCB, and 3D mechanical designs |
| `firmware/` | ESP32 & ADS1115 readout code, noise and quenching measurement scripts |
| `data/` | Raw CSVs and processed datasets |
| `docs/` | Reports and experimental summaries |
| `scripts/` | Python utilities for plotting and filtering data |

---

## 🧲 Roadmap
- [ ] Add lock-in detection mode (software modulation)
- [ ] Integrate temperature and light sensors for stabilization
- [ ] Migrate from ADS1115 to ADS131M04 (24-bit, multi-channel)
- [ ] Implement ROS2 node for remote NV-sensor readout
- [ ] PCB v2: modular, low-noise layout for multiple photodiodes

---

## 🧑‍🔬 Author
**Samuel Sánchez Moreno**  
Hochschule Esslingen – Fraunhofer IAO Project  
Research focus: optical sensing, low-noise analog design, NV-center magnetic readout.
