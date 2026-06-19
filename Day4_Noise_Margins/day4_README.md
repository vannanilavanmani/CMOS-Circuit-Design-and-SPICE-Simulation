# Day 4: CMOS Inverter Noise Margin Robustness Evaluation

This directory contains the theoretical formulations, analytical equations, and SPICE simulation netlists required to evaluate the noise immunity and structural robustness of a CMOS inverter using the Google/SkyWater Sky130nm PDK.

## Table Of Contents
- [Noise Margin Critical Parameters](#noise-margin-critical-parameters)
- [Mathematical Derivation & Unity Gain Criteria](#mathematical-derivation--unity-gain-criteria)
- [Asymmetric PMOS Sizing & VTC Shifting](#asymmetric-pmos-sizing--vtc-shifting)
- [Simulation File Inventory](#simulation-file-inventory)
- [How to Run and Extract Metrics](#how-to-run-and-extract-metrics)

---

## Noise Margin Critical Parameters

Noise Margin ($NM$) is a fundamental metric that quantifies a digital circuit's electrical immunity to spurious signal fluctuations or crosstalk on its input lines. It defines the maximum allowable noise voltage that can be superimposed on a digital signal without corrupting the logic state of the receiving cell.

An electrical characterization of a CMOS inverter VTC isolates four critical voltage metrics:

- **$V_{OL}$ (Outputs Logic Low):** The nominal voltage produced at the output when the cell processes a valid logic high ($V_{out} = 0\text{V}$).
- **$V_{OH}$ (Outputs Logic High):** The nominal voltage produced at the output when the cell processes a valid logic low ($V_{out} = V_{DD} = 1.8\text{V}$).
- **$V_{IL}$ (Input Input Low Threshold):** The maximum input voltage that the cell safely interprets as a logic low.
- **$V_{IH}$ (Input Input High Threshold):** The minimum input voltage that the cell safely interprets as a logic high.

### Noise Margin Formulae:
The total logic noise margin is subdivided into two distinct protective bands:

$$\text{Noise Margin Low } (NM_L) = V_{IL} - V_{OL}$$
$$\text{Noise Margin High } (NM_H) = V_{OH} - V_{IH}$$

---

## Mathematical Derivation & Unity Gain Criteria

The transition limits $V_{IL}$ and $V_{IH}$ cannot be determined through simple voltage levels alone. They are explicitly defined as the operational markers where the slope of the Voltage Transfer Characteristics curve equals negative unity:

$$\frac{dV_{out}}{dV_{in}} = -1$$

Beyond these unity-gain inflection points, the absolute value of the voltage gain ($A_v = |\frac{dV_{out}}{dV_{in}}|$) exceeds $1$, creating an unstable, regenerative amplifier state that aggressively drives the output to a clean binary rail.

### Slope Analysis:
- **When $\mathbf{V_{in} < V_{IL}}$:** The signal gain magnitude is less than $1$. Noise perturbations on the input line are electrically attenuated and suppressed by the circuit.
- **When $\mathbf{V_{IL} < V_{in} < V_{IH}}$:** The signal gain magnitude is much greater than $1$. The circuit is highly sensitive, transitioning rapidly through its high-gain state.
- **When $\mathbf{V_{in} > V_{IH}}$:** The signal gain magnitude drops below $1$ again, restoring high-margin logic levels at the output terminal.

---

## Asymmetric PMOS Sizing & VTC Shifting

To maintain balanced performance metrics, standard cells use a symmetric design ratio ($\beta_n = \beta_p$), centering the switching midpoint at $V_{m} \approx V_{DD}/2$. If the aspect ratios deviate, the noise profiles alter predictably:

### 1. Oversized PMOS Configuration ($W_p \gg 2.5 \times W_n$)
- **VTC Shift:** The entire transfer curve shifts toward the right (approaching the $V_{DD}$ rail).
- **Physical Reason:** The pull-up device exhibits significantly less channel resistance, keeping the output clamped high longer as $V_{in}$ begins to rise.
- **Noise Margin Impact:** $NM_L$ expands because $V_{IL}$ shifts higher, while $NM_H$ decreases because $V_{IH}$ moves rightward.

### 2. Undersized PMOS Configuration ($W_p \approx W_n$)
- **VTC Shift:** The curve shifts toward the left (approaching the $0\text{V}$ ground rail).
- **Physical Reason:** The stronger pull-down NMOS discharges the output capacitance much earlier in the input voltage sweep.
- **Noise Margin Impact:** $NM_H$ expands at the expense of a severely degraded $NM_L$.

---

## Simulation File Inventory

This directory contains two specific simulation netlists designed to extract slope derivatives and evaluate geometric sizing limits:

### 1. Baseline Noise Margin Calculation Deck (`noise_margin.spice`)
This netlist runs a fine-step static sweep and uses the Ngspice mathematical derivative engine (`deriv`) to pinpoint the precise locations where the slope crosses `-1`.

```spice
* Day 4: Automated Static Noise Margin Extraction
.include "sky130_fd_pr/models/corners/tt.spice"

* Balanced CMOS Inverter Instance
Xn out in 0 0     sky130_fd_pr__nfet_0v18 W=1u L=0.15u
Xp out in vdd vdd sky130_fd_pr__pfet_0v18 W=2.5u L=0.15u

Vsource vdd 0 1.8
Vin in 0 0

* High-resolution DC sweep to enable accurate numerical differentiation
.dc Vin 0 1.8 0.001

.control
run
* Calculate the first derivative of output voltage with respect to input sweep
deriv v(out) vtc_slope

* Plot the VTC alongside the slope derivative to extract Vil and Vih points
plot v(out) vtc_slope vs v(in) ylimit -2 2 title 'VTC & Gain Slope Derivative (dVout/dVin)'
.endc
.end