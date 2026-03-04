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

## Saturation Region Requirements

For a MOSFET amplifier to function correctly, both transistors must remain in the **saturation region**.  
Operating in this region ensures that the drain current mainly depends on the gate voltage rather than the drain voltage, which is essential for achieving stable amplification.

| Parameter | Minimum Requirement | Maximum Limit | Purpose |
|-----------|--------------------|---------------|---------|
| VGS (NMOS) | ≥ VTHn = 0.36 V | ≤ VDD | Enables channel formation |
| VDS (NMOS) | ≥ Vov | ≤ VDD | Ensures saturation operation |
| VSG (PMOS) | ≥ \|VTHp\| = 0.39 V | ≤ VDD | Allows PMOS conduction |
| VSD (PMOS) | ≥ Vov | ≤ VDD | Maintains saturation |

---

# Drain–Source Voltage Selection

To maximize the usable output range of the amplifier, the drain–source voltage is chosen close to the midpoint of the supply voltage.

| Calculation | Result |
|-------------|--------|
| VDS = VDD / 2 | 1.5 / 2 |
| VDS | **0.75 V** |

### Explanation

Positioning the operating point near half of the supply voltage provides balanced voltage headroom in both directions.  
This allows the output signal to vary without entering cutoff or triode regions.

---

# Source Voltage Choice

A small voltage drop is introduced at the source terminal through a resistor.  
This approach improves bias stability and reduces sensitivity to parameter variations.

| Parameter | Value |
|-----------|------|
| VS | **0.2 V** |

### Design Considerations

| Reason | Description |
|------|-------------|
| Positive VS | Introduces local feedback |
| Small magnitude | Prevents loss of voltage swing |
| Bias stabilization | Variations in current automatically adjust VGS |

Therefore, **VS = 0.2 V** provides a good balance between stability and voltage headroom.

---

# Output Voltage Calculation

The output voltage corresponds to the drain node voltage and is related to the drain–source voltage.

VDS = Vout − VS

| Parameter | Calculation | Result |
|-----------|-------------|--------|
| VDS | Vout − VS | 0.75 = Vout − 0.2 |
| Vout | 0.75 + 0.2 | **0.95 V** |

---

# Source Resistor Determination

The required source resistance is obtained from the selected source voltage and desired drain current.

| Calculation | Result |
|-------------|--------|
| RS = VS / ID | 0.2 / (200 × 10⁻⁶) |
| RS | **1 kΩ** |

This resistor sets the source voltage and helps maintain a constant current.

---

# NMOS Gate Bias

The gate voltage is determined from the threshold voltage and chosen overdrive voltage.

| Calculation | Result |
|-------------|--------|
| VGS = VTH + Vov = 0.36 + 0.25 | **0.61 V** |
| VG = VGS + VS = 0.61 + 0.2 | **0.81 V** |

This gate voltage ensures the NMOS operates with the desired current level.

---

# Overdrive Voltage Verification

The overdrive voltage determines the strength of inversion and the current capability of the device.

| Calculation | Result |
|-------------|--------|
| VGS = VG − VS = 0.81 − 0.2 | **0.61 V** |
| Vov = VGS − VTH = 0.61 − 0.36 | **0.25 V** |

### Acceptable Overdrive Range

| Minimum Vov | Maximum Vov |
|-------------|-------------|
| > 0 | < VDS = 0.75 V |

Thus

0 < Vov < 0.75

The selected value **Vov = 0.25 V** falls within this acceptable region.

### Design Insight

A moderate overdrive voltage is desirable because it:

• improves transconductance  
• maintains controlled drain current  
• keeps sufficient voltage margin for signal swing

---

# PMOS Gate Voltage

The PMOS gate voltage is calculated using the required source–gate voltage.

| Calculation | Result |
|-------------|--------|
| VSG = Vov + \|VTHp\| = 0.25 + 0.39 | **0.64 V** |
| VGp = VDD − VSG = 1.5 − 0.64 | **0.86 V** |

This bias ensures that the PMOS transistor supplies the required current.

---

# Saturation Verification

To confirm correct operation, both devices must satisfy their respective saturation conditions.

| Device | Condition | Verification |
|-------|-----------|--------------|
| NMOS | VDS ≥ Vov | 0.75 ≥ 0.25 ✔ |
| PMOS | VSD ≥ Vov | 0.55 ≥ 0.25 ✔ |

Since these conditions are satisfied, both MOSFETs operate in the **saturation region**, enabling proper amplification.

---

# Final DC Operating Point

| VS | VDS | Vout | VG | VGp | ID | RS | Vov |
|----|-----|------|----|-----|----|----|----|
| 0.2 V | 0.75 V | 0.95 V | 0.81 V | 0.86 V | 200 µA | 1 kΩ | 0.25 V |

This bias configuration establishes a stable operating point where both transistors remain in saturation while allowing adequate voltage headroom for the output signal.

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

---

# Transient Analysis – Circuit 2A  
(Source Degenerated Common Source Amplifier)

The dynamic behavior of the amplifier was examined using **transient analysis** in LTspice.  
A small sinusoidal signal was applied to the **gate terminal** while maintaining the required DC bias so that the MOSFET operates around its designed operating point.

---

## Applied Input Signal

| Signal Type | Frequency | Amplitude | DC Bias |
|-------------|-----------|-----------|--------|
| Sinusoidal | 1 kHz | 10 mV | 0.81 V |

---

## LTspice Input Source

The input voltage source used in the simulation is defined as:

Vin = SINE(0.81 10m 1k)

---

## Explanation

The **DC offset (0.81 V)** represents the gate bias voltage obtained from the DC analysis.  
This bias ensures that the transistor operates at the desired operating point with  
**drain current approximately equal to 200 µA**.

A small AC amplitude of **10 mV** is applied so that the amplifier operates in the **linear small-signal region**, allowing the output waveform to accurately represent the gain characteristics of the circuit.

## Input Waveform

<img width="1913" height="881" alt="inp 1" src="https://github.com/user-attachments/assets/fe077139-7bf3-40b2-8205-520ba746648a" />

The above waveform represents the sinusoidal input applied at the gate.

---

## Output Waveform


<img width="1909" height="894" alt="op 1" src="https://github.com/user-attachments/assets/d73bb7bb-b74f-45af-906e-a1da86149ee9" />

Since this is a **common source amplifier**, the output signal is inverted
with respect to the input and exhibits a larger amplitude.

## Input and Output Comparison

<img width="1919" height="874" alt="ip op 1" src="https://github.com/user-attachments/assets/71175604-fd53-40b9-a184-a312b39696b8" />


The combined waveform clearly shows amplification and the expected
**180° phase inversion**.

---
# Practical Gain Calculation from Transient Waveform

The voltage gain of the amplifier is determined using the cursor
measurements obtained from the LTspice transient plot.

---

## Input Signal Measurement

| Parameter | Value |
|-----------|------|
| Maximum Vin | 814.87795 mV |
| Minimum Vin | 805.21089 mV |
| Vin (Peak-to-Peak) | **9.667065 mV** |

---

## Output Signal Measurement

| Parameter | Value |
|-----------|------|
| Maximum Vout | 1.0011576 V |
| Minimum Vout | 901.27185 mV |
| Vout (Peak-to-Peak) | **99.885744 mV** |

---

# Voltage Gain Calculation

| Calculation | Result |
|-------------|--------|
| Av = Vout(p-p) / Vin(p-p) | 99.885744 mV / 9.667065 mV |
| Voltage Gain (Av) | **10.33 V/V** |

---

# Gain in Decibels

| Calculation | Result |
|-------------|--------|
| Gain (dB) = 20 log₁₀(Av) | 20 log₁₀(10.33) |
| Gain (dB) | **20.28 dB** |

---

# Final Result

| Vin(p-p) | Vout(p-p) | Gain (Av) | Gain (dB) |
|----------|-----------|-----------|-----------|
| 9.667065 mV | 99.885744 mV | **10.33 V/V** | **20.28 dB** |

The transient analysis shows that the amplifier produces an output
signal approximately **10.33 times larger than the input signal**,
confirming the amplification capability of the circuit.


