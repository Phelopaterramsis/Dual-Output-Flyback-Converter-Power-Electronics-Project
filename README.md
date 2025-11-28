# 🔌 Dual-Output Flyback Converter – Power Electronics Project

This folder contains our ECEN 436 Power Electronics final project at the University of Nebraska–Lincoln, where we designed, built, and tested a closed-loop flyback converter with a custom dual-output transformer.

## 📌 Course

- Course: ECEN 436 – Power Electronics  
- University: University of Nebraska–Lincoln (UNL)  
- Instructor: Dr. Jun Wang  
- Semester: Fall 2023  

## 👥 Team

- Youssef Abo Taleb  
- Phelopater Ramsis  
- Mohamed Essam  

---

## 🧾 Project Overview

The goal of this semester-long project was to:

- Design and build a **flyback converter** with **dual isolated outputs** (+15 V and −15 V).  
- Operate from an **18–30 V DC input range**.  
- Meet a **minimum power conversion efficiency of 85%**.  
- Design, wind, and validate the **custom flyback transformer** (coupled inductor) that satisfies the electrical and magnetic requirements.

We were provided with:

- A pre-designed PCB  
- Full circuit schematics  
- All active and passive components  

Our main design freedom and challenge was the **transformer design**, winding strategy, and practical implementation.

---

## ⚙️ Converter Design Summary

- Topology: Isolated flyback converter (dual output)  
- Input voltage: 18–30 V DC  
- Outputs: +15 V and −15 V  
- Control IC: Current-mode PWM controller with fixed 100 kHz switching frequency  
- Features:  
  - Soft-start to reduce inrush current  
  - Current-mode control for better line/load regulation  
  - Cycle-by-cycle current limiting for protection  

The primary-side circuitry is similar to a standard single-output flyback; the additional complexity comes from the **two secondary windings** and the transformer design.

---

## 🧮 Key Design Steps

### 1️⃣ Electrical Design

- Determined duty cycles, turns ratio, and operating mode (CCM).  
- Chosen transformer turns ratio `n = Ns / Np ≈ 0.5` with final turns:  
  - Primary: Np = 8  
  - Secondary 1: Ns1 = 4  
  - Secondary 2: Ns2 = 4  
- Designed the magnetizing inductance and checked that the converter stays within the desired mode and current ripple limits.  

### 2️⃣ Transformer Magnetic Design

- Targeted a specific range for LK / LM (leakage to magnetizing inductance ratio).  
- Calculated magnetizing inductance, peak currents, and maximum flux density to stay below core saturation.  
- Chose an air-gap length and core size that keep:  
  - LM at the desired value  
  - Bmax safely below Bsat  
- Selected wire gauges for primary and secondaries based on RMS current and window area:  
  - Primary: 18 AWG  
  - Secondary: 20 AWG  

### 3️⃣ PLECS Simulation

- Built a full flyback converter model in PLECS.  
- Verified:  
  - Start-up behavior  
  - Regulation of the outputs  
  - Current waveforms in primary and secondaries  
  - Stress on semiconductor devices  

This step helped validate the design before hardware implementation.

---

## 🧵 Transformer Construction

### 4️⃣ Wire and Winding Choices

- Started experimenting with **Litz wire** to lower high-frequency losses (skin and proximity effects).  
- Evaluated:  
  - Frequency of operation (100 kHz)  
  - Strand size and count  
  - Insulation requirements  
  - Current capability vs. physical size  

We also studied several **winding techniques** (layer, sectional, bifilar, toroidal, separate vs. stacked outputs, etc.) to manage:

- Leakage inductance  
- Coupling between windings  
- Voltage distribution and insulation  
- Heat dissipation  

### 5️⃣ Practical Winding and Trials

We went through several physical trials:

- **Attempt 1**  
  - Achieved LK / LM ≈ 3.52% (close to target),  
  - But the winding order was wrong (secondary-secondary-primary), so it was rejected.

- **Attempt 2**  
  - LK / LM ≈ 3.6%,  
  - Transformer burned when connected to PCB, likely due to an internal short.

- **Attempt 3 (Final)**  
  - Final turns: Np = 8, Ns1 = 4, Ns2 = 4  
  - Measured LM ≈ 12.69 µH and LK ≈ 0.28 µH  
  - LK / LM ≈ 2.2% – our best result and within design expectations.  

The final transformer was built with Litz wire, using proper insulation layers between primary and secondaries and an 8:4:4 turns distribution.

---

## 🔧 PCB Assembly and Fabrication

- Soldered all SMD and through-hole components: resistors, diodes, capacitors, MOSFET, controller IC, terminals, and connectors.  
- Used 63/37 or 67/37 solder with flux to ensure low-resistance joints.  
- Performed continuity checks with a multimeter after soldering.  
- Visually inspected all joints (and re-touched cold joints) before installing the transformer.  

---

## 📊 Final Testing and Results

### 6️⃣ Qualification Tests

- Tested the converter at input voltages of **18 V, 24 V, and 30 V DC**.  
- Measured output voltages and currents on both +15 V and −15 V rails.  
- Observed switching waveforms using an oscilloscope to verify correct operation and duty cycle behavior.  

### 7️⃣ Efficiency

Power conversion efficiency was computed using:

- Pin = Vin × Iin  
- Pout = V1 × I1 + V2 × I2  
- Efficiency η = (Pout / Pin) × 100%  

Measured overall efficiencies:

- ≈ 85.3% at 18 V input  
- ≈ 85.5% at 24 V input  
- ≈ 85.6% at 30 V input  

These results meet the course target of **at least 85% efficiency**.

---

## 💡 Lessons Learned

From this project we gained:

- Hands-on experience designing and building an isolated flyback converter.  
- Practical understanding of how transformer design (turns, air gap, winding style) affects leakage inductance, magnetizing inductance, and efficiency.  
- Skills in using PLECS and lab instrumentation (oscilloscope, LCR meter, multimeter).  
- Experience with PCB soldering, debugging shorts, and verifying safe operation.  
- Appreciation for the trade-off between ideal design equations and real-world manufacturing constraints.  

---

## 🗂️ Files in This Folder

- `Power Electronics.pdf` – full project report with detailed calculations, photos, and plots.  
- `README.md` – this summary file.  
