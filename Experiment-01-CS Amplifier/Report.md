# Experiment 1:  Design of Common Source Amplifier using NMOS (TSMC 180nm)


---

Q1)Design a Common Source (CS) amplifier using an NMOS transistor in TSMC 180nm technology library using LTspice with the given initial conditions :

- Supply voltage (VDD) = 1.5V  
- Power constraint P ≤ 0.5mW  
- Load capacitance CL = 1pF  
- Channel length Ln = 180nm  

Do The DC analysis, transient analysis and AC frequency response analysis and study the effect of load capacitance on gain and bandwidth.


# Introduction

Amplifiers form the core of analog circuit design, enabling weak signals to be strengthened for further processing.  
In MOSFET-based analog design, three basic configurations are commonly used:

- **Common Source (CS)**
- **Common Drain (CD)**
- **Common Gate (CG)**

Among these, the **Common Source amplifier** is the most popular choice for voltage amplification because it delivers:

- Significant voltage gain  
- Reasonably high input impedance  
- Good output voltage swing  
- An inherent phase reversal of 180° between input and output  

In comparison:  
- **CD (Source Follower)** → provides unity gain and acts as a buffer  
- **CG** → suitable for high-frequency and low-input-impedance applications  

Thus, the CS topology becomes the preferred option for general-purpose signal amplification in integrated circuits.

A MOSFET works as a voltage-controlled current device. Small variations at the gate terminal modulate the channel current, and this varying current develops an amplified voltage at the drain node through the drain resistor.

For the MOSFET to function effectively as an amplifier, it must be biased in the **saturation region**, defined by:

VGS > VTH  
VDS ≥ (VGS − VTH)

In real CMOS technologies, every MOSFET includes intrinsic parasitic capacitances such as:

- **Gate–source capacitance (Cgs)**  
- **Gate–drain capacitance (Cgd)**  
- **Drain–body capacitance (Cdb)**  

These capacitances influence the high-frequency performance, introducing poles and limiting bandwidth.  
When an external **load capacitor** is added, the bandwidth reduces further, illustrating the typical gain-bandwidth trade-off encountered in analog design.

# Circuit
<img width="944" height="673" alt="image" src="https://github.com/user-attachments/assets/6b468354-6584-4def-8bd5-b56879ae2611" />

# Device Parameters (Extracted from MOSFET Specifications)

The following physical parameters are taken from the MOSFET technology data and are used for calculating the required electrical values.

### **1. Threshold Voltage**
The device begins to conduct when the gate-to-source voltage exceeds:
- **Vth = 0.36 V**


### **2. Oxide Thickness**
The gate oxide layer has a thickness of:
- **t_ox = 4.1 × 10⁻⁹ m**



### **3. Electron Mobility**
Carrier mobility for electrons in this technology is:
- **μₙ = 273.809 × 10⁻⁴ m²/V·s**


### 4. Oxide permittivity: εox = εr ε0 = 8.854 × 10⁻¹² × 3.9  
εox = 3.45 × 10⁻¹¹  

Oxide capacitance: Cox = εox / tox  
Cox = (3.45 × 10⁻¹¹) / (4.1 × 10⁻⁹)  
Cox = 8.414 mF/m²  

### Calaculations :
# DC Analysis

Power given:

P ≤ 0.5 mW  

Since:

P ≤ VDD*ID  

ID ≤ P / VDD

ID ≤ (0.5 × 10⁻³) / 1.5

ID ≤ 333.333 µA  

Let us assume:

ID = 200 µA  

Power condition check:

P = ID × VDD  

P = 200µA × 1.5  

P = 0.3 mW < 0.5 mW  (It is satisfied for the assumed Current we can take any current value less than 333.33 µA  )

### Midpoint Bias :
In a Common Source amplifier, the MOSFET should be biased so that the output signal can swing as much as possible without distortion (clipping).
This happens when the operating point (Q-point) is placed in the middle of the load line

VDS = Vout = VDD / 2
VDS = 1.5 / 2 = 0.75 v

Drain resistor:

RD = (VDD − VDS) / ID  

RD = (1.5 − 0.75) / 200µA  

RD = 3.75 kΩ

### For Saturation Region :

VDS ​≥ VGS ​− VTH

​0.75 ​≥ VGS ​− 0.36

 VGS ​≤ 1.11 V

 Using MOSFET Current  equation (In Saturation Region) : 

ID = (1/2) μn Cox (W/L) (VGS − Vth)²  

Rearranging:

W = (2 ID L) / [μn Cox (VGS − Vth)²]

Substituting values:

W ≈ 1.07 µm  

For Theoretically fixed value ID of 200µA we get width of w ≈ 1.07µm.

But ,Practically to get same vaue of  ID ≈ 200µA in simulation, width increased to:

W ≈ 1.534 µm  

As from the current equation w is directly proportional to ID
- If width increases, current increases
- If length increases, current decreases because resistance increases(Inversely  proportional)

### DC Operating Point :
<img width="807" height="483" alt="image" src="https://github.com/user-attachments/assets/f14887b1-8d4d-4f8a-9096-306e0d888bcc" />

VDS ≈ 0.75 V

Check saturation:

VGS ≥ Vth
VDS ≥ VGS − Vth

Condition satisfied → MOSFET in saturation 

# DC Sweep Analysis
DC Sweep is an analysis in LTspice (or any circuit simulator) where the DC value of a voltage source or current source is varied gradually over a specified range.
For each step, the simulator calculates the circuit’s DC operating point.

In MOSFET circuits, performing a DC sweep of VGS helps in:

- Identifying the threshold voltage
- Observing how drain current (ID) changes
- Locating saturation, cutoff, and triode regions
- Choosing the correct bias point (Q-point) for amplification
<img width="1355" height="824" alt="image" src="https://github.com/user-attachments/assets/09ecef02-00ed-46ee-ac1f-cc041fe169d5" />

# Transient Analysis(Time-Domain Response)
A 1 kHz AC sine wave was applied to the gate of the MOSFET to observe the dynamic behavior of the Common-Source (CS) amplifier. The transient simulation helps verify amplification, phase inversion, and time-domain linearity

Input Signal (Vin)
- Frequency : 1 kHz
- Amplitude : 19.192 mV peak-to-peak
- The signal is small enough to ensure that the MOSFET operates in the linear small-signal region around the bias point.
<img width="1919" height="886" alt="Screenshot 2026-02-23 234318" src="https://github.com/user-attachments/assets/dc018d1e-6892-4918-baee-6a07140a3a80" />


Output Signal (Vout)
- Measured amplitude: 43.919 mV peak-to-peak
- The waveform is inverted, confirming the expected 180° phase shift of a CS amplifier.
- The output waveform shows no clipping or distortion, indicating proper biasing and stable operation.
<img width="1915" height="884" alt="Screenshot 2026-02-23 234155" src="https://github.com/user-attachments/assets/1da65a4e-54e9-4310-84ab-e29bc6ff0e48" />


Both input and output :
- Input and output waveforms were displayed together for comparison.
- Output amplitude is higher than input, indicating amplification.
- Output is 180° out of phase, confirming inversion in the CS amplifier.
- A small DC shift is present because of biasing.
- Overall results verify that the Common-Source amplifier operates correctly.
<img width="1906" height="863" alt="Screenshot 2026-02-23 234513" src="https://github.com/user-attachments/assets/21775d55-6ac5-4f67-b613-d0dd3ca0bbcc" />

Caiculations :

Vin(p-p) = 909.586 mV − 890.394 mV
Vin(pp) = 19.192 mV

Vout(p-p) = 769.445 mV − 725.526 mV
Vout(p-p) = 43.919 mV

Practical gain:

Av = Vout / Vin

Av = 43.919 / 19.192

Av = 2.288 v/v

Gain in dB:

Av(dB) = 20 log(2.288)

Av(dB) = 7.189 dB

Theoretical Gain Calculation 

For a CS amplifier, the small-signal voltage gain is given by:
Av ​= − gm ​RD​
Where:
- 𝑔𝑚 = transconductance of MOSFET
- 𝑅𝐷 = drain resistance
- Negative sign indicates 180° phase inversion

gm = 2ID / VGS − VTH
gm = (2 × 200µA) / (0.9 − 0.36)

gm = 0.74 mS

Av = 0.74 × 10⁻³ × 3.75 × 10³

Av = 2.775 v/v

Gain in dB:

20 log(2.775) = 8.865 dB

These are the reasons why the Practical Gain < Theoretical Gain 

- Channel-length modulation reduces effective gain (finite output resistance r_o)
- Loading effect decreases gain because the effective load is (R_D || R_L)
- Parasitic resistances inside the MOSFET reduce the actual voltage gain
- Biasing may not be ideal, causing the actual g_m to be lower than theoretical
- Parasitic capacitances slightly reduce gain even at low frequencies
- Measurement probe loading reduces the output amplitude	​

# AC Analysis

## Without Load Capacitor	
Since the circuit includes only MOSFET parasitic capacitances, the frequency response remains wide, resulting in high bandwidth
<img width="1919" height="856" alt="Screenshot 2026-02-24 202846" src="https://github.com/user-attachments/assets/b62c94c0-a3f5-4ab0-afce-58a27ccbe2cd" />

Without capacitors, the CS amplifier shows a flat gain because only resistive elements control 
the midband response. The gain starts decreasing only at very high frequencies due to MOSFET 
parasitic capacitances, giving the circuit a very high bandwidth.

- 3dB gain:≈ 4.189dB  

- upper Cutoff frequency:≈ 100 GHz  


## With Load Capacitor CL = 1pF

With coupling/bypass capacitors, the amplifier shows limited bandwidth because these capacitors create additional low-frequency and high-frequency poles that reduce the gain at both ends of the frequency range.

<img width="1909" height="854" alt="image" src="https://github.com/user-attachments/assets/1586d653-fb08-46df-97d8-fe80f5c931c3" />


- 3dB gain point: 4.189 dB 
- Cutoff frequency:≈ 47.86 MHz

## Effect of Load Capacitance on Frequency Response (AC Analysis)

 Case 1: Without Load Capacitor (CL = 0)
- Only MOSFET parasitic capacitances (Cgd, Cdb) are present.
- These capacitances are very small (fF range), so the RC time constant is extremely low.
- This pushes the dominant pole to a very high frequency.

**Observed −3dB Frequency:** **≈ 100 GHz**

---

Case 2: With Load Capacitor (CL = 1 pF)
- Adding a 1 pF capacitor increases the output capacitance significantly.
- The larger capacitance forms a dominant low-pass RC pole at the output.
- This reduces the amplifier bandwidth sharply.

**Observed −3dB Frequency:** **≈ 47.86 MHz**

---
 Summary
- **Without CL:** very small capacitance → extremely high bandwidth.  
- **With CL:** large capacitance → dominant pole at low frequency → reduced bandwidth.

### **Theoretical Calculations for Voltage Gain (Av)**

To calculate the theoretical voltage gain of the Common Source amplifier, we first determine the transconductance ($g_m$) of the MOSFET at our chosen operating point.

**Step 1: Calculate Transconductance ($g_m$)**
Using the first-order square-law approximation for a MOSFET in the saturation region:
$$g_m \approx \frac{2 I_D}{V_{GS} - V_{TH}}$$

Based on the circuit design and the `tsmc018.lib` SPICE model:
* **ID:** 200 µA (from DC operating point simulation)
* **VGS:** 0.9V (Input DC bias)
* [cite_start]**VTH:** 0.366V (Nominal threshold voltage `VTH0` extracted from the TSMC 180nm library [cite: 2])

$$g_m = \frac{2 \times 200 \times 10^{-6}}{0.9 - 0.36}$$
$$g_m = \frac{ 400 \times 10^{-6}}{0.54}$$
$$g_m \approx 0.74 \text{ mA/V}$$

**Step 2: Calculate Ideal Voltage Gain**
If we assume the internal output resistance ($r_o$) is infinitely large, the ideal gain formula is:
$$A_v \approx -g_m R_D$$

Given our drain resistor is 3.75 kΩ:
$$A_v = -(0.749 \times 10^{-3}) \times (3.75 \times 10^3)$$
$$A_v \approx - 2.77 \text{ V/V}$$
*(Note: The negative sign denotes the 180° phase inversion typical of a Common Source amplifier).*

**Step 3: Calculate Practical Voltage Gain (Including $r_o$)**
In 180nm short-channel devices, channel-length modulation significantly lowers the internal output resistance ($r_o$). Because $r_o$ acts in parallel with $R_D$, the exact gain equation is:
$$A_v = -g_m (r_o || R_D)$$

Using the practical $r_o$ value of approximately 10.7 kΩ (derived from the simulation's `gds` parameter):
$$r_o || R_D = \frac{10.7 \times 3.75}{10.7 + 3.75} \approx 2.77 \text{ k}\Omega$$
$$A_v = -(0.74 \text{ mA/V}) \times (2.77 \text{ k}\Omega)$$
$$A_v \approx -2.04 \text{ V/V}$$

**Conclusion:**
The calculated practical gain of **-2.04 V/V** almost perfectly matches the simulated transient analysis result of **-2.28 V/V** (magnitude), validating the SPICE simulation against theoretical models.

# Summary

- The design meets the power requirement since the total power consumption is **0.3 mW**, which is safely below the **0.5 mW limit**.
- The MOSFET is confirmed to be in the **saturation region**, ensuring correct small-signal amplification.
- The **practical voltage gain** obtained from simulation is **7.189 dB**.
- The **theoretical voltage gain** based on small-signal calculations is **8.865 dB**.
- The difference between theoretical and simulated gain is due to **non-ideal MOSFET effects** such as channel-length modulation and parasitic capacitances.
- The **bandwidth without any load capacitor** is extremely high, around **100 GHz**.
- When a **1 pF load capacitor** is added, the bandwidth drops to **47.86 MHz** because of the dominant RC pole created at the output node.

### **Conclusion**

The Common Source amplifier successfully meets the design objectives of providing voltage amplification while maintaining low power consumption.  
The MOSFET is biased correctly in the saturation region, ensuring linear operation and predictable small-signal behavior. The theoretical gain and the simulated gain closely agree, with minor deviation caused by practical non-idealities such as channel-length modulation and parasitic capacitances.  

The frequency response analysis shows that the amplifier can achieve extremely high bandwidth when only intrinsic device capacitances are present. However, introducing an external load capacitor significantly reduces the bandwidth, demonstrating the dominant effect of output capacitance on high-frequency performance.  

Overall, the CS amplifier achieves stable gain, satisfies the power constraint, and exhibits behavior consistent with MOSFET theory and SPICE simulations, validating the design and analysis.


---

# Other CS Configurations 

## Circuit

<img width="1157" height="773" alt="Screenshot 2026-03-16 175640" src="https://github.com/user-attachments/assets/77de9abd-94b7-4400-9e4c-1bbf0fcc4f2b" />

| Device | Function |
|------|------|
| M1 | NMOS amplifier |
| M2 | PMOS active load |

Supply voltage:

VDD = **1.5 V**

---

# DC Bias Condition

To obtain maximum symmetric swing:

Formula:

Vout = VDD / 2

| Parameter | Value |
|------|------|
| VDD | 1.5 V |
| Vout | 0.75 V |
| VD1 | 0.75 V |
| VD2 | 0.75 V |
| VG2 | 0.75 V |

# Saturation Condition (NMOS) M1

Condition:

VDS ≥ VGS − VTH

Using the boundary condition:

VGS = VDS + VTH

| Parameter | Value |
|------|------|
| VDS | 0.75 V |
| VTH | 0.366 V |
| VGS | 1.116 V |

Since

VDS ≥ VGS − VTH

0.75 ≥ 1.116 − 0.366  
0.75 ≥ 0.75

Therefore the **NMOS operates in saturation region**.
---

# Operating Point (LTspice)

<img width="803" height="632" alt="1_other configuration" src="https://github.com/user-attachments/assets/ea641d8c-3919-4827-ac93-339cc5724c61" />

| Parameter | Value |
|------|------|
| Vin | 1.116 V |
| Vout | 0.751 V |


---

# MOSFET Width Calculation

MOSFET current equation:

ID = (1/2) μCox (W/L) (Vov)²

---

## NMOS Width

| Parameter | Value |
|------|------|
| Initial Width (W1) | 0.55 µm |
| Balanced Width | **0.8296 µm** |
| Length | 0.18 µm |

---

## PMOS Width

| Parameter | Value |
|------|------|
| Initial Width (W2) | 5.706 µm |
| Balanced Width | **7.56 µm** |
| Length | 0.18 µm |

---

# Transient Analysis

### Input Signal

<img width="1912" height="872" alt="Screenshot 2026-03-16 175949" src="https://github.com/user-attachments/assets/58f88059-78d5-4bb1-8358-effc740f0d3f" />

Input signal:

SINE(1.116 10m 1000)

| Parameter | Value |
|------|------|
| Offset | 1.116 V |
| Amplitude | 10 mV |
| Frequency | 1 kHz |

---

### Output Signal

<img width="1919" height="877" alt="Screenshot 2026-03-16 175835" src="https://github.com/user-attachments/assets/f57a0e7f-7b54-4e65-9368-29b1a1d2462a" />


Observation:

| Property | Result |
|------|------|
| Phase | 180° inversion |
| Output bias | ≈ 0.75 V |

---

### Input vs Output

<img width="1917" height="889" alt="Screenshot 2026-03-16 180017" src="https://github.com/user-attachments/assets/bf987999-1294-48a2-9683-e92313aeaa80" />

Output waveform is **inverted with respect to input**.

---

#  AC Analysis

<img width="1917" height="889" alt="Screenshot 2026-03-16 180017" src="https://github.com/user-attachments/assets/619bb191-8dc7-47aa-b1a3-521e511f9c48" />

| Parameter | Value |
|-----------|-------|
| Midband Gain (Av) | -11.723 dB |
| 3 dB Gain | -14.723 dB |
---

#  Reason for Negative Gain

| Step | Operation |
|------|------|
| 1 | Vin increases |
| 2 | NMOS drain current increases |
| 3 | Voltage drop across PMOS load increases |
| 4 | Output voltage decreases |

Thus

Vin ↑ → Vout ↓

This produces a **180° phase shift**, resulting in **negative gain**.

---

# Final Results

| Parameter | Value |
|------|------|
| VDD | 1.5 V |
| Vout | 0.75 V |
| NMOS Width (Balanced) | 0.8296 µm |
| PMOS Width (Balanced) | 7.56 µm |
| Gain | −11.723 |


# Conclusion

The Common Source (CS) amplifier with PMOS active load was designed and analyzed using LTspice. The circuit was biased to obtain a symmetric output swing with **Vout ≈ VDD/2 (0.75 V)**. Both NMOS and PMOS transistors operate in the **saturation region**, ensuring proper amplification.

From the transient analysis, the output signal is **inverted with respect to the input**, confirming the **180° phase shift** characteristic of a CS amplifier. AC analysis shows a **midband gain of −11.723 dB**, indicating voltage amplification with phase inversion.

Thus, the circuit successfully demonstrates the operation of a **Common Source amplifier with active load**, providing stable biasing and amplification.

---

# Comparison of CS Amplifier Configurations

| Parameter | CS Amplifier (NMOS with RD) | CS Amplifier (NMOS with PMOS Active Load) |
|-----------|-----------------------------|-------------------------------------------|
| Technology | TSMC 180 nm | TSMC 180 nm |
| Supply Voltage (VDD) | 1.5 V | 1.5 V |
| Load Type | Resistor (RD = 3.75 kΩ) | PMOS Active Load |
| Bias Output Voltage | ≈ 0.75 V | ≈ 0.75 V |
| Drain Current (ID) | ≈ 200 µA |  ≈ 200 µA|
| NMOS Width | 1.534 µm | 0.8296 µm |
| PMOS Width | Not used | 7.56 µm |
| Phase Shift | 180° | 180° |
| Practical Gain | 7.189 dB | −11.723 dB |
| Bandwidth (without CL) | ≈ 100 GHz | Very high (GHz range) |
| Bandwidth (with CL = 1 pF) | ≈ 47.86 MHz | Reduced due to output capacitance |
| Output Inversion | Yes | Yes |
| Output Swing | Limited by RD | Improved due to active load |


---

# Key Observations

- Both circuits operate as **Common Source amplifiers**, producing a **180° phase inversion**.
- The **resistor-loaded CS amplifier** is simpler but provides **lower gain**.
- The **PMOS active load configuration** provides **higher effective load resistance**, resulting in **higher gain**.
- The **bandwidth decreases significantly when load capacitance is added**, demonstrating the **gain–bandwidth trade-off** in analog circuits.


