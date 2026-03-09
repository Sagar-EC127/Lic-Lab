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


## Width Optimization 

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

# Transient Analysis  
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

---
# AC Analysis 

AC small-signal simulation was carried out to study the frequency behavior of the amplifier.  
This analysis helps in determining how the circuit responds to signals at different frequencies and allows the evaluation of the **midband voltage gain** and overall **frequency response** of the amplifier.

<img width="1919" height="878" alt="image" src="https://github.com/user-attachments/assets/169b761a-571a-45a1-827e-052f40c2cd90" />

### Frequency Response Results

| Midband Gain | −3 dB Gain | Bandwidth |
|--------------|------------|-----------|
| **20.278 dB** | **17.278 dB** | **315.183 MHz** |

The AC analysis shows that the amplifier provides a midband gain of **20.278 dB**.  
At the −3 dB point, the gain reduces to **17.278 dB**, and the measured bandwidth is **315.183 MHz**.

## Theoretical Gain 

Small-signal parameters obtained from the LTspice operating point:

| gm₁ | ro₁ | ro₂ | RS |
|-----|-----|-----|----|
| 1.6 mS | 25 kΩ | 25 kΩ | 1 kΩ |

The gain of a **source-degenerated common source amplifier**
with active load is given by:

Av = - gm₁ / (1 + gm₁RS + RS/ro₁) × ([gm₁RSro₁ + RS + ro₁] ∥ ro₂)

| Denominator | Output Resistance Term | Voltage Gain | Gain (dB) |
|-------------|-----------------------|--------------|-----------|
| 1 + 1.6 + (1k/25k) = **2.64** | ([gm₁RSro₁ + RS + ro₁] ∥ ro₂) = (40k + 1k + 25k) ∥ 25k ≈ **18.13 kΩ** | (1.6 mS / 2.64) × 18.13 kΩ ≈ **11 V/V** | 20 log₁₀(11) ≈ **20.8 dB** |

For **TSMC 180 nm technology**, the channel-length modulation parameter
λ typically lies in the range **0.1–0.2 V⁻¹**.

Using

ro = 1 / (λID)

and choosing **λ = 0.2 V⁻¹** with **ID = 200 µA**,

ro ≈ **25 kΩ**, which reduces the theoretical gain and makes it close
to the gain obtained from **AC and transient simulations**.

---
### Observation
From the AC analysis, the amplifier exhibits a midband gain of **20.278 dB**.  
This value is close to the gain obtained from both the **theoretical calculation**
and the **transient analysis**, indicating consistent amplifier performance.

### Reason for Small Difference
The small difference between theoretical and simulated values arises because
analytical calculations consider simplified device models, whereas LTspice
accounts for practical effects such as **channel-length modulation and other
non-ideal MOSFET parameters**.

-----------------------------------------------------------------------------------
### EXP2- CIRCUIT 2B – Common Source – Cascode Amplifier with Active Load
-----------------------------------------------------------------------------------
### Circuit Implementation in LTspice


<img width="894" height="813" alt="Screenshot 2026-03-01 102526" src="https://github.com/user-attachments/assets/00e1a399-5384-4141-82b5-e61cc5112627" />

## DC  Analysis  (Cascode Amplifier)

### Design Parameters

| Parameter | Value |
|-----------|------|
| Supply Voltage (VDD) | 1.5 V |
| Drain Current (ID) | 200 µA |
| Overdrive Voltage (Vov) | 0.25 V |
| NMOS Threshold Voltage (VTHn) | 0.36 V |
| PMOS Threshold Voltage (VTHp) | −0.39 V |

---

# Bottom NMOS (M2)

The lower NMOS transistor establishes the required bias current.

| Parameter | Calculation | Value |
|-----------|-------------|------|
| VGS2 | VTHn + Vov | 0.36 + 0.25 = **0.61 V** |
| Gate Voltage | Bias value | **0.61 V** |
| Source Voltage | Ground | **0 V** |
| Drain Voltage | VS1 | **0.30 V** |
| VDS2 | VD2 − VS2 | **0.30 V** |

### Saturation Verification

| Condition | Result |
|-----------|--------|
| VDS2 ≥ Vov | 0.30 ≥ 0.25 ✔ |

Thus **M2 operates in saturation**.

---

# Cascode NMOS (M1)

The cascode transistor increases output resistance and improves gain.

| Parameter | Calculation | Value |
|-----------|-------------|------|
| Gate Voltage | Given | **0.91 V** |
| Source Voltage | VS1 | **0.30 V** |
| VGS1 | VG1 − VS1 | 0.91 − 0.30 = **0.61 V** |

The output node voltage is selected using

Vout = VDS1 + VS1

| Parameter | Calculation | Value |
|-----------|-------------|------|
| VDS1 | VDD / 2 | 1.5 / 2 = **0.75 V** |
| Vout | 0.75 + 0.30 | **1.05 V** |
| VDS1 (check) | Vout − VS1 | **0.75 V** |

### Saturation Verification

| Condition | Result |
|-----------|--------|
| VDS1 ≥ Vov | 0.75 ≥ 0.25 ✔ |

Hence **M1 remains in saturation**.

---

# PMOS Active Load (M3)

The PMOS transistor provides the load current for the cascode stage.

| Parameter | Calculation | Value |
|-----------|-------------|------|
| Source Voltage | VDD | **1.5 V** |
| Gate Voltage | Given | **0.91 V** |
| VSG3 | VS − VG | 1.5 − 0.91 = **0.59 V** |

| Parameter | Calculation | Value |
|-----------|-------------|------|
| VSD3 | VS − Vout | 1.5 − 1.05 = **0.45 V** |

### Saturation Verification

| Condition | Result |
|-----------|--------|
| VSD3 ≥ Vov | 0.45 ≥ 0.25 ✔ |

Thus **PMOS load operates in saturation**.

---

# Final DC Node Voltages

| Node | Voltage |
|-----|--------|
| VS2 | 0 V |
| VS1 | 0.30 V |
| Vout | 1.05 V |

All transistors satisfy the **saturation condition**, ensuring correct operation of the cascode amplifier.

### Selection of Source Voltage (VS1)

For proper cascode operation, the lower NMOS must satisfy the
saturation condition:

VDS ≥ Vov

| VS1 | VDS2 | Condition | Result |
|----|------|-----------|--------|
| 0.2 V | 0.2 V | 0.2 < 0.25 | NMOS enters triode (not suitable) |
| 0.3 V | 0.3 V | 0.3 ≥ 0.25 | NMOS remains in saturation ✔ |

Thus, **VS1 = 0.2 V is not sufficient**, while **VS1 ≥ 0.3 V**
keeps the transistor in saturation and ensures proper
operation of the cascode amplifier.

###  LTspice Operating Point

<img width="851" height="618" alt="Screenshot 2026-03-01 102338" src="https://github.com/user-attachments/assets/32720210-a40b-4fe7-8eb1-c30ffdbc2355" />

### Width Calculation

The transistor widths required to obtain the desired drain current  
ID = 200 µA. were calculated using the square-law
saturation current equation.

| Device | Calculated Width (µm) |
|-------|----------------------|
| NMOS | **5** |
| PMOS | **11.83** |

### Practical Width Selection

During LTspice simulation, the transistor widths were adjusted
so that the circuit produces the required **ID ≈ 200 µA** while
keeping all devices in saturation.

| Transistor | Type | Width (µm) |
|-----------|------|------------|
| M1 | NMOS (Cascode) | **16.60718** |
| M2 | NMOS (Bottom) | **16.60718** |
| M3 | PMOS (Load) | **38.5** |

-----------------------------------------
## Transient Analysis 

 # Input Waveform

 <img width="1916" height="928" alt="Screenshot 2026-03-01 102857" src="https://github.com/user-attachments/assets/8568b85a-ae4d-423a-8b93-730aa312dc55" />

# Output Waveform

<img width="1913" height="875" alt="Screenshot 2026-03-01 103142" src="https://github.com/user-attachments/assets/38d263bd-6630-4f08-92cd-da4371debe6a" />

# Input & Output (Combined)

<img width="1911" height="863" alt="Screenshot 2026-03-01 103214" src="https://github.com/user-attachments/assets/208f7956-02b7-4bef-b1a9-506db2891e07" />

### Practical Gain from Transient Waveform

Peak-to-peak voltages were obtained from LTspice cursor measurements.

| Signal | Maximum | Minimum | Peak-to-Peak |
|------|--------|--------|-------------|
| Vin | 919.53398 mV | 900.45526 mV | **0.01908 V** |
| Vout | 1.0722513 V | 1.0396893 V | **0.03256 V** |

### Voltage Gain

| Calculation | Result |
|-------------|--------|
| Av = Vout(p-p) / Vin(p-p) | 0.03256 / 0.01908 |
| Voltage Gain | **1.71 V/V** |

### Gain in dB

| Calculation | Result |
|-------------|--------|
| Av(dB) = 20 log₁₀(1.71) | **4.66 dB** |


# AC Analysis

# Frequency Response 

To determine midband gain and bandwidth,
small-signal AC analysis was performed.

<img width="1913" height="863" alt="Screenshot 2026-03-01 103846" src="https://github.com/user-attachments/assets/565df979-5709-4dc7-a598-20536256cd45" />

### Frequency Response Results

| Maximum Gain | −3 dB Gain | −3 dB Frequency |
|--------------|------------|----------------|
| **4.643 dB** | **1.643 dB** | **277.41 MHz** |

---------
---
### EXP2 – CIRCUIT 2C – 

Common Source Amplifier with Diode-Connected NMOS Current Source and PMOS Active Load
-------------------------------------------------------------

<img width="1152" height="724" alt="image" src="https://github.com/user-attachments/assets/238f321f-1714-432e-a2f9-38f08a4c5a21" />

---
# DC Analysis – Circuit 2C

## Design Conditions

| Parameter | Value |
|-----------|-------|
| VDD | 1.5 V |
| ID | 200 µA |
| VTHn | 0.36 V |
| VTHp | −0.39 V |

---

## Voltage Constraints for Saturation Operation (VDD = 1.5 V)

| Parameter | Minimum Limit | Maximum Limit | Explanation |
|-----------|---------------|---------------|-------------|
| VGS (NMOS) | ≥ 0.36 V | ≤ 1.5 V | Must exceed threshold voltage for channel formation |
| VDS (NMOS) | ≥ VOV | ≤ 1.5 V | Required to keep NMOS in saturation region |
| VSG (PMOS) | ≥ 0.39 V | ≤ 1.5 V | Must exceed PMOS threshold magnitude for conduction |
| VSD (PMOS) | ≥ VOV | ≤ 1.5 V | Ensures PMOS operates in saturation |

---

# Verification of Overdrive Voltage

The overdrive voltage (VOV) ensures that the MOSFET operates in the saturation region.

## Gate Voltage Calculation

| Expression | Value |
|------------|-------|
| VGS = VTH + VOV = 0.36 + 0.25 | **0.61 V** |
| VOV = VGS − VTH = 0.61 − 0.36 | **0.25 V** |

## Valid Range for Overdrive Voltage

| Condition | Value |
|-----------|-------|
| Minimum VOV | > 0 |
| Maximum VOV | < VDS |

For the designed circuit,

VDS ≈ **0.75 V** *(approximately half of VDD = 1.5 V)*

Therefore,

0 < VOV < 0.75 V

### Design Justification

A moderate value of overdrive voltage is selected because it offers several advantages:

• Provides sufficient **transconductance (gm)** for amplification  
• Maintains a **stable drain current (ID)**  
• Leaves enough **voltage headroom for signal swing**

---

# Diode-Connected NMOS Bias (M3)

For a diode-connected MOSFET, the **gate and drain are shorted**:

VG = VD

The source of **M3** is connected to ground.

| Node | Voltage |
|------|--------|
| VS3 | 0 V |

Using the selected bias point,

| Node | Voltage |
|------|--------|
| VG3 = VD3 | **0.5 V** |

Since this node is directly connected to the **source of M1**, we obtain

| Node | Voltage |
|------|--------|
| VS1 | **0.5 V** |

### Justification

The diode-connected NMOS establishes a stable bias node where  
**VG3 = VD3 = VS1 = 0.5 V**, allowing the circuit to maintain the required current (~200 µA).

---

# DC Gate Bias for M1

To maintain the required drain current in **M1**, the gate–source voltage must satisfy

| Expression | Value |
|-----------|-------|
| VGS1 = VTH + VOV = 0.36 + 0.25 | **0.61 V** |

Since

VS1 = **0.5 V**

the gate voltage becomes

| Expression | Value |
|-----------|-------|
| VG1 = VS1 + VGS1 = 0.5 + 0.61 | **1.11 V** |

Therefore,

**VIN(DC) ≈ 1.11 V**

This bias keeps **M1 operating in saturation**.

---

# Output Voltage Selection

For maximum symmetrical signal swing,

| Calculation | Result |
|-------------|--------|
| VDS ≈ VDD / 2 = 1.5 / 2 | **0.75 V** |

Thus the output voltage is

| Calculation | Result |
|-------------|--------|
| Vout = VDS + VS1 = 0.75 + 0.5 | **≈ 1.25 V** |

This operating point allows adequate output swing while maintaining saturation.

---

# Biasing of PMOS Active Load (M2)

To conduct the required current, the PMOS transistor must satisfy

| Calculation | Result |
|-------------|--------|
| VSG2 = (VTHp + VOV) = 0.39 + 0.25 | **0.64 V** |

Since the source of **M2** is tied to the supply

VS2 = **VDD = 1.5 V**

the gate voltage becomes

| Calculation | Result |
|-------------|--------|
| VG2 = VS2 − VSG2 = 1.5 − 0.64 | **0.86 V** |

## Drain–Source Voltage of M2

Using the calculated output voltage,

| Calculation | Result |
|-------------|--------|
| VSD2 = VS2 − Vout = 1.5 − 1.25 | **0.25 V** |

This ensures the PMOS transistor operates as an **active load**.

---

# Saturation Region Verification

To ensure proper amplifier operation, each transistor must satisfy the **saturation condition**.

| Device | Saturation Condition | Calculated Value | Result |
|------|----------------------|------------------|--------|
| M1 (NMOS) | VDS ≥ VOV | 0.75 ≥ 0.25 | ✔ Saturation |
| M3 (NMOS) | VDS ≥ VOV | 0.50 ≥ 0.25 | ✔ Saturation |
| M2 (PMOS) | VSD ≥ VOV | 0.25 ≥ 0.25 | ✔ Saturation |

### Conclusion

All three transistors **M1, M2, and M3** satisfy the required saturation condition.  
Therefore, the circuit operates correctly with all devices biased in the **saturation region**, which is necessary for proper amplifier operation.

---
# Final DC Operating Point

| VS1 | Vout | VG1 | VG2 | ID | VOV |
|----|----|----|----|----|----|
| 0.5 V | 1.25 V | 1.11 V | 0.86 V | 200 µA | 0.25 V |

The diode-connected NMOS establishes the source voltage of **M1 at approximately 0.5 V**, which sets the proper gate bias and maintains the required drain current. This biasing ensures stable circuit operation while keeping the transistors within their intended operating region.

---
### LTspice Operating Point

<img width="854" height="608" alt="Screenshot 2026-03-10 002522" src="https://github.com/user-attachments/assets/38923257-f0fb-4176-9ef0-379769e01cd3" />

## Width Selection 

The transistor widths were first estimated from the **MOSFET saturation current equation** so that the circuit could achieve the required bias current of **ID ≈ 200 µA**.

| Device | Theoretical Width | Practical Width (Simulation) |
|------|------|------|
| M1 (NMOS – Amplifier) | 5 µm | 19.35 µm |
| M2 (NMOS – Active Load) | 15.95 µm | 60.75 µm |
| M3 (PMOS – Diode Connected Current Source) | 11.83 µm | 41.65 µm |

### Explanation

The theoretical widths provide only an **initial estimate** because practical MOSFET behavior in circuit simulators differs from the ideal equations.

| Practical Effect | Impact on Design |
|------|------|
| Short channel effects | Modify the effective current flowing through the device |
| Device model parameters | Cause deviations from the ideal square-law relation |
| Bias voltage sensitivity | Small voltage changes significantly influence the drain current |

Hence, the transistor widths were **fine-tuned during LTspice simulation** until the circuit produced the required **bias current of approximately 200 µA** while ensuring all transistors remained in the **saturation region for proper amplifier operation**.

---
## Transient Analysis

---
### Input Waveform

<img width="1919" height="858" alt="image" src="https://github.com/user-attachments/assets/659b3249-8413-4694-b17b-0f8213698e04" />

---
### Output Waveform

<img width="1918" height="846" alt="image" src="https://github.com/user-attachments/assets/840720fd-ab82-4028-8f76-82f28955f54e" />

---
### Input & Output

<img width="1907" height="863" alt="image" src="https://github.com/user-attachments/assets/d5fecae2-ae80-4b51-b92e-c300f022c820" />

---
## Practical Gain 

| Vin(p-p) | Vout(p-p) | Gain (Av) | Gain (dB) |
|----------|-----------|-----------|-----------|
| 1.1199 − 1.1002 = **0.0197 V** | 1.3240 − 1.1319 = **0.1921 V** | 0.1921 / 0.0197 = **9.75 V/V** | **19.78 dB** |

---

### Observation

The simulated output signal shows a larger amplitude compared to the input signal, indicating that the circuit provides voltage amplification. The calculated gain is approximately **9.75 V/V (19.78 dB)**, confirming the amplifier behavior of the designed MOSFET stage.

----
# AC Analysis 

<img width="1914" height="877" alt="image" src="https://github.com/user-attachments/assets/e1814d42-5da8-4f15-bcce-8b69637ad894" />

---
---
## Frequency Response Results – Circuit 2C

| Gain (dB) | −3 dB Gain | Bandwidth |
|-----------|------------|-----------|
| 19.73 dB | **16.73 dB** | **662.6 MHz** |

The AC frequency response shows that the amplifier maintains a nearly constant gain in the midband region.  
The gain decreases by **3 dB at approximately 662.6 MHz**, which represents the bandwidth of the amplifier.

---

## Summary

In this experiment, different **MOSFET amplifier configurations** were designed and simulated using **TSMC 180 nm CMOS models in LTspice** with a supply voltage of **1.5 V**.

The following circuits were analyzed:

• **Circuit 2A – Source Degenerated Common Source Amplifier**  
• **Circuit 2B – Cascode Amplifier**  
• **Circuit 2C – Common Source Amplifier with Active Load**

For each circuit, the **DC operating point** was calculated to keep the MOSFETs in the **saturation region**.  
After biasing the circuits, **transient analysis** was used to observe signal amplification and **AC analysis** was performed to determine the gain and bandwidth.

---

## Inference

• The **source-degenerated amplifier (2A)** improves bias stability due to the presence of the source resistor, but this feedback slightly reduces voltage gain.

• The **cascode amplifier (2B)** increases output resistance and improves frequency performance, although the practical gain obtained from simulation is relatively small.

• The **active-load amplifier (2C)** provides better gain because the current-source load replaces a large resistor, which improves voltage amplification.

---

## Conclusion

The experiment demonstrates the effect of different amplifier structures on gain and bandwidth.

The **source-degenerated amplifier** provides stable operation, the **cascode amplifier** improves isolation and output resistance, and the **active-load common source amplifier** achieves higher voltage gain.

The LTspice simulation results are close to the theoretical expectations, confirming the correct design and operation of the MOSFET amplifier circuits.

---

## Performance Comparison of Amplifiers

| Feature | Circuit 2A | Circuit 2B | Circuit 2C |
|--------|-------------|-------------|-------------|
| Amplifier Type | Source Degenerated CS | Cascode Amplifier | CS with Active Load |
| Bias Method | Source resistor feedback | Cascode biasing | Diode-connected NMOS |
| DC Output Level | ≈ 0.95 V | ≈ 1.05 V | ≈ 1.25 V |
| Voltage Gain | ≈ 20.28 dB | ≈ 4.66 dB | ≈ 19.73 dB |
| Bandwidth | ≈ 315 MHz | ≈ 277 MHz | ≈ 662 MHz |
| Stability | High | High | Moderate |
| Design Complexity | Moderate | Higher | Moderate |
