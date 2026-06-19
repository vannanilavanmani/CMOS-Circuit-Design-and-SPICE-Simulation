# Day 5: Power Supply Scaling Sensitivity & Device Variation Monte Carlo Analysis

This directory contains the advanced reliability characterization, multi-rail voltage scaling testbenches, and statistical Monte Carlo simulation decks used to evaluate manufacturing process tolerances using the Google/SkyWater Sky130nm PDK.

## Table Of Contents
- [Supply Voltage ($V_{DD}$) Scaling & Low-Power Thresholds](#supply-voltage-v_dd-scaling--low-power-thresholds)
- [Foundry Process Variations & Transistor Mismatch](#foundry-process-variations--transistor-mismatch)
- [Simulation File Inventory](#simulation-file-inventory)
- [How to Run and Analyze Statistical Lots](#how-to-run-and-analyze-statistical-lots)

---

## Supply Voltage ($V_{DD}$) Scaling & Low-Power Thresholds

As modern integrated circuits scale down to save dynamic power ($P_{dyn} = C_{load} V_{DD}^2 f_{clk}$), reducing the supply voltage rail ($V_{DD}$) is the most effective strategy. However, lowering the supply voltage significantly degrades cell performance as the rail approaches the device threshold voltage ($V_t$):

### 1. Nominal vs. Near-Threshold Scaling Regimes:
- **Nominal Rail ($V_{DD} = 1.8\text{V}$):** Transistors operate with maximum overdrive voltage ($V_{gs} - V_t$), providing clean, sharp VTC transitions and rapid capacitive charging rates.
- **Low-Power Rail ($V_{DD} = 1.2\text{V}$):** Transition delays increase moderately, and the maximum noise margins shrink proportionally as the overall logical swing narrows.
- **Near-Threshold Rail ($V_{DD} = 0.8\text{V}$):** The supply sits near the primitive threshold voltage limit ($V_t \approx 0.76\text{V}$). The cell experiences severe propagation delays because drift currents collapse toward sub-threshold exponential regimes, heavily reducing cell robustness.

---

## Foundry Process Variations & Transistor Mismatch

During physical semiconductor fabrication, atomic-scale imperfections distort designed target geometries. No two transistors on a wafer are completely identical. These structural variations are mathematically categorized into two fundamental domains:



### 1. Global (Inter-Die / Lot-to-Lot) Variations
These capture macroscopic shifts across an entire wafer or manufacturing lot. Factors include physical gradients across the lithography tool, furnace temperature drifts, or variations in chemical mechanical polishing (CMP). This alters universal parameters such as base oxide thickness ($T_{ox}$) or uniform threshold voltage offsets across the whole die.

### 2. Local (Intra-Die / Spatial Mismatch) Variations
These represent random micro-disparities between adjacent, co-located transistors on the exact same silicon die. The primary drivers are:
- **Random Dopant Fluctuation (RDF):** Statistical variations in the exact number and spatial arrangement of implanted dopant atoms within the localized channel depletion zone. This causes a localized distribution drift in threshold voltages ($V_t$).
- **Line Edge Roughness (LER):** Atomic deviations along the edges of the patterned poly-silicon gate, which introduces variations into the effective channel length ($L_{eff}$).

### The Monte Carlo Solution:
To prevent timing failures in production, engineers run **Monte Carlo Simulations**. The simulator runs hundreds of loop iterations, randomly varying device parameters across a statistical Gaussian distribution curve based on foundry lot data. This ensures the design meets target noise margins across all process corners.

---

## Simulation File Inventory

This directory includes the final reliability decks analyzing voltage rail compromises and statistical geometric tolerances:

### 1. Multi-Rail Power Supply Scaling Deck (`supply_var.spice`)
This netlist maps the input sweep across three nested supply configurations ($1.8\text{V} \rightarrow 1.3\text{V} \rightarrow 0.8\text{V}$) to visualize VTC degradation under extreme low-power configurations.

```spice
* Day 5: Multi-Rail Power Supply Scaling Verification
.include "sky130_fd_pr/models/corners/tt.spice"

* Symmetrical Inverter Topology
Xn out in 0 0     sky130_fd_pr__nfet_0v18 W=1u L=0.15u
Xp out in vdd vdd sky130_fd_pr__pfet_0v18 W=2.5u L=0.15u

Vin in 0 0
Vsource vdd 0 1.8

* Sweep input voltage continuously while stepping the Vsource power rail down
.dc Vin 0 1.8 0.01 Vsource 0.8 1.8 0.5

.control
run
plot v(out) vs v(in) title 'VTC Performance Under VDD Supply Scaling (1.8V to 0.8V)'
.endc
.end