# 🌊 Smart Single-Pulse Water Level Controller (NE555 + 2N2222)

![Project Status](https://img.shields.io/badge/Status-Tested%20%26%20Working-brightgreen)
![R&D Duration](https://img.shields.io/badge/R%26D-1.5%20Months%20Testing-blue)
![Developer](https://img.shields.io/badge/Developer-Individual%20Project-orange)

An optimized, highly reliable, and low-cost hardware solution for water level sensing and automatic pump/relay control using the **NE555 Timer** in Monostable mode and a **2N2222 NPN Transistor**.

This design solves the infamous **"Continuous Trigger Lock" (Latch-up)** issue in standard 555 monostable circuits when water probes stay submerged continuously.

---

## 💡 The Engineering Challenge & Solution

### The Problem in Traditional 555 Circuits:
When water reaches the probes (`BASE_WAT`), it establishes a continuous conductive path. In standard 555 timer circuits, holding Pin 2 (Trigger) LOW continuously prevents the timer from completing its timing cycle or resetting, causing the output load (LED/BUZZER) to hang indefinitely.

### The Solution (Developed after 1.5 Months of Practical Prototyping):
Through **1.5 months of rigorous testing, component tuning, and field validation**, this standalone analog circuit was perfected:
1. **`BASE_WAT` Water Probes:** Detect water presence via conductivity to activate the Base of the 2N2222 NPN transistor.
2. **AC-Coupling Pulse Generator:** A $100nF$ ceramic capacitor converts the continuous DC conduction into a sharp, single negative pulse at Pin 2 of the NE555 by Driven the base of 2N222A .
3. **Automatic Discharge & Reset:** A $10k\Omega$ Collector pull-up resistor and a $10k\Omega$ Base pull-down resistor ensure full capacitor discharge and instant reset capability once water drops below the `BASE_WAT` level.

---

## ✨ Key Features

- ⏱️ **True Single-Pulse Triggering:** Timer completes its configured runtime (~2.5 to 3 minutes) and turns off smoothly, even if probes remain submerged in water.
- 💧 **High Water Sensitivity:** Reliable detection with tap water via `BASE_WAT` probes without false triggering.
- 🔄 **Instant Auto-Reset:** Ready for the next cycle immediately after water level drops below the probes.
- ⚡ **Pure Hardware Solution:** No microcontrollers, no programming, and zero software lag.

---
## ⚙️ NE555 Operational Modes Comparison

### 1. Monostable Mode (Used in this Main Project)
- **Function:** Generates a **single pulse** of duration $T$ upon receiving a LOW trigger signal at Pin 2.
- **Application:** Timing out the water pump (turning it ON for ~2.5–3 minutes then automatically switching OFF).
- **Time Formula:** $$T = 1.1 \times R_T \times C_T$$
  *(With $R_T =100\text{K}\Omega$ and $C_T = 100\mu\text{F}$,.

---

### 2. Astable Mode (Optional Extension for Alarm/Buzzer)
- **Function:** Generates a continuous **square wave oscillation** (no stable state) without requiring an external trigger.
- **Application:** Driving a piezo buzzer or flashing warning LED when water reaches the probes.
- **Frequency Formula:**
  $$f = \frac{1.44}{(R_A + 2R_B) \times C}$$
- **Duty Cycle Formula:**
  $$\text{Duty Cycle (\%)} = \frac{R_A + R_B}{R_A + 2R_B} \times 100$$

#### Astable Mode Bill of Materials (If adding a Water Alarm):
| Component | Typical Value | Description |
| :--- | :--- | :--- |
| **$R_A$ Resistor** | $1k\Omega - 10k\Omega$ | Charge resistor (VCC to Pin 7) |
| **$R_B$ Resistor** | $10k\Omega - 100k\Omega$ | Charge/Discharge resistor (Pin 7 to Pins 6 & 2) |
| **Capacitor ($C$)** | $10\mu\text{F} - 100\mu\text{F}$ | Sets oscillation frequency |
| **Output Device** | Piezo Buzzer / LED | Connected to Pin 3 for audible/visual alert |

---


## 🛠️ Bill of Materials (BOM)

| Component | Value / Model | Function / Description |
| :--- | :--- | :--- |
| **Timer IC** | NE555 | Monostable Multivibrator |
| **NPN Transistor** | 2N2222 (or 2N2222A) | Water Sensor Trigger Driver |
| **Coupling Capacitor** | 100nF (104 Ceramic) | Converts DC signal into Trigger Pulse |
| **Timing Capacitor ($C_T$)** | 100µF / 16V–25V | Timing Delay Capacitor |
| **Timing Resistor ($R_T$)** | 100KΩ | Sets timer delay (~2.5–3 Minutes) |
| **Pull-Up Resistors** | $2 \times 10k\Omega$ | 2N2222 Collector Pull-up & NE555 Pin 2 Pull-up |
| **Base Pull-Down** | 10kΩ | 2N2222 Base discharge resistor |
| **Control Capacitor** | 10nF (103 Ceramic) | Noise filtering on Pin 5 |
| **Water Probes** | `BASE_WAT` | VCC Probe(AC-Couple) & Transistor Base Probe |
| **Output Driver** | pin 8 (VCC)  | Astable Mode Timer IC_VCC|


---

## 🧪 Testing & Development Timeline

- **Weeks 1–4:** Tested standard BJT switches and direct RC triggering; suffered from false triggers, floating base noise, and latching issues.
- **Weeks 5–6 (Finalized Design):** Added the $100k\Omega$ Base pull-down for 2N2222 and $10k\Omega$ Collector pull-up with the $100nF$ AC coupling capacitor. Confirmed 100% success rate under actual water tank conditions with exact 2.5–3 minute pulse timing.

---

## 👤 Developer & Acknowledgments

- **Developed & Tested by:** Individual Project / Independent Maker
- **R&D Period:** 1.5 Months of practical hardware testing.
---

## 📐 Circuit Schematic Diagram
