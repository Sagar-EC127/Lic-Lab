# Linear Integrated Circuits Laboratory  

## Experiment 2: Common Source Amplifier – CONFIGURATIONS (TSMC 180nm)

## 1. AIM
To design and analyze the following MOS amplifier configurations using TSMC 180nm CMOS models in LTspice:

1. Source-Degenerated Common Source Amplifier  
2. Cascode Amplifier  
3. Current-Mirror Loaded Common Source Amplifier  

---

## 2. SOFTWARE REQUIRED
- LTspice Tool
- TSMC 180nm Model Library  
- Supply Voltage: **VDD = 1.5 V**  
- NMOS and PMOS Devices  

---

## 3. THEORY

### 3.1 Overview of MOS Amplifiers
MOSFET-based analog amplifiers rely on operating the transistor in the **saturation region**, where the drain current becomes relatively independent of drain voltage.  
This region provides:

- High transconductance  
- Better linearity  
- Reliable voltage gain  
- Predictable small-signal behavior  

In saturation:

ID = (1/2) μCox (W/L) (Vov)^2 

Small-signal parameters:


gm = 2ID / Vov  

ro = 1 / (λID)


Voltage gain for a CS stage:

Av = -gm × Rout

---

### 3.2 Source-Degenerated Common Source Amplifier
This amplifier inserts a resistor \(R_s\) between the source terminal and ground.  
It offers:

- Local negative feedback  
- Higher linearity  
- Reduced gain sensitivity to device variations  
- Improved thermal and bias stability  

The small-signal gain becomes:

Av = -gm1 * Rout / (1 + gm1 Rs)

---

### 3.3 Cascode Amplifier
A cascode stage stacks a **common-source** MOSFET with a **common-gate** MOSFET.  
Advantages include:

- Very high output resistance  
- Reduced Miller effect  
- Higher voltage gain  
- Larger bandwidth  
- Better isolation between input and output  

Output resistance:

Rout ≈ gm3 * ro3 * ro1

Voltage gain:

Av = -gm1 * Rout

---

### 3.4 Current Mirror Loaded CS Amplifier
Uses a diode-connected MOSFET and a matched transistor to form an active load.  
Provides:

- Accurate bias current  
- High integration efficiency  
- Moderate gain  
- Avoids large resistors on-chip  

Voltage gain:
Av = -gm1 * Rout

---

## 4. DEVICE PARAMETERS (UPDATED FOR TSMC 180nm)

| Parameter | Value |
|----------|-------|
| Technology | TSMC 180 nm |
| Supply Voltage | **1.5 V** |
| Target Drain Current | **200 µA** |
| Overdrive Voltage | **0.25 V** |
| Channel Length (L) | **180 nm** |
| NMOS Mobility (µn) | 273.8 × 10⁻⁴ m²/Vs |
| PMOS Mobility (µp) | 115.7 × 10⁻⁴ m²/Vs |
| Oxide Thickness (tox) | 4.1 nm |
| Oxide Permittivity (εox) | 3.54 × 10⁻¹¹ F/m |

Gate oxide capacitance:

 Cox = εox / tox  

Cox = (3.54 × 10⁻¹¹) / (4.1 × 10⁻⁹) 

Cox = 8.634 mF/m² 

---
## 5. OPERATING CONDITIONS FOR SATURATION

For NMOS:  VDS ≥ Vov

For PMOS: VSD ≥ |Vov|

Drain Current:

ID = (1/2) μCox (W/L) (Vov)^2

Transconductance:

gm = 2ID / Vov

Output Resistance:

ro = 1 / (λID)

---

## 6. PROCESS TRANSCONDUCTANCE PARAMETERS

### NMOS:
(calculated using Device Parameters(From Datasheet))
μnCox = μn × Cox  

μnCox = 0.0273809 × 8.634 × 10⁻3  

μnCox = 2.363 × 10⁻4 A/V²  

μnCox ≈ 236 µA/V²  

------------------------------------------------------------
### PMOS:
μpCox = μp × Cox  

μpCox = 0.011568 × 8.634 × 10⁻3  

μpCox = 9.99 × 10⁻5 A/V² 

μpCox ≈ 100 µA/V²

---

## 7. WIDTH CALCULATIONS (L = 180 nm)

Using:

ID = (1/2) μCox (W/L) (Vov)^2  

Rearranging:

W = (2 ID L) / [μCox (Vov)^2]

### 7.1 NMOS Width

Wn = (2 × 200×10⁻6 × 180×10⁻9)   / [2.303×10⁻4 × (0.25)^2]

Wn = (7.2 × 10⁻11) / (1.439 × 10⁻5)

Wn = 5.002 µm  


### 7.2 PMOS Width

Wp = (2 × 200×10⁻6 × 180×10⁻9)   / [9.735×10⁻5 × (0.25)^2]

Wp = (7.2 × 10⁻11)  / (6.095 × 10⁻6)

Wp = 11.83 µm  

---

## FINAL DIMENSIONS

| Transistor | W (µm) | L (µm) | W/L |
|------------|--------|--------|------|
| NMOS | **5** | **0.18** | 27.777 |
| PMOS | **11.83** | **0.18** | 65.722 |

### Key Notes:
- PMOS width > NMOS width due to lower hole mobility.  
- Dimensions ensure ID ≈ 200 µA for VOV = 0.25 V.  

---

