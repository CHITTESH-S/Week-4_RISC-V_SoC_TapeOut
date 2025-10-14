# 🌟 RISC-V SoC Tapeout – Week-4: CMOS Circuit Design (Using Sky130-style) 

> **SPICE-based CMOS** circuit design and simulation using the **Sky130 PDK** — exploring device behavior, inverter characteristics, timing, and variation analysis.

---

## 📘 Quick Project Snapshot

* 🚀 **Title:** Week 4 — CMOS Circuit Design using Sky130 PDK
* 🎯 **Goal:** Characterize NMOS/PMOS devices, build/analyze a CMOS inverter, and study timing, noise margins, and variation with Ngspice.
* 🧪 **Tools:** Ngspice, Sky130 device models, text editor, plotting tool (e.g., gnuplot, matplotlib).
* 🗂️ **Repo layout:** See **Project structure** below.

---

## 🗂️ Project structure (suggested)

```
Week4_CMOS_Circuit_Design_sky130/
├─ Day1_NMOS_Id_vs_Vds/
│  ├─ netlist.cir
│  ├─ run.sh
│  ├─ results/
│  └─ README.md
├─ Day2_CMOS_VTC/
│  └─ README.md
├─ Day3_CMOS_Switching_Dynamics/
│  └─ README.md
├─ Day4_Noise_Margin_Robustness/
│  └─ README.md
├─ Day5_Power_Supply_Variation/
│  └─ README.md
├─ .gitignore
├─ LICENSE
└─ README.md
```
---

## ✅ What to include in each day folder

* 📄 `netlist.cir` — Ngspice netlist for the experiment (use `.param` variables).
* ▶️ `run.sh` — single-line runner (e.g., `ngspice -b netlist.cir > results/log.txt`).
* 📊 `results/` — png plots, csv exported data.
* ✍️ `README.md` — short analysis + extracted numeric values (Vth, Vm, delays, noise margins).

---

## 🧭 Day-by-day Mini-lab guide

### Day 1 — NMOS Id vs Vds
* 🎯 **Objective:** Sweep Vds for multiple Vgs to observe linear and saturation regions and channel-length modulation.
* 🛠️ **Files:** `netlist_Id_Vds.cir`, `run.sh`.
* 🧾 **Expected outputs:** Id–Vds plots (linear & log), CSV of I(D) vs V(D).
* 📌 **Analysis:** Identify knee, estimate output resistance in saturation.

### Day 2 — Vth & CMOS Inverter VTC
* 🎯 **Objective:** Extract Vth (Id–Vgs methods) and plot Vout vs Vin for a CMOS inverter to find Vm (switching point).
* 🛠️ **Files:** `netlist_vtc.cir`, `run.sh`.
* 📌 **Analysis:** Locate Vm where Vin=Vout; explain relation to transistor sizing.

### Day 3 — Transient Switching Dynamics
* 🎯 **Objective:** Apply pulse input and measure tPLH / tPHL and rise/fall times (use `.measure`).
* 🛠️ **Files:** `netlist_tran.cir`, `run.sh`.
* 📌 **Analysis:** Relate delays to device sizes and load capacitance.

### Day 4 — Noise Margin & Robustness
* 🎯 **Objective:** From VTC compute VOL, VOH, VIL, VIH and then NML/NMH.
* 🛠️ **Files:** `netlist_vtc.cir` (reuse), annotated VTC plots.
* 📌 **Analysis:** Discuss effect of Vm shifts on noise margins.

### Day 5 — VDD & Device Variation Analysis
* 🎯 **Objective:** Sweep VDD and W/L ratios; capture shifts in Vm, delays, and noise margins.
* 🛠️ **Files:** `netlist_variation.cir`, `run.sh`.
* 📌 **Analysis:** Tabulate results and identify sensitivity.

---



