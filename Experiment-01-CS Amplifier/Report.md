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

P ≤ 1 mW  

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

P = 0.3 mW < 1 mW  (It is satisfied for the assumed Current we can take any current value less than 333.33 µA  )

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
​





