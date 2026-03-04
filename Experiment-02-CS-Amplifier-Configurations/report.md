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

### Key Equations – Source Degenerated Common Source Amplifier

| Parameter | Equation | Description |
|-----------|----------|-------------|
| Drain Current (Saturation) | ID = (1/2) μCox (W/L) (Vov)² | MOSFET drain current equation in saturation region |
| Transconductance (gm) | gm = 2ID / Vov | Small-signal transconductance of the MOSFET |
| Output Resistance (ro) | ro = 1 / (λID) | Small-signal output resistance of the MOSFET |
| Voltage Gain (Av) | Av = -gm × Rout | Voltage gain of a common source amplifier |

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

### Output Resistance and Voltage Gain

| Parameter | Equation | Description |
|-----------|----------|-------------|
| Output Resistance (Rout) | Rout ≈ gm3 × ro3 × ro1 | Approximate output resistance of the amplifier stage |
| Voltage Gain (Av) | Av = -gm1 × Rout | Voltage gain of the common source amplifier |
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

### MOSFET Operating Conditions and Small-Signal Parameters

| Parameter | Equation | Description |
|-----------|----------|-------------|
| NMOS Saturation Condition | VDS ≥ Vov | Condition required for NMOS to operate in saturation |
| PMOS Saturation Condition | VSD ≥ \|Vov\| | Condition required for PMOS to operate in saturation |
| Drain Current (ID) | ID = (1/2) μCox (W/L) (Vov)² | MOSFET drain current equation in saturation region |
| Transconductance (gm) | gm = 2ID / Vov | Small-signal transconductance of the MOSFET |
| Output Resistance (ro) | ro = 1 / (λID) | Small-signal output resistance of the MOSFET |

---

## 6. PROCESS TRANSCONDUCTANCE PARAMETERS

### Process Transconductance Parameter Calculation

| Device | Formula | Substitution | Result |
|-------|---------|--------------|--------|
| NMOS | μnCox = μn × Cox | 0.0273809 × 8.634 × 10⁻³ | μnCox = 2.363 × 10⁻⁴ A/V² ≈ 236 µA/V² |
| PMOS | μpCox = μp × Cox | 0.011568 × 8.634 × 10⁻³ | μpCox = 9.99 × 10⁻⁵ A/V² ≈ 100 µA/V² |
---

## 7. WIDTH CALCULATIONS (L = 180 nm)

Using:

ID = (1/2) μCox (W/L) (Vov)^2  

Rearranging:

W = (2 ID L) / [μCox (Vov)^2]

### Transistor Width Calculation

| Device | Expression | Intermediate Step | Calculated Width |
|------|-------------|------------------|------------------|
| NMOS Width (Wn) | Wn = (2 × 200×10⁻⁶ × 180×10⁻⁹) / [2.303×10⁻⁴ × (0.25)²] | Wn = (7.2 × 10⁻¹¹) / (1.439 × 10⁻⁵) | Wn = 5.002 µm |
| PMOS Width (Wp) | Wp = (2 × 200×10⁻⁶ × 180×10⁻⁹) / [9.735×10⁻⁵ × (0.25)²] | Wp = (7.2 × 10⁻¹¹) / (6.095 × 10⁻⁶) | Wp = 11.83 µm |
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
### EXP 2 – Circuit 2A: Source Degenerated Common Source Amplifier

**Objective**

To design and simulate a source-degenerated common source MOSFET amplifier that operates at a drain current (ID) of 200 µA while achieving maximum symmetrical output voltage swing.

**Circuit Implementation (LTspice)**

The circuit was implemented and simulated using LTspice. Appropriate MOSFET sizing and biasing conditions were selected so that the transistor operates in the saturation region with a drain current of 200 µA and provides a stable operating point for maximum symmetric output swing.

<img width="984" height="768" alt="Screenshot 2026-02-26 161121" src="https://github.com/user-attachments/assets/beee8f34-c559-4b10-a035-3eb624ac3197" />

---
# DC Analysis

## Given Design Parameters

| Parameter | Value |
|-----------|-------|
| Supply Voltage (VDD) | 1.5 V |
| Drain Current (ID) | 200 µA |
| Threshold Voltage (NMOS) | 0.36 V |
| Threshold Voltage (PMOS) | −0.39 V |

---

## Conditions for Saturation Operation

For proper amplification, both MOSFETs must operate in the **saturation region**.

| Parameter | Minimum Requirement | Maximum Limit | Purpose |
|-----------|--------------------|---------------|---------|
| VGS (NMOS) | ≥ VTHn = 0.36 V | ≤ VDD | Channel formation |
| VDS (NMOS) | ≥ Vov | ≤ VDD | Maintain saturation |
| VSG (PMOS) | ≥ \|VTHp\| = 0.39 V | ≤ VDD | PMOS conduction |
| VSD (PMOS) | ≥ Vov | ≤ VDD | Saturation condition |

---

# Selection of Drain–Source Voltage

To allow **maximum symmetrical output swing**, the transistor is biased at approximately half of the supply voltage.

| Calculation | Result |
|-------------|--------|
| VDS = VDD / 2 | 1.5 / 2 |
| VDS | **0.75 V** |

### Reason

Placing the operating point near **mid-supply voltage** allows equal headroom for positive and negative signal variations.

---

# Source Voltage Selection

A small source voltage is introduced using a **source resistor** to improve bias stability.

| Parameter | Value |
|-----------|------|
| VS | **0.2 V** |

### Explanation

| Reason | Description |
|------|-------------|
| VS > 0 | Provides source degeneration |
| VS << VDD | Maintains drain voltage headroom |
| Current stabilization | Increase in current raises VS and reduces VGS |

Thus **VS = 0.2 V** ensures stable biasing.

---

# Output Voltage Determination

The drain voltage (output node) is obtained from the relation

VDS = Vout − VS

| Parameter | Calculation | Result |
|-----------|-------------|--------|
| VDS | Vout − VS | 0.75 = Vout − 0.2 |
| Vout | 0.75 + 0.2 | **0.95 V** |

---

# Source Resistor Value

The source resistor is calculated using Ohm’s law.

| Calculation | Result |
|-------------|--------|
| RS = VS / ID | 0.2 / (200 × 10⁻⁶) |
| RS | **1 kΩ** |

---

# NMOS Gate Voltage

| Calculation | Result |
|-------------|--------|
| VGS = VTH + Vov = 0.36 + 0.25 | **0.61 V** |
| VG = VGS + VS = 0.61 + 0.2 | **0.81 V** |

---

# Verification of Overdrive Voltage

| Calculation | Result |
|-------------|--------|
| VGS = VG − VS = 0.81 − 0.2 | **0.61 V** |
| Vov = VGS − VTH = 0.61 − 0.36 | **0.25 V** |

### Valid Overdrive Range

| Minimum Vov | Maximum Vov |
|-------------|-------------|
| > 0 | < VDS = 0.75 V |

Thus

0 < Vov < 0.75

The obtained value **Vov = 0.25 V** lies within this range.

### Justification

A moderate overdrive voltage:

• ensures adequate transconductance  
• maintains stable drain current  
• provides sufficient voltage headroom

---

# PMOS Gate Voltage

| Calculation | Result |
|-------------|--------|
| VSG = Vov + \|VTHp\| = 0.25 + 0.39 | **0.64 V** |
| VGp = VDD − VSG = 1.5 − 0.64 | **0.86 V** |

---

# Saturation Verification

| Device | Condition | Verification |
|-------|-----------|--------------|
| NMOS | VDS ≥ Vov | 0.75 ≥ 0.25 ✔ |
| PMOS | VSD ≥ Vov | 0.55 ≥ 0.25 ✔ |

Both MOS transistors operate in the **saturation region**.

---

# Final DC Operating Point

| VS | VDS | Vout | VG | VGp | ID | RS | Vov |
|----|-----|------|----|-----|----|----|----|
| 0.2 V | 0.75 V | 0.95 V | 0.81 V | 0.86 V | 200 µA | 1 kΩ | 0.25 V |

The selected operating point keeps both transistors in saturation and allows sufficient voltage swing for proper amplifier operation.

<img width="685" height="560" alt="image" src="https://github.com/user-attachments/assets/5342b604-c9c2-4a94-a175-8fe8617086b2" />


## Width Optimization – Circuit 2A

The theoretical transistor widths provide an approximate starting point.  
During simulation, the widths were adjusted slightly to achieve the desired drain current of **ID ≈ 200 µA** under realistic MOSFET model conditions.

| Device | Initial Width (µm) | Adjusted Width (µm) | Justification |
|------|------------------|------------------|--------------|
| NMOS | 5 | 13.2 | The calculated width serves as an initial estimate. In practical simulations, parasitic effects and non-ideal device behavior slightly reduce the expected current. Therefore, the NMOS width was increased to obtain the required drain current close to 200 µA. |
| PMOS | 11.83 | 37.5 | Since hole mobility in PMOS devices is lower than electron mobility in NMOS devices, a wider PMOS transistor is required to deliver the same current level. Hence, the PMOS width was increased during simulation to meet the target current. |

### Design Insight

Increasing the transistor width improves the current conduction capability of the device.  
Thus, small adjustments in width were made until the circuit produced the expected **drain current of approximately 200 µA** while maintaining correct bias conditions.
