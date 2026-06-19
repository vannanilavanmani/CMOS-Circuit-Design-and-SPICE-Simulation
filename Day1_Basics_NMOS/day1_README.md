# Day 1: Basics of NMOS Drain Current ($I_d$) vs. Drain-to-Source Voltage ($V_{ds}$)

This directory houses the foundational device characterization work and SPICE netlists verifying a 4-terminal primitive NMOS transistor using the open-source Google/SkyWater Sky130nm PDK.

## Table Of Contents
- [Introduction to Circuit Design and SPICE](#introduction-to-circuit-design-and-spice)
- [Strong Inversion and Threshold Voltage Chemistry](#strong-inversion-and-threshold-voltage-chemistry)
- [Drain Current Models (Linear vs. Saturation)](#drain-current-models-linear-vs-saturation)
- [Simulation File Inventory](#simulation-file-inventory)
- [How to Run and Plot](#how-to-run-and-plot)

---

## Introduction to Circuit Design and SPICE
Circuit simulations provide critical behavioral models where analytical calculations fail due to modern sub-micron physical constraints. In physical digital design flows, automated cell characterization engines execute thousands of SPICE simulations to generate lookup charts (Liberty format, `.lib`). These standard library databases map precise cell propagation delays and output signal transition slews as a function of changing input slews and output capacitive pin loads.

---

## Strong Inversion and Threshold Voltage Chemistry

The state of the NMOS device transitions across distinct physical phases depending on the potential applied to the gate:

- **$V_{gs} = 0\text{V}$**: The physical interface establishes two back-to-back $n^+ - p - n^+$ diodes. The structure offers an exceptionally high resistance profile; no conducting carrier inversion layer can form.
- **$V_{gs} > 0\text{V}$**: Positive potential applied to the poly-silicon gate repels majority hole carriers deep into the P-substrate. A depletion region consisting of fixed negative acceptor ions is left behind at the oxide interface.
- **Strong Inversion ($V_{gs} \ge V_t$)**: As the gate bias increases, the surface potential drops below twice the bulk Fermi potential ($2\phi_F$), dropping the local energy bands down. This attracts minority electron carriers directly beneath the gate oxide, fundamentally inverting the local channel surface to $n$-type material.
- **The Body Effect**: If a reverse body bias is applied to the substrate layer ($V_{sb} > 0\text{V}$), the depletion width expands, trapping additional fixed charges. Consequently, a larger gate potential is required to overcome this depletion field and achieve strong inversion, altering the threshold voltage ($V_t$) via:
  $$V_t = V_{t0} + \gamma \left( \sqrt{|2\phi_F| + V_{sb}} - \sqrt{|2\phi_F|} \right)$$

---

## Drain Current Models (Linear vs. Saturation)

Once the inversion channel is formed, applying a lateral drain-to-source bias ($V_{ds}$) governs electron drift vectors through two key operating zones:

### 1. Linear/Resistive Region ($V_{ds} < V_{gs} - V_t$)
At low drain potentials, a continuous charge channel connects the source to the drain. The inversion channel behaves functionally as a voltage-controlled continuous resistor. The current climbs quadratically with increasing $V_{ds}$ before beginning to taper:
$$I_d = \mu_n C_{ox} \frac{W}{L} \left[ (V_{gs} - V_t)V_{ds} - \frac{V_{ds}^2}{2} \right]$$

### 2. Saturation Region ($V_{ds} \ge V_{gs} - V_t$)
When $V_{ds}$ reaches the overdrive limit ($V_{gs} - V_t$), the local voltage drop across the oxide near the drain boundary falls below the threshold voltage required to sustain inversion. The channel drops to a depth of zero—a phenomenon known as the **pinch-off point**. Further increases in $V_{ds}$ do not increase channel drift acceleration; current instead stabilizes to a constant saturation value, modulated minorly by Channel Length Modulation ($\lambda$):
$$I_d = \frac{1}{2}\mu_n C_{ox} \frac{W}{L} (V_{gs} - V_t)^2 (1 + \lambda V_{ds})$$

---

## Simulation File Inventory

The standard node parsing topology for a 4-terminal MOSFET device requires strict positional mapping across **Drain, Gate, Source, and Substrate (D-G-S-B)** terminals. This directory contains two testbench setups mapping this hardware structure:

### 1. `nmos_id_vds.spice`
This deck sweeps the lateral drain voltage across multiple distinct gate-bias steps to map the device's output characteristic curves.

```spice
* Day 1: NMOS Id vs Vds Output Characteristics Sweep
.param VDD=1.8
.include "sky130_fd_pr/models/corners/tt.spice"

* Device Declaration: Xname Drain Gate Source Substrate model_name parameters
X1 d g 0 0 sky130_fd_pr__nfet_0v18 W=1u L=0.15u

* Independent DC Sources
Vds d 0 0.0
Vgs g 0 0.0

* DC Sweep Setup: Sweep Vds from 0 to 1.8V (10mV increments), step Vgs from 0 to 1.8V (200mV increments)
.dc Vds 0 1.8 0.01 Vgs 0 1.8 0.2

.control
run
plot -i(Vds) vs v-sweep title 'NMOS Output Characteristics (Id vs Vds)'
.endc
.end