# 🌟 RISC-V SoC Tapeout – Week 4: Day 1 (Basics of NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds))

> **Ngspice + Sky130** — Device‑level Theory & Practical Sessions.

---

### 📘 Objective

🔎 **Understand** NMOS physics and Id–Vds behaviour.  

🛠️ **Prepare** for Ngspice+Sky130 simulations.  

🧾 **Provide** formulas, derivations, plots, and practical notes for lab use.

---

## 1. ✅ Overview & Learning Outcomes

🎯 *Goal:* Explain how $\(I_D\)$ depends on $\(V_{DS}\)$ for different $\(V_{GS}\)$ and prepare for DC sweep simulations in Ngspice.

✔️ **Outcomes:**
  - 🧠 Understand inversion & threshold.  
  - ✍️ Derive the long‑channel Id–Vds formula.  
  - 📈 Identify linear vs saturation regions.  
  - 🧲 Quantify body effect and short‑channel deviations.

---

## 2. 🧩 Device Structure & Terminals
- 🧭 **NMOS:** n‑channel MOSFET on p‑substrate.  
- 🔌 **Terminals:** Gate (G), Drain (D), Source (S), Body (B).  
- 📏 **Geometry:** Width (W), Length (L), Oxide thickness (t_{ox}).  
- ⚠️ **Note:** body usually tied to ground in logic cells; body biasing used in analog/special designs.

---

## 3. ⚙️ Operating Regimes — Intuition & Conditions
- ❌ **Cutoff:** $\(V_{GS} < V_T\)$ — negligible conduction.  
- 🔁 **Linear / Resistive:** $\(V_{DS} < V_{GS} - V_T\)$ — channel uniform, device behaves like a resistor.  
- 🔴 **Pinch‑off / Saturation:** $\(V_{DS} \ge V_{GS} - V_T\)$ — channel pinches near drain; \(I_D\) saturates.

---

## 4. 🧲 Threshold Voltage (V_T) & Body Effect
- ✨ **Definition:** $\(V_T\)$ — gate voltage required for strong inversion (continuous n‑channel).

- 📘 **Body‑effect (correct form):**

$\[\boxed{V_T = V_{T0} + \gamma\left(\sqrt{2\phi_F + V_{SB}} - \sqrt{2\phi_F}\right)}\]$

  - 🔬 $\(V_{T0}\)$: zero‑bias threshold.  
  - ⚙️ $\(\gamma = \sqrt{\dfrac{2 q \varepsilon_{si} N_A}{C_{ox}}}\)$: body‑effect coefficient.  
  - 📌 $\(\phi_F\)$: Fermi potential (depends on doping).

- 🔎 **Implication:** increasing $\(V_{SB}\)$ → increases $\(V_T\)$ (device harder to turn on).

---

## 5. 📐 Induced Channel Charge & Local Potential
- 📍 Local potential along channel: $\(V(x)\)$, with $\(V(0)=0\)$ (source), $\(V(L)=V_{DS}\)$ (drain).  
- ⚖️ Local gate overdrive: $\(V_{GS} - V(x) - V_T\)$.  
- 💡 Local inversion charge per unit area:

$\[Q_i(x) = C_{ox}\bigl(V_{GS} - V(x) - V_T\bigr)\]$

  where $\(C_{ox} = \dfrac{\varepsilon_{ox}}{t_{ox}}\)$.

---

## 6. ✍️ Drift‑current → Integral Derivation
- 🧩 Start: current per width \(W\):

$\[I_D = W \int_0^L v(x)\, Q_i(x)\, dx\]$

- 🔁 Substitute $\(v(x) = \mu_n E(x) = \mu_n \dfrac{dV(x)}{dx}\) and \(Q_i(x)\)$ then change variables to voltage:

$\[I_D = W \mu_n C_{ox} \int_0^{V_{DS}} (V_{GS} - V - V_T)\, dV\]$

- 🔢 Integrate:

$\[I_D = W \mu_n C_{ox} \Big[(V_{GS}-V_T)V_{DS} - \tfrac{V_{DS}^2}{2}\Big] \frac{1}{L}\]$

- ⚙️ Define process transconductance $\(K_N = \mu_n C_{ox} \dfrac{W}{L}\)$ →

$\[\boxed{I_D = K_N \Big[(V_{GS}-V_T)V_{DS} - \tfrac{1}{2} V_{DS}^2\Big]}\]$

---

## 7. ⚡ Linear (Resistive) Region — Simplified
- ✅ If $\(V_{DS} \ll V_{GS} - V_T\)$:

$\[I_D \approx K_N (V_{GS} - V_T) V_{DS}\]$

- 🧠 Interpretation: device ≈ voltage‑controlled resistor; conductance ∝ $\(V_{GS}-V_T\)$.

---

## 8. 🔴 Pinch‑off & Saturation — Square‑law Result
- 🔎 Pinch‑off at $\(V_{DS} = V_{GS} - V_T\)$.  
- 📌 Ideal long‑channel saturation current:

$\[\boxed{I_{D(sat)} = \tfrac{1}{2} K_N (V_{GS} - V_T)^2}\]$

- ⚠️ Practical correction (channel‑length modulation):

$\[I_D \approx \tfrac{1}{2} K_N (V_{GS} - V_T)^2 (1 + \lambda V_{DS})\]$

---

## 9. 🔬 Short‑channel & Second‑order Effects (practical)
- 🚩 Velocity saturation — carriers saturate at $\(v_{sat}\)$, reducing square‑law scaling.  
- 📉 Mobility degradation $(\(\theta\))$ — vertical field reduces µ at high $\(V_{GS}\)$.  
- ⚡ DIBL — $\(V_T\)$ decreases at high $\(V_{DS}\)$ → higher leakage.  
- 🔌 Series resistances $\(R_S, R_D\)$ reduce effective biases.

> 💡 Use foundry SPICE models (Sky130) to capture these — theory is a first approximation.

---

## 10. 📉 Subthreshold Conduction & Slope
- 🧪 When $\(V_{GS} < V_T\)$: exponential conduction:

$\[I_D \propto e^{\dfrac{V_{GS}}{n V_T^{\mathrm{th}}}}\]$

- 📏 Subthreshold slope (SS):

$\[\mathrm{SS} = \dfrac{dV_{GS}}{d(\log_{10} I_D)}\]$ (mV/decade)

- 🔍 Ideal limit ≈ 60 mV/dec at 300 K; practical devices have larger SS.

---

## 11. 📐 Derived Quantities & Quick Formulas
- ⚙️ $\(K_N = \mu_n C_{ox} \dfrac{W}{L}\)$.  
- 📈 $\(g_m = \dfrac{dI_D}{dV_{GS}}$ = K_N $(V_{GS} - V_T)$ = $\sqrt{2 K_N I_D}\)$.  
- 📉 $\(g_{ds} = \dfrac{dI_D}{dV_{DS}}\)$ → approximate $\(\lambda \approx g_{ds}/I_D\)$.

---

## 12. 📊 Theoretical Plots
- 📈 **Id vs Vds** (family for multiple Vgs).  
- 🔀 **Id vs Vgs** (transfer) at low/high Vds.  
- 📐 **sqrt(Id) vs Vgs** (V_T extraction for long‑channel).  
- 📉 **log(Id) vs Vgs** (SS measurement).  
- ⚖️ **g_m vs I_D** and **g_m/I_D vs I_D** for sizing insights.

---

## 13. 🛠️ Practical SPICE Notes (theory → practice)
- 🧾 **Units:** always specify `W=5u`, `L=0.15u`, etc.  
- 🔎 **Node order:** MOS instances use `D G S B` — missing body node changes behaviour.  
- 📂 **Model inclusion:** use `.include` / `.lib` (Sky130) for accurate parameters.  
- 🧮 **Extraction:** export raw data and post‑process (Python/Matplotlib recommended).

---

## 14. 🧪 Day‑1 Exercises (lab)
1. 🧭 Plot **Id vs Vds** for Vgs = {0.2, 0.5, 0.8, 1.1, 1.4, 1.7} V — identify regions.  
2. 📐 Extract **V_T** via sqrt(Id) method (Id vs Vgs at Vds=50 mV).  
3. 📉 Compute **SS** from log(Id) vs Vgs.  
4. 🧲 Demonstrate body effect: step VSB and plot V_T vs VSB.

---

## 20. 🔭 Next Steps & References

▶️ **Day 2:** velocity saturation, mobility degradation, CMOS inverter VTC and timing extraction.
  
🧰 **Tools:** Ngspice, Python (NumPy/Matplotlib), Sky130 models & example netlists.

---

