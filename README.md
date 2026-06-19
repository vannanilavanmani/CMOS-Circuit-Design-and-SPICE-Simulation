# CMOS Circuit Design and SPICE Simulation using Sky130nm Technology

## Table of Contents
- [Day 1 – NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)](#day-1--nmos-drain-current-id-vs-drain-to-source-voltage-vds)
  - [Circuit Design and SPICE Simulation Fundamentals](#circuit-design-and-spice-simulation-fundamentals)
    - [L1 – Need for SPICE Simulations](#l1--need-for-spice-simulations)
    - [L2 – NMOS: The Core Element in Circuit Design](#l2--nmos-the-core-element-in-circuit-design)
    - [L3 – Strong Inversion and Threshold Voltage](#l3--strong-inversion-and-threshold-voltage)
    - [L4 – Effect of Positive Substrate Bias on Threshold Voltage](#l4--effect-of-positive-substrate-bias-on-threshold-voltage)
  - [NMOS Operating Regions: Resistive and Saturation](#nmos-operating-regions-resistive-and-saturation)
    - [L1 – Resistive Region at Low Drain-Source Voltage](#l1--resistive-region-at-low-drain-source-voltage)
    - [L2 – Understanding Drift Current](#l2--understanding-drift-current)
    - [L3 – Drain Current Model in Linear Region](#l3--drain-current-model-in-linear-region)
    - [L4 – SPICE Analysis of Resistive Operation](#l4--spice-analysis-of-resistive-operation)
    - [L5 – Pinch-Off Condition](#l5--pinch-off-condition)
    - [L6 – Drain Current Model in Saturation Region](#l6--drain-current-model-in-saturation-region)
  - [Getting Started with SPICE](#getting-started-with-spice)
    - [L1 – SPICE Environment Overview](#l1--spice-environment-overview)
    - [L2 – Writing Circuits in SPICE Syntax](#l2--writing-circuits-in-spice-syntax)
    - [L3 – Technology Parameters in SPICE](#l3--technology-parameters-in-spice)
    - [L4 – Running Your First SPICE Simulation](#l4--running-your-first-spice-simulation)
    - [L5 – SPICE Lab with Sky130 Models](#l5--spice-lab-with-sky130-models)
- [Day 2 – Velocity Saturation and CMOS Inverter VTC Basics](#day-2--velocity-saturation-and-cmos-inverter-vtc-basics)
  - [Short-Channel Effects and Velocity Saturation](#short-channel-effects-and-velocity-saturation)
    - [L1 – SPICE Simulations at Lower Technology Nodes](#l1--spice-simulations-at-lower-technology-nodes)
    - [L2 – Id vs Vgs for Long and Short Channel Devices](#l2--id-vs-vgs-for-long-and-short-channel-devices)
    - [L3 – Velocity Saturation at Different Electric Fields](#l3--velocity-saturation-at-different-electric-fields)
    - [L4 – Velocity Saturation Drain Current Model](#l4--velocity-saturation-drain-current-model)
    - [L5 – Sky130 Lab: Id-Vgs Characteristics](#l5--sky130-lab-id-vgs-characteristics)
    - [L6 – Sky130 Lab: Threshold Voltage Extraction](#l6--sky130-lab-threshold-voltage-extraction)
  - [CMOS Voltage Transfer Characteristics (VTC)](#cmos-voltage-transfer-characteristics-vtc)
    - [L1 – MOSFET Viewed as a Switch](#l1--mosfet-viewed-as-a-switch)
    - [L2 – Standard MOS Voltage and Current Parameters](#l2--standard-mos-voltage-and-current-parameters)
    - [L3 – PMOS and NMOS Id vs Vds Characteristics](#l3--pmos-and-nmos-id-vs-vds-characteristics)
    - [L4 – Step 1: Mapping PMOS Gate-Source Voltage to Vin](#l4--step-1-mapping-pmos-gate-source-voltage-to-vin)
    - [L5 – Steps 2 & 3: Converting Drain-Source Voltages to Vout](#l5--steps-2--3-converting-drain-source-voltages-to-vout)
    - [L6 – Step 4: Overlaying Load Curves to Obtain VTC](#l6--step-4-overlaying-load-curves-to-obtain-vtc)
- [Day 3 – CMOS Switching Threshold and Dynamic Simulations](#day-3--cmos-switching-threshold-and-dynamic-simulations)
  - [VTC via SPICE Simulation](#vtc-via-spice-simulation)
    - [L1 – Building the SPICE Deck for a CMOS Inverter](#l1--building-the-spice-deck-for-a-cmos-inverter)
    - [L2 – Running the CMOS Inverter SPICE Simulation](#l2--running-the-cmos-inverter-spice-simulation)
    - [L3 – Sky130 CMOS VTC Lab](#l3--sky130-cmos-vtc-lab)
  - [Switching Threshold and CMOS Robustness](#switching-threshold-and-cmos-robustness)
    - [L1 – Switching Threshold Vm Explained](#l1--switching-threshold-vm-explained)
    - [L2 – Vm as a Function of (W/L)n and (W/L)p](#l2--vm-as-a-function-of-wln-and-wlp)
    - [L3 – (W/L) Ratios as a Function of Vm](#l3--wl-ratios-as-a-function-of-vm)
    - [L4 – Static and Dynamic Simulation Results](#l4--static-and-dynamic-simulation-results)
    - [L5 – Impact of Increased PMOS Width](#l5--impact-of-increased-pmos-width)
    - [L6 – CMOS Inverter in Clock Trees and STA](#l6--cmos-inverter-in-clock-trees-and-sta)
- [Day 4 – CMOS Noise Margin Robustness](#day-4--cmos-noise-margin-robustness)
  - [Evaluating CMOS Inverter Robustness: Noise Margin](#evaluating-cmos-inverter-robustness-noise-margin)
    - [L1 – What is Noise Margin?](#l1--what-is-noise-margin)
    - [L2 – Noise Margin Voltage Parameters](#l2--noise-margin-voltage-parameters)
    - [L3 – Noise Margin Equations and Summary](#l3--noise-margin-equations-and-summary)
    - [L4 – Noise Margin vs PMOS Width](#l4--noise-margin-vs-pmos-width)
    - [L5 – Sky130 Noise Margin Lab](#l5--sky130-noise-margin-lab)
- [Day 5 – Power Supply and Device Variation Robustness](#day-5--power-supply-and-device-variation-robustness)
  - [Robustness to Power Supply Variation](#robustness-to-power-supply-variation)
    - [L1 – SPICE Simulations for Power Supply Scaling](#l1--spice-simulations-for-power-supply-scaling)
    - [L2 – Trade-offs of Low Supply Voltage](#l2--trade-offs-of-low-supply-voltage)
    - [L3 – Sky130 Supply Variation Lab](#l3--sky130-supply-variation-lab)
  - [Robustness to Device Variation](#robustness-to-device-variation)
    - [L1 – Variation Source: Etching Process](#l1--variation-source-etching-process)
    - [L2 – Variation Source: Gate Oxide Thickness](#l2--variation-source-gate-oxide-thickness)
    - [L3 – SPICE Simulation Under Device Variations](#l3--spice-simulation-under-device-variations)
    - [L4 – Summary and Conclusions](#l4--summary-and-conclusions)
    - [L5 – Sky130 Device Variation Lab](#l5--sky130-device-variation-lab)

---

# Day 1 – NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)

## Circuit Design and SPICE Simulation Fundamentals

### L1 – Need for SPICE Simulations
Circuit design involves connecting PMOS and NMOS transistors to implement logic functions like NAND, NOR, OR, and AND gates.

<img width="542" height="526" alt="image" src="https://github.com/user-attachments/assets/bf9b9eed-3cf4-41be-bcfe-8b3ea7eadcb0" />

The inverter shown above has specific electrical characteristics. SPICE simulations help us determine delay and derive the appropriate W/L ratio for each transistor.

<img width="965" height="695" alt="image" src="https://github.com/user-attachments/assets/e2264a62-e4b1-4506-bb0f-eded09d303f3" />

**Why SPICE?**  
Clock Tree Synthesis, signal integrity (crosstalk), and timing analysis all rely on delay information that originates from SPICE simulations. Without accurate delay data, physical design concepts like timing closure and crosstalk analysis become meaningless.

Consider a Clock Tree Synthesis scenario with buffers driving different capacitive loads:

<img width="1206" height="392" alt="image" src="https://github.com/user-attachments/assets/a0dbe0ed-6981-4966-8d1d-7bf4d223ef61" />

SPICE produces a **Delay Table** where rows represent input slew rates and columns represent output loads. The cell at each intersection gives the propagation delay. Both Level 1 and Level 2 buffer delay tables are computed this way.

<img width="1410" height="668" alt="image" src="https://github.com/user-attachments/assets/422a8a28-f4e6-469a-97d4-535f02762e3d" />

These delay tables are the direct product of SPICE-based circuit characterization of CMOS logic cells.

### L2 – NMOS: The Core Element in Circuit Design
An NMOS transistor is built on a P-type substrate with heavily doped n+ regions forming the source and drain. An isolation region separates it from neighboring devices. Over the channel sits a thin oxide layer, topped by a metal gate terminal.

<img width="1195" height="507" alt="image" src="https://github.com/user-attachments/assets/fafb4e04-8d70-42dd-bae3-7570c38be028" />

**Threshold Voltage**  
Threshold voltage is fundamental to all transistor characterization. With Vgs = 0 (source, drain, and body all grounded), the p-substrate and n+ regions form reverse-biased PN junctions — no channel exists and resistance is very high.

<img width="1322" height="528" alt="image" src="https://github.com/user-attachments/assets/8e2fee4c-8616-4886-859c-d6c08d166541" />

Applying a positive Vgs charges the gate, attracting negative charges toward the substrate surface beneath the oxide.

<img width="1345" height="555" alt="image" src="https://github.com/user-attachments/assets/ef79f61f-5540-4ffb-aec8-06fa9354759a" />

### L3 – Strong Inversion and Threshold Voltage
As negative charges accumulate, a depletion region forms by repelling the majority holes in the p-substrate.

<img width="831" height="402" alt="image" src="https://github.com/user-attachments/assets/335a3525-699e-4c66-8161-2201df2b9070" />

Increasing Vgs further widens the depletion region. At a critical gate voltage, the surface inverts to behave like n-type material — this is called **Strong Inversion**, and the corresponding Vgs value is defined as the **Threshold Voltage (Vt)**.

<img width="1332" height="551" alt="image" src="https://github.com/user-attachments/assets/03776359-fd17-4e04-9fd5-9212422217df" />

Beyond Vt, electrons from the n+ source and drain fill the inverted surface, forming a conducting channel.

<img width="1358" height="573" alt="image" src="https://github.com/user-attachments/assets/f8c47353-dbf7-4026-b4d9-89ebff6cd24d" />

<img width="1350" height="618" alt="image" src="https://github.com/user-attachments/assets/183a52c0-755d-43c6-9731-9043b047e679" />

Even though the channel bridges source to drain, without a drain voltage electrons do not flow — this is the **Cut-Off Region**.

Applying a negative body potential (Vsb > 0) increases the source-to-body junction depletion width:

<img width="1311" height="532" alt="image" src="https://github.com/user-attachments/assets/0aa83b1f-12c2-4765-bd3f-caa35daac877" />

<img width="1283" height="607" alt="image" src="https://github.com/user-attachments/assets/1dd9f64e-5345-4dc9-98b2-6dcde19765ef" />

### L4 – Effect of Positive Substrate Bias on Threshold Voltage
With a positive Vsb applied, raising Vgs widens the depletion region in both cases. However, the positive body bias pulls some channel electrons back toward the source, slowing down surface inversion.

<img width="1247" height="617" alt="image" src="https://github.com/user-attachments/assets/65d128ea-03af-4dd4-af13-28b261e0fe66" />

As a result, a higher gate voltage is required to achieve inversion — the threshold voltage increases.

<img width="1356" height="658" alt="image" src="https://github.com/user-attachments/assets/98b3483c-2c33-4244-b96d-6098ee9b0163" />

<img width="632" height="235" alt="image" src="https://github.com/user-attachments/assets/8025a009-e2dd-4e83-a4d6-c1725668e6fc" />

The body-effect coefficient Gamma is supplied by the foundry. SPICE simulations extract the actual Vt value from device measurements.

<img width="1327" height="643" alt="image" src="https://github.com/user-attachments/assets/8955fdc9-1230-4562-b513-4eca06eb5d3c" />

---

## NMOS Operating Regions: Resistive and Saturation

### L1 – Resistive Region at Low Drain-Source Voltage
Beyond the cut-off region, applying a small Vds puts the device in the **Linear (Resistive) Region**. As Vgs increases, the channel charge density grows proportionally to (Vgs – Vt).

<img width="1305" height="508" alt="image" src="https://github.com/user-attachments/assets/29f349a8-c77e-4d13-a323-82b1fa6bfb74" />

With Vt = 0.45V and a small Vds, a voltage gradient develops across the channel length.

<img width="1317" height="567" alt="image" src="https://github.com/user-attachments/assets/aed1572f-fd2b-492d-82ca-bd1ce4a94b1e" />

<img width="1318" height="577" alt="image" src="https://github.com/user-attachments/assets/bf52a8c7-5553-4c74-888c-cdb43b09e3bc" />

The effective channel length is slightly shorter than the drawn length due to depletion at the drain end.

<img width="797" height="510" alt="image" src="https://github.com/user-attachments/assets/c35a777b-b625-495c-bb37-9f92dfd92a64" />

The x-axis represents the channel voltage V(x); the y-axis shows the local charge density influenced by Vgs – V(x).

<img width="817" height="558" alt="image" src="https://github.com/user-attachments/assets/a472661e-b9bd-4cfb-8437-ea5be2474fe2" />

### L2 – Understanding Drift Current
The effective gate overdrive at any point x is (Vgs – V(x)). At x = 0, this equals Vgs; at x = Vds = 0.05V, it becomes Vgs – 0.05V. The induced charge density is directly proportional to this local overdrive.

<img width="411" height="150" alt="image" src="https://github.com/user-attachments/assets/f303fe6e-388f-4395-9650-e7121cd5aff4" />

<img width="390" height="451" alt="image" src="https://github.com/user-attachments/assets/14f8c404-0d02-4d21-8d67-b20ff1801eae" />

Since there is a voltage difference from source to drain, the current mechanism here is **Drift Current** (as opposed to diffusion current which is concentration-gradient driven).

<img width="1285" height="618" alt="image" src="https://github.com/user-attachments/assets/e1ba1c63-b342-4377-9fe8-1a2e58c93e02" />

The top-view of the transistor helps visualize how drain current flows across the channel width:

<img width="1311" height="687" alt="image" src="https://github.com/user-attachments/assets/6c473806-a163-4120-974a-73e11da97839" />

### L3 – Drain Current Model in Linear Region
Since the channel voltage varies along its length, carrier velocity — which depends on mobility and the local electric field — also varies.

<img width="448" height="651" alt="image" src="https://github.com/user-attachments/assets/6518460a-1e4c-481f-8341-d99a1fa9a376" />

Integrating the current equation with dV from 0 to Vds and dx from 0 to L gives:

<img width="442" height="428" alt="image" src="https://github.com/user-attachments/assets/382f07af-71b5-4f00-894d-bdab05e92d0e" />

<img width="377" height="48" alt="image" src="https://github.com/user-attachments/assets/f6f5158c-850f-4272-b381-0b57dc30e7a9" />

Parameters Cox, W/L, Vgs, µn, and Vt are **technology parameters** — extracted from foundry data and validated via SPICE simulation.

<img width="387" height="211" alt="image" src="https://github.com/user-attachments/assets/ee457e12-6af7-4389-a11a-036ba5a4b652" />

Note: the drain current is a quadratic function of Vds in this region. The device is in **Linear Region** only when **(Vgs – Vt) ≥ Vds**.

<img width="708" height="432" alt="image" src="https://github.com/user-attachments/assets/853ed5fa-0257-4a73-91dd-09007f16d273" />

<img width="683" height="443" alt="image" src="https://github.com/user-attachments/assets/bdfa5383-5b3b-452f-b437-0768814f2551" />

### L4 – SPICE Analysis of Resistive Operation
To fully characterize Id across different Vgs values, we sweep Vds up to (Vgs – Vt) for each bias condition — this requires SPICE simulation.

<img width="591" height="172" alt="image" src="https://github.com/user-attachments/assets/d9735c9f-3a26-49aa-bc9b-62e64d65babe" />

### L5 – Pinch-Off Condition
When Vds increases beyond (Vgs – Vt), the channel voltage at the drain end equals Vt — the channel starts to disappear at that end. This is the **Pinch-Off** condition.

<img width="1367" height="625" alt="image" src="https://github.com/user-attachments/assets/d29ecff9-3641-49c7-9348-fa7537ff7118" />

- Vgs – Vds > Vt → conducting channel exists throughout  
- Vgs – Vds = Vt → channel just begins to pinch off at drain  

<img width="1380" height="611" alt="image" src="https://github.com/user-attachments/assets/b51e39ef-093f-463d-8faa-7c6bb23cc68d" />
<img width="1352" height="621" alt="image" src="https://github.com/user-attachments/assets/8d325d80-10d4-47e3-aed0-2caaf0715a36" />

Beyond pinch-off (Vgs – Vds < Vt), no channel exists at the drain side — the device enters **Saturation**.

<img width="1492" height="602" alt="image" src="https://github.com/user-attachments/assets/40146460-641e-4f89-a950-acebeba103e3" />

<img width="1310" height="582" alt="image" src="https://github.com/user-attachments/assets/e62baac0-53e1-4c61-a9d6-e26a0a4b8ec1" />

<img width="391" height="102" alt="image" src="https://github.com/user-attachments/assets/4c0aca6a-e230-47d1-9e30-9416785487be" />

### L6 – Drain Current Model in Saturation Region
In saturation, the effective channel voltage is pinned at (Vgs – Vt), making Id independent of Vds. Substituting Vds = Vgs – Vt into the linear region equation gives the saturation drain current:

<img width="467" height="360" alt="image" src="https://github.com/user-attachments/assets/3df0adef-9616-499c-97de-477da403178b" />

Ideally this makes the MOSFET a perfect current source. However, increasing Vds actually expands the drain depletion region, slightly shortening the effective channel. This causes a weak Vds dependency in the saturation current — the **Channel Length Modulation** effect.

<img width="1476" height="586" alt="image" src="https://github.com/user-attachments/assets/899bf2cb-f752-43ad-8750-5fc9d6b62f50" />

<img width="876" height="168" alt="image" src="https://github.com/user-attachments/assets/b3d388c1-7074-49c9-a019-7d0ff212271f" />

---

## Getting Started with SPICE

### L1 – SPICE Environment Overview
The SPICE simulation environment relies on device model parameters provided by the foundry (highlighted in the figure below) along with a netlist describing the circuit.

<img width="1412" height="611" alt="image" src="https://github.com/user-attachments/assets/5872cd9a-70d1-46cf-9fe4-f5247f8d3415" />

<img width="1313" height="591" alt="image" src="https://github.com/user-attachments/assets/c7f8c503-a596-40a7-85e8-b00b1eef4cf9" />

<img width="922" height="536" alt="image" src="https://github.com/user-attachments/assets/260175cb-7abc-4fc6-a332-6b73b7954cae" />

Feeding these model parameters and the netlist into the SPICE engine produces the Id vs Vds family of curves for various Vgs values.

**SPICE Netlist** — The circuit must be described in a format the SPICE engine understands:

<img width="1262" height="585" alt="image" src="https://github.com/user-attachments/assets/ec870ea4-f7ce-4e99-939a-d6e8646c499e" />

### L2 – Writing Circuits in SPICE Syntax
To describe a circuit in SPICE:

- **Identify all nodes** — points where two or more components connect

  <img width="653" height="410" alt="image" src="https://github.com/user-attachments/assets/726a94e6-1333-41dc-a4c0-d9c766b00f9b" />

- **Assign names to each node**
- **Write the netlist** — a MOSFET has 4 terminals, described in Drain-Gate-Source-Substrate (DGSS) order

<img width="1307" height="418" alt="image" src="https://github.com/user-attachments/assets/fe360627-afb9-41d7-917d-95b7ac8ca6b7" />
<img width="1211" height="371" alt="image" src="https://github.com/user-attachments/assets/5d8f624b-296a-499a-9cc2-c9fd0946fb52" />
<img width="1213" height="412" alt="image" src="https://github.com/user-attachments/assets/c7d30d08-94c4-4891-95b3-4fc8c95fa3c9" />
<img width="1132" height="381" alt="image" src="https://github.com/user-attachments/assets/b9dad3c6-2cc6-48a5-9409-a7eb90f39301" />
<img width="1197" height="385" alt="image" src="https://github.com/user-attachments/assets/e091f59b-d7b8-4913-9ee3-0a2cc5d324f0" />

The DGSS ordering is used for this long-channel MOSFET model. Resistors are described similarly between two nodes.

<img width="1252" height="471" alt="image" src="https://github.com/user-attachments/assets/f9599207-d326-4da5-b92b-53d80a85c4cb" />
<img width="1172" height="406" alt="image" src="https://github.com/user-attachments/assets/15ce1ea6-b8d3-47f6-9ef9-978ddd83bbc6" />
<img width="1242" height="402" alt="image" src="https://github.com/user-attachments/assets/36660836-b886-4c2e-9649-d13863d65f7f" />
<img width="1263" height="416" alt="image" src="https://github.com/user-attachments/assets/880832b5-5f1b-49f3-9c01-25ef9bdc55c4" />
<img width="1247" height="463" alt="image" src="https://github.com/user-attachments/assets/1d36164e-cf12-49e3-84b5-8f2928f4a8b9" />

### L3 – Technology Parameters in SPICE
Technology parameters like mobility (µn), oxide capacitance (Cox), and threshold voltage (Vt) come from foundry model files. These are plugged into SPICE to simulate realistic device behavior.

### L4 – Running Your First SPICE Simulation
With the netlist and model files in place, SPICE sweeps the voltage sources and solves for the circuit's operating point at each step, producing the characteristic curves.

### L5 – SPICE Lab with Sky130 Models
Using Sky130 PDK model files, we simulate the Id vs Vds characteristics with realistic process parameters.

---

# Day 2 – Velocity Saturation and CMOS Inverter VTC Basics

## Short-Channel Effects and Velocity Saturation

### L1 – SPICE Simulations at Lower Technology Nodes
At smaller geometry nodes, short-channel effects become significant and the long-channel MOSFET equations no longer accurately model device behavior.

### L2 – Id vs Vgs for Long and Short Channel Devices
Long-channel devices show a quadratic Id vs Vgs relationship. Short-channel devices deviate from this due to carrier velocity saturation.

### L3 – Velocity Saturation at Different Electric Fields
At low electric fields, carrier velocity increases linearly with field strength. At high electric fields (encountered in short-channel devices), velocity saturates at a maximum value — this is **Velocity Saturation**.

### L4 – Velocity Saturation Drain Current Model
The velocity saturation effect modifies the drain current model. Unlike long-channel devices, short-channel devices can saturate at a lower Vds, affecting the overall current drive capability.

### L5 – Sky130 Lab: Id-Vgs Characteristics
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/17f7032a-f654-4c22-81e9-acbc1cbe368f" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/b490e2f2-76aa-49f1-b37c-e986cb3e4126" />

The short-channel device shows a more linear Id-Vgs relationship at higher Vgs values due to velocity saturation effects, as opposed to the expected quadratic behaviour in long-channel devices.

### L6 – Sky130 Lab: Threshold Voltage Extraction
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/1e4b97da-884d-4447-b8ae-4d83ff1aef33" />

Vt is identified as the gate voltage at which Id begins rising sharply. Drawing a tangent to the Id-Vgs curve and finding its x-intercept gives approximately **Vt ≈ 0.76V**.

<img width="292" height="30" alt="image" src="https://github.com/user-attachments/assets/dfd6b8ca-308f-425e-97d0-58cb1799fca4" />

---

## CMOS Voltage Transfer Characteristics (VTC)

### L1 – MOSFET Viewed as a Switch
<img width="907" height="508" alt="image" src="https://github.com/user-attachments/assets/6bb70912-c36e-4031-bf01-7e05871b28a8" />

- When |Vgs| < Vt → device OFF, behaves as an open switch  
- When |Vgs| > Vt → device ON, behaves as a closed switch  

<img width="1220" height="685" alt="image" src="https://github.com/user-attachments/assets/48869cbb-daee-4a3b-96a8-bdd0fb45a79f" />

### L2 – Standard MOS Voltage and Current Parameters
To derive the VTC and compute propagation delay, we analyse the CMOS inverter in its two steady-state conditions:

- Vin = Vdd → PMOS OFF, NMOS ON

<img width="1292" height="680" alt="image" src="https://github.com/user-attachments/assets/f65a1301-44f9-482e-b8dd-7b5cb3d39e47" />

- Vin = 0 → PMOS ON, NMOS OFF

<img width="1347" height="696" alt="image" src="https://github.com/user-attachments/assets/c15bdbc8-99af-48e0-a23c-726e7e415b66" />

When Vin = Vdd, load capacitor CL discharges through NMOS. When Vin = 0, CL charges through PMOS.

<img width="1322" height="428" alt="image" src="https://github.com/user-attachments/assets/a4f22e15-1c9a-44cf-bfa2-e27b37557439" />

Terminal naming for the CMOS inverter:

<img width="506" height="618" alt="image" src="https://github.com/user-attachments/assets/7225993f-5a53-4456-9959-3cdf52d77960" />

Note: **Idsp = –Idsn** — the drain currents are equal in magnitude but opposite in direction.

### L3 – PMOS and NMOS Id vs Vds Characteristics
<img width="485" height="677" alt="image" src="https://github.com/user-attachments/assets/f2026254-f2b7-4623-967a-79fbc649a8ea" />

<img width="897" height="432" alt="image" src="https://github.com/user-attachments/assets/2e55422f-9659-4ce7-b6ac-b1fe6d41d1a0" />

### L4 – Step 1: Mapping PMOS Gate-Source Voltage to Vin
Since the VTC is expressed in terms of external signals Vin and Vout (not internal node voltages), we convert all internal voltages. Starting assumption: long-channel device, Vdd = 2V.

<img width="372" height="237" alt="image" src="https://github.com/user-attachments/assets/081d616c-e17f-4741-8a96-0d5eae2b2b9a" />

Since Vgsp = Vin – Vdd, we get Vin = Vgsp + Vdd. The PMOS Id-Vds curve is then replotted with Vin on the x-axis:

<img width="871" height="443" alt="image" src="https://github.com/user-attachments/assets/cd415d3f-042b-460e-8314-4bb28d50d663" />

### L5 – Steps 2 & 3: Converting Drain-Source Voltages to Vout
Since Vdsp = Vout – Vdd, converting Vdsp to Vout shifts the PMOS curve left by Vdd:

<img width="1333" height="391" alt="image" src="https://github.com/user-attachments/assets/c9709e57-c876-4521-9ff6-88fb68f9927c" />

When Vout = 2V → Vdsp = 0 → zero current (capacitor fully charged). When Vout = 0V → finite charging current flows. This gives the PMOS load curve.

<img width="513" height="392" alt="image" src="https://github.com/user-attachments/assets/3a31512c-bd15-4f84-8a43-cb125285ad24" />

For NMOS: Vgsn = Vin and Vdsn = Vout directly, so the NMOS curves map straightforwardly:

<img width="223" height="75" alt="image" src="https://github.com/user-attachments/assets/ede06e12-72e7-4da9-8341-820177ed7b4e" />

<img width="410" height="287" alt="image" src="https://github.com/user-attachments/assets/e434b1a5-c734-43c2-9565-19714e01f38e" />
<img width="892" height="380" alt="image" src="https://github.com/user-attachments/assets/143a185e-09e5-4c51-8964-eae5b983c47c" />

### L6 – Step 4: Overlaying Load Curves to Obtain VTC
Superimposing both PMOS and NMOS load curves reveals the intersection points, which trace the VTC:

<img width="1340" height="412" alt="image" src="https://github.com/user-attachments/assets/e06060aa-bb37-4abc-a225-7cce4569c224" />

<img width="573" height="361" alt="image" src="https://github.com/user-attachments/assets/60499256-909d-4fad-ba5b-5a5e58d4939d" />

Operating region summary (Vdd = 2V):

| Vin | Vout Range | NMOS Region | PMOS Region |
|-----|-----------|-------------|-------------|
| 0V | 2V | Cut-Off | Linear |
| 0.5V | 1.5V – 2V | Saturation | Linear |
| 1V | 0.5V – 1.5V | Saturation | Saturation |
| 1.5V | 0V – 0.5V | Linear | Saturation |
| 2V | 0V | Linear | Cut-Off |

<img width="1332" height="687" alt="image" src="https://github.com/user-attachments/assets/e484815f-7533-4c87-a6c3-ca79158ac59e" />

---

# Day 3 – CMOS Switching Threshold and Dynamic Simulations

## VTC via SPICE Simulation

### L1 – Building the SPICE Deck for a CMOS Inverter
The SPICE deck requires: circuit topology (netlist), component values, node names, and model file references.

Circuit with M1 (PMOS) and M2 (NMOS):

<img width="546" height="501" alt="image" src="https://github.com/user-attachments/assets/87648d3d-9f23-4e6a-b66a-872306e570f1" />

Component values — equal W/L for both transistors as starting point:

<img width="622" height="487" alt="image" src="https://github.com/user-attachments/assets/01bb49d8-39b6-40e1-850f-6a6a95dc5946" />

Identifying and naming nodes:

<img width="766" height="532" alt="image" src="https://github.com/user-attachments/assets/e7a2d759-0ff9-4c2c-939e-ac4af8840cae" />

<img width="592" height="482" alt="image" src="https://github.com/user-attachments/assets/683acee0-3468-498a-9f94-c804122c5a4b" />

Complete SPICE deck (MOSFET syntax: D-G-S-S):

<img width="1227" height="585" alt="image" src="https://github.com/user-attachments/assets/1b54b47c-edea-4a16-ac0d-fe40405cd393" />

### L2 – Running the CMOS Inverter SPICE Simulation
<img width="1197" height="582" alt="image" src="https://github.com/user-attachments/assets/6d58c77a-50fe-4eab-9891-287d7a98ae44" />
<img width="1192" height="553" alt="image" src="https://github.com/user-attachments/assets/a06f6d8e-c074-4aa9-9946-6056ed71f927" />
<img width="1280" height="592" alt="image" src="https://github.com/user-attachments/assets/f4e7acd7-6158-432b-8003-b2c74656f9b0" />

Vin is swept from 0 to 2.5V in 0.05V steps. Model files supply all technology parameters.

<img width="1223" height="565" alt="image" src="https://github.com/user-attachments/assets/1bd6f151-618b-4612-82fd-6b43f7eec459" />

VTC for Wn = Wp = 0.375µm, Ln = Lp = 0.25µm (W/L = 1.5):

<img width="743" height="567" alt="image" src="https://github.com/user-attachments/assets/91c4ab55-57f1-45ab-826b-b9a9631647ee" />

VTC for Wn = 0.375µm, Wp = 0.9375µm (Wp/Lp = 2.5, so PMOS is 2.5× stronger):

<img width="741" height="572" alt="image" src="https://github.com/user-attachments/assets/5d83f191-3962-4e25-99b3-aa5d3f520d92" />

The second curve shifts right because the stronger PMOS requires higher Vin to overcome it.

### L3 – Sky130 CMOS VTC Lab
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/3e6c8b58-05e8-4c43-94a8-e1f8323a9e00" />

PMOS W/L is 2.33× larger than NMOS. Vin is swept from 0 to 1.8V in 0.01V steps.

<img width="1913" height="1078" alt="image" src="https://github.com/user-attachments/assets/a9aa02e7-a3f0-4485-9b07-129fd8260d03" />

Run `ngspice` and type `plot out vs in` to view the VTC:

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/2b2cd0ab-86fa-43cb-aae5-6192e7c52c10" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/e71074c8-50af-44c1-9316-790007b9394e" />

The switching threshold is where Vin = Vout. Zoom in using right-click + drag:

<img width="1918" height="1076" alt="image" src="https://github.com/user-attachments/assets/f23c8b99-6ef4-49e3-860b-2e0c324f4320" />

**Switching threshold for W/L = 2.3 → Vm ≈ 0.876V**

<img width="280" height="30" alt="image" src="https://github.com/user-attachments/assets/816fa465-de21-4d8d-bff4-fb79ab059723" />

Transient analysis with a pulse input (0→1V, rise/fall = 0.1ns, pulse width = 2ns, period = 4ns):

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/fe3e84fa-8511-4f02-917e-570de93216d9" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/93a365ad-7eff-4172-921b-d0301c2978f7" />
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/786bea0f-e506-4475-b099-575545bd0685" />

Propagation delays are measured at 50% of output swing (0.9V):

<img width="305" height="67" alt="image" src="https://github.com/user-attachments/assets/9e8f888e-74a1-465c-8cb5-71ee3302b0f7" />

**Rise Delay = 2.482ns – 2.15ns = 0.333ns**

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/4c675f5c-cef5-4f78-8692-67398bbf94eb" />

<img width="315" height="71" alt="image" src="https://github.com/user-attachments/assets/73197af2-d7b5-4545-a2b6-aebde88f7f20" />

**Fall Delay = 4.334ns – 4.050ns = 0.285ns**

---

## Switching Threshold and CMOS Robustness

### L1 – Switching Threshold Vm Explained
Comparing two inverters with different W/L ratios shows that while the VTC shape is preserved, Vm shifts — demonstrating the robustness of CMOS logic.

<img width="1243" height="578" alt="image" src="https://github.com/user-attachments/assets/c246dc3c-6686-4d8f-b8a5-74136a9323de" />

Drawing the 45° line intersects the VTC at Vm. Case 1: Vm ≈ 0.9V; Case 2: Vm ≈ 1.2V.

<img width="1168" height="417" alt="image" src="https://github.com/user-attachments/assets/7b300b9a-c5ee-4a11-ab44-6bc6027f8b63" />

At Vm, both transistors are simultaneously in saturation — a brief high-current condition during switching.

<img width="1083" height="462" alt="image" src="https://github.com/user-attachments/assets/5b52f85c-c43e-4b4f-b38f-e51e8fe28170" />

### L2 – Vm as a Function of (W/L)n and (W/L)p
<img width="553" height="367" alt="image" src="https://github.com/user-attachments/assets/6c11d77c-26a3-46e5-bf6c-349740e6eb00" />
<img width="860" height="53" alt="image" src="https://github.com/user-attachments/assets/b8533cc5-176d-4cb7-97c3-7d6ad5f4ec88" />
<img width="557" height="148" alt="image" src="https://github.com/user-attachments/assets/aacac08b-2543-4f88-8ddb-ce58cad2b763" />

### L3 – (W/L) Ratios as a Function of Vm
To achieve Vm = Vdd/2 = 1.25V, we work backwards from **Idsn = –Idsp**, expanding both gain factors:

<img width="962" height="362" alt="image" src="https://github.com/user-attachments/assets/4abd767b-176b-42c2-9e2e-bdf52323fed2" />

<img width="517" height="92" alt="image" src="https://github.com/user-attachments/assets/950f6372-d1d7-4c18-8cfd-5b1f35cdfce5" />
<img width="517" height="92" alt="image" src="https://github.com/user-attachments/assets/a532b030-2296-4ff8-981d-2ab29cd88dea" />

All RHS quantities come from model files — given Vm, the required W/L ratios can be solved analytically.

<img width="301" height="233" alt="image" src="https://github.com/user-attachments/assets/8534791b-2793-4986-bdad-4a2ef6bde1fe" />

### L4 – Static and Dynamic Simulation Results
For (W/L)n = (W/L)p = 1.5:

<img width="750" height="567" alt="image" src="https://github.com/user-attachments/assets/1c8f3e81-2023-429d-9a9e-b80e35d3ad09" />

Rise and fall delays from transient simulation:

<img width="1256" height="512" alt="image" src="https://github.com/user-attachments/assets/836bb013-63a3-44aa-b0d5-d640359c35f7" />

### L5 – Impact of Increased PMOS Width
With (W/L)p = 2×(W/L)n:

<img width="1181" height="507" alt="image" src="https://github.com/user-attachments/assets/7333b09a-2e41-40b2-881e-373214b16c5b" />

Vm increases since the stronger PMOS demands more current from NMOS to switch the output.

With (W/L)p = 3×(W/L)n:

<img width="1197" height="507" alt="image" src="https://github.com/user-attachments/assets/f3bea4a2-8853-4330-8886-86e6ab224069" />

<img width="1241" height="512" alt="image" src="https://github.com/user-attachments/assets/abf77cdf-93df-45b2-8373-b9d526a1c8e6" />
<img width="1207" height="512" alt="image" src="https://github.com/user-attachments/assets/978a4960-3442-4ba5-bd1b-e8f336f8812a" />

> **Key observation:** Rise delay decreases as PMOS width increases, because a wider PMOS can charge the output load capacitor faster.

### L6 – CMOS Inverter in Clock Trees and STA
Final dataset from width variation experiments:

<img width="692" height="236" alt="image" src="https://github.com/user-attachments/assets/0359ac26-996d-423d-bd27-99e08b6dddaa" />

Key takeaways:
- Vm remains relatively stable across W/L variations — demonstrating CMOS robustness during manufacturing
- When (W/L)p ≈ 2×(W/L)n, rise and fall delays become approximately equal (**symmetric inverter**) — ideal for clock buffers where symmetric delay is essential for timing closure

<img width="1110" height="653" alt="image" src="https://github.com/user-attachments/assets/30d33241-5e2f-4389-9a80-cd8d2ad5baaf" />

---

# Day 4 – CMOS Noise Margin Robustness

## Evaluating CMOS Inverter Robustness: Noise Margin

### L1 – What is Noise Margin?
**Noise Margin** quantifies how much spurious noise on an input a logic gate can absorb while still producing a correct output. An ideal inverter would have an infinite transition slope — output switches instantaneously from VOH to VOL as Vin crosses Vm.

<img width="557" height="451" alt="image" src="https://github.com/user-attachments/assets/2465a4e2-199d-4698-aa7d-58f0b42f0c6f" />

In practice, parasitic capacitances and resistances produce a finite transition slope:

<img width="368" height="316" alt="image" src="https://github.com/user-attachments/assets/f8f2f3f3-dc21-45eb-90b7-c9f2fdb8ef94" />

Valid logic levels:
- 0 ≤ Vin ≤ VIL → Output = VOH (logic HIGH)
- VIH ≤ Vin ≤ Vdd → Output = VOL (logic LOW)

<img width="405" height="342" alt="image" src="https://github.com/user-attachments/assets/8e3c22bf-b012-4a75-a08d-910511ed2980" />

### L2 – Noise Margin Voltage Parameters
The actual VTC of a CMOS inverter has a non-infinite slope. The valid output voltage ranges must satisfy **VOL < VOH < Vdd** and **0 < VOL < VIL**.

<img width="356" height="337" alt="image" src="https://github.com/user-attachments/assets/d848d4c0-de9b-4b6b-8c6a-f3006bae557c" />

The transition region has a slope of approximately –1 (unity gain points define VIL and VIH).

### L3 – Noise Margin Equations and Summary
Plotting all four voltage levels on a common scale:

<img width="733" height="443" alt="image" src="https://github.com/user-attachments/assets/c25a3266-d8f3-4e16-8afa-298756b3a59d" />

- **Noise Margin High (NMH)** = VOH – VIH  
- **Noise Margin Low (NML)** = VIL – VOL  

Any noise within these margins keeps the logic level unambiguous. Noise exceeding the margins puts the output in the undefined region.

<img width="783" height="423" alt="image" src="https://github.com/user-attachments/assets/80791538-0e36-46a8-9bf1-043e740dd778" />

<img width="822" height="481" alt="image" src="https://github.com/user-attachments/assets/6443e129-644a-4d0d-a4c4-0439ba4165de" />

### L4 – Noise Margin vs PMOS Width
To find VIL and VIH, locate where the VTC slope equals –1 and project onto both axes:

<img width="1207" height="542" alt="image" src="https://github.com/user-attachments/assets/5ab8cb26-4ab7-4e77-9a04-be82cfcdac12" />

Larger noise margins indicate a more noise-immune design:

<img width="1175" height="523" alt="image" src="https://github.com/user-attachments/assets/98daed0b-5528-4d72-8a99-06806511d1b8" />
<img width="1197" height="503" alt="image" src="https://github.com/user-attachments/assets/89b5f850-df64-4e6e-abcb-366cc3755d13" />
<img width="1203" height="517" alt="image" src="https://github.com/user-attachments/assets/13199ec4-704c-4812-aba2-38257330e40b" />

Beyond (W/L)p = 4×(W/L)n, noise margins plateau — further width increases offer diminishing returns.

<img width="677" height="226" alt="image" src="https://github.com/user-attachments/assets/fca7bcac-471c-4114-8c64-4b97cba1f5b0" />

The noise margin analysis also reveals the boundary between **Digital** and **Analog** operating regions of the CMOS inverter:

<img width="741" height="546" alt="image" src="https://github.com/user-attachments/assets/3e9a0cf6-a232-4ff2-ad4c-214b03803af3" />
<img width="772" height="542" alt="image" src="https://github.com/user-attachments/assets/56c5c94d-b59f-456c-ba92-b22fab03b6d9" />

### L5 – Sky130 Noise Margin Lab
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/af440785-3266-41ad-97ed-dd819824aaa5" />
<img width="1918" height="1077" alt="image" src="https://github.com/user-attachments/assets/58aba228-174c-453c-90df-e81aeab49d53" />

PMOS/NMOS W/L ratio = 2.77; Vin swept from 0 to 1.8V in 0.01V steps.

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/7e8e9139-43f7-4aa7-9737-9e7e378d443b" />
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/bc470f7d-f493-47c5-89e9-dfbad4e053bb" />

At slope = –1: x-axis gives VIL and VIH; y-axis gives VOH and VOL.

<img width="278" height="60" alt="image" src="https://github.com/user-attachments/assets/501565f8-b944-4af8-854b-a9f1eded062b" />

**NMH = VOH – VIH = 1.70952 – 0.98778 = 0.72V**  
**NML = VIL – VOL = 0.7733 – 0.09523 = 0.678V**

---

# Day 5 – Power Supply and Device Variation Robustness

## Robustness to Power Supply Variation

### L1 – SPICE Simulations for Power Supply Scaling
As process nodes shrink, the operating supply voltage scales down. The CMOS inverter must maintain consistent characteristics under this scaling.

<img width="1172" height="328" alt="image" src="https://github.com/user-attachments/assets/03dcd0b9-4dd3-4762-83b2-9cbb882e7bc3" />
<img width="723" height="442" alt="image" src="https://github.com/user-attachments/assets/e403056b-c4bb-4b18-a67c-baf5b02842ab" />
<img width="717" height="436" alt="image" src="https://github.com/user-attachments/assets/f357c6d2-fa02-43bc-bf51-184494cf8858" />
<img width="421" height="171" alt="image" src="https://github.com/user-attachments/assets/25f4e021-6818-4e30-85d9-cf300b35bd03" />

VTC characteristics for Vdd = 2.5V, 2V, 1.5V, 1V, and 0.5V:

<img width="742" height="568" alt="image" src="https://github.com/user-attachments/assets/87cf496c-6386-4374-9e92-1a6ef71959c1" />

### L2 – Trade-offs of Low Supply Voltage
The **Gain Factor** (|ΔVout/ΔVin|) characterizes the sharpness of the VTC transition:

<img width="968" height="516" alt="image" src="https://github.com/user-attachments/assets/dd11da87-d570-4fe1-9439-bd449e39af6a" />

<img width="976" height="547" alt="image" src="https://github.com/user-attachments/assets/102b9c1b-82ce-4d72-bc7e-fb502591c636" />

<img width="1000" height="526" alt="image" src="https://github.com/user-attachments/assets/f9a05a5f-40c0-4bad-be1f-3cd16f1445f4" />
<img width="927" height="527" alt="image" src="https://github.com/user-attachments/assets/b96be82f-5993-4fd1-9cc2-c0756dc212df" />

**Advantages of lower supply voltage:**

<img width="722" height="212" alt="image" src="https://github.com/user-attachments/assets/ab3ef568-d3f7-44cb-a6c5-6524ba5b72ec" />

**Disadvantages:** At lower Vdd, CL charges and discharges more slowly — both rise delay and fall delay increase, degrading circuit performance.

### L3 – Sky130 Supply Variation Lab
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/94a3c1ba-3139-4838-b302-2320ce3f643e" />
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/56419121-44bb-4f73-9084-06b1503b6544" />

Starting from Vdd = 1.8V, stepped down in 0.2V increments (6 simulation runs):

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/af291d32-1484-4d6b-8291-dabc5b70df65" />

Gain measurements:

- **Vdd = 1.8V:** Gain = 7.62

  <img width="292" height="61" alt="image" src="https://github.com/user-attachments/assets/0f2be4f4-0e6f-4d6f-b0c2-5ef6fa17bd3e" />

- **Vdd = 0.8V:** Gain = 9.38

  <img width="267" height="52" alt="image" src="https://github.com/user-attachments/assets/112695f4-b69a-4c76-bd41-a066a08ac6b7" />

---

## Robustness to Device Variation

### L1 – Variation Source: Etching Process
During fabrication, the lithographic etching process introduces variation in the physical dimensions of the gate — both length (L) and width (W) can deviate from the target values.

<img width="1208" height="580" alt="image" src="https://github.com/user-attachments/assets/f4496266-b2a9-4e21-bb84-54e6519478e4" />

In a chain of inverters, dimensional variation is more pronounced at the array boundaries than in the center:

<img width="1288" height="652" alt="image" src="https://github.com/user-attachments/assets/a326d12c-e0b7-4daa-bf13-311ccaa8e476" />
<img width="1121" height="618" alt="image" src="https://github.com/user-attachments/assets/8683fe6c-a634-4720-98d4-8ef619ab52b1" />

<img width="1324" height="621" alt="image" src="https://github.com/user-attachments/assets/998d8d7c-941f-4643-a768-13896c578018" />

Since drain current depends on W/L, any geometric variation directly impacts the inverter's electrical characteristics:

<img width="926" height="483" alt="image" src="https://github.com/user-attachments/assets/b1c7130a-de89-4cf1-ab2e-064702878082" />

### L2 – Variation Source: Gate Oxide Thickness
The gate oxide layer beneath the polysilicon gate can vary in thickness (tox) during deposition.

<img width="1318" height="561" alt="image" src="https://github.com/user-attachments/assets/25b705ca-1d73-4127-a9bc-a69e2af0c8c2" />
<img width="826" height="377" alt="image" src="https://github.com/user-attachments/assets/df455509-4718-4074-9eda-bb314e6462c0" />

Since **Cox = εox / tox**, any variation in oxide thickness directly changes the gate capacitance and consequently the drain current.

<img width="1205" height="597" alt="image" src="https://github.com/user-attachments/assets/a802cce3-df91-4e80-9b34-d2f931de9f8d" />

<img width="1162" height="461" alt="image" src="https://github.com/user-attachments/assets/d06ee6da-3467-41cb-8a0e-280b15faae56" />

### L3 – SPICE Simulation Under Device Variations
We test two corner cases to evaluate robustness:
- **Strong PMOS / Weak NMOS** — wider PMOS, lower resistance path to Vdd
- **Weak PMOS / Strong NMOS** — wider NMOS, lower resistance path to Vss

<img width="1148" height="339" alt="image" src="https://github.com/user-attachments/assets/398d01a6-ffc4-4a10-86a8-3907d3214b69" />
<img width="594" height="436" alt="image" src="https://github.com/user-attachments/assets/41b1f2f6-c4ba-4c71-a8e6-d1fc8e3b4844" />
<img width="695" height="398" alt="image" src="https://github.com/user-attachments/assets/9314e15f-c027-47ba-b34e-f35d886e5aff" />
<img width="726" height="321" alt="image" src="https://github.com/user-attachments/assets/280f196e-1bde-417a-9955-7a0f2029ee39" />
<img width="753" height="567" alt="image" src="https://github.com/user-attachments/assets/33e8fc0e-5220-4dc4-8da9-4c8dd5406e02" />

### L4 – Summary and Conclusions
<img width="994" height="537" alt="image" src="https://github.com/user-attachments/assets/aec473f9-00f5-4028-b122-fa2922affcb3" />

- Strong PMOS shifts Vm to the right; Strong NMOS shifts Vm to the left

<img width="1006" height="541" alt="image" src="https://github.com/user-attachments/assets/38851b7b-ec82-4400-93d8-c3c651d51ae9" />

- Despite these corner variations, the noise margins remain largely unchanged — confirming that the CMOS inverter is robustly designed

<img width="519" height="169" alt="image" src="https://github.com/user-attachments/assets/edd63a58-b8bb-462e-84e5-b8c977d4a4d2" />

### L5 – Sky130 Device Variation Lab
<img width="1912" height="1079" alt="image" src="https://github.com/user-attachments/assets/5b26708d-6351-4aa8-b2d2-758a174a6f8b" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/518ac3f8-9460-49ab-943e-e09cc37ca4ac" />

In this lab, PMOS width is significantly larger than NMOS — a Strong PMOS / Weak NMOS corner. Vm is expected to shift rightward.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ef15e759-7036-445a-b5b1-53b0df38050a" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/841f9eea-395a-4213-93c5-8e5a06de59f0" />

The simulation results confirm the expected right-shift of Vm, validating the theoretical model and demonstrating the CMOS inverter's inherent robustness across process corners.
