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



