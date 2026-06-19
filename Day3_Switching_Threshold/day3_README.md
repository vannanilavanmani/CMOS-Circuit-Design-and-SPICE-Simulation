# Day 3: CMOS Inverter Switching Threshold & Dynamic Transient Simulations

This directory contains the mathematical derivations and SPICE simulation netlists for characterizing a static CMOS inverter cell's switching midpoint ($V_m$) and dynamic propagation delays using the Google/SkyWater Sky130nm Process Design Kit (PDK).

## Table Of Contents
- [Switching Threshold ($V_m$) Mathematical Derivation](#switching-threshold-v_m-mathematical-derivation)
- [Dynamic Transient Analysis Theory](#dynamic-transient-analysis-theory)
- [Simulation File Inventory](#simulation-file-inventory)
- [How to Run and Plot Waveforms](#how-to-run-and-plot-waveforms)

---

## Switching Threshold ($V_m$) Mathematical Derivation

The switching threshold ($V_m$ or $V_{sp}$) is defined as the unique static equilibrium point where the input voltage equals the output voltage ($V_{in} = V_{out}$). Graphically, this marks the exact intersection of the VTC curve with the line $V_{out} = V_{in}$. 

At this specific operation point, both the NMOS pull-down and PMOS pull-up transistors are operating concurrently in the **Saturation Region** because:
- For NMOS: $V_{ds} = V_{out} = V_{m} > V_{gs} - V_{tn} = V_{m} - V_{tn}$
- For PMOS: $|V_{ds}| = V_{DD} - V_{out} = V_{DD} - V_{m} > |V_{gs}| - |V_{tp}| = V_{DD} - V_{m} - |V_{tp}|$

### Equating Saturated Drift Currents:
Ignoring channel length modulation ($\lambda = 0$), we equate the drain current magnitudes ($I_{dn} = |I_{dp}|$):

$$\frac{1}{2}\mu_n C_{ox} \left(\frac{W}{L}\right)_n (V_{in} - V_{tn})^2 = \frac{1}{2}\mu_p C_{ox} \left(\frac{W}{L}\right)_p (V_{DD} - V_{in} - |V_{tp}|)^2$$

Substituting $V_{in} = V_{m}$ and defining the geometric/mobility ratio parameter $r$:

$$r = \sqrt{\frac{\mu_p (W/L)_p}{\mu_n (W/L)_n}}$$

Solving for the switching midpoint $V_m$:

$$V_m - V_{tn} = r(V_{DD} - V_m - |V_{tp}|)$$

$$V_m(1 + r) = V_{tn} + r(V_{DD} - |V_{tp}|)$$

$$V_m = \frac{V_{tn} + r(V_{DD} - |V_{tp}|)}{1 + r}$$

### The Symmetric Inverter Condition
To optimize noise immunity margins equally, an ideal digital inverter should switch precisely at the half-supply mark ($V_m = V_{DD}/2$). Assuming matched device thresholds ($V_{tn} = |V_{tp}|$), this symmetrical constraint requires $r = 1$, yielding:

$$\mu_n \left(\frac{W}{L}\right)_n = \mu_p \left(\frac{W}{L}\right)_p \implies W_p = \left(\frac{\mu_n}{\mu_p}\right) W_n$$

Because electron mobility ($\mu_n$) is roughly $2$ to $3$ times faster than hole mobility ($\mu_p$) in silicon, the pull-up PMOS width must be scaled up systematically ($W_p \approx 2.5 \times W_n$) to balance switching performance.

---

## Dynamic Transient Analysis Theory

Static parameters do not fully capture digital operating speeds. Dynamic simulations inject a pulsed voltage waveform into the gate input node to extract time-domain delay and edge transition characteristics.

### 1. Cell Propagation Delays
Propagation metric points are measured exactly at the $50\%$ voltage threshold marks ($0.9\text{V}$ for a $1.8\text{V}$ rail):
- **$t_{pHL}$ (High-to-Low Propagation Delay):** Time difference between the $50\%$ rising edge of the input and the $50\%$ falling edge of the output. The output node discharges through the NMOS pulldown channel.
- **$t_{pLH}$ (Low-to-High Propagation Delay):** Time difference between the $50\%$ falling edge of the input and the $50\%$ rising edge of the output. The output node charges up through the PMOS pullup channel.

$$\text{Average Propagation Delay } (t_{pd}) = \frac{t_{pHL} + t_{pLH}}{2}$$

### 2. Output Slew/Transition Times
Slew rates determine the shape of signal paths and are measured across the $10\%$ to $90\%$ voltage boundaries ($0.18\text{V}$ to $1.62\text{V}$):
- **Rise Time ($t_r$):** The duration for the output signal to transition from $10\%$ up to $90\%$ of $V_{DD}$.
- **Fall Time ($t_f$):** The duration for the output signal to transition from $90\%$ down to $10\%$ of $V_{DD}$.

---

## Simulation File Inventory

This directory contains two specific testbenches built using Sky130 technology primitives to analyze static and dynamic characteristics:

### 1. `inv_vtc.spice`
Traces the continuous input/output static voltage states to verify the calculated $V_m$ value.

```spice
* Day 3: CMOS Inverter Static VTC Characterization
.include "sky130_fd_pr/models/corners/tt.spice"

* Component Declarations (Drain Gate Source Substrate)
Xn out in 0 0     sky130_fd_pr__nfet_0v18 W=1u L=0.15u
Xp out in vdd vdd sky130_fd_pr__pfet_0v18 W=2.5u L=0.15u

* Supplies
Vsource vdd 0 1.8
Vin in 0 0

* Static DC Sweep
.dc Vin 0 1.8 0.01

.control
run
plot v(out) vs v(in) title 'Static Inverter VTC Curve'
.endc
.end