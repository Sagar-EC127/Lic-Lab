# Experiment 04  
# Differential Amplifier Analysis

---

## Aim

To design and simulate a MOSFET differential amplifier using LTspice and analyze its performance using DC analysis , transient, and AC analysis.
## Design Specifications (common for all circuits )

| Parameter | Description | Value |
|----------|------------|------|
| VDD | Positive supply voltage | 0.9 V |
| VSS | Negative supply voltage | -0.9 V |
| P | Power constraint | ≤ 2.2 mW |
| \(V_{in,cm}\) | Input common-mode voltage | 0 V |
| \(V_{out,cm}\) | Output common-mode voltage | 0 V |
| \(V_p\) | common source voltage  | -0.7 V |
| L | Channel length | 540 nm |
---

## Circuit Description

The differential amplifier consists of:

- Two NMOS transistors (M1 and M2)
- A constant current source (tail current source)
- PMOS active load or resistive load
- Two input voltages (Vin1 and Vin2)
- Output taken from one or both drains

The circuit operates by comparing two input signals and amplifying their difference.

---

## Introduction

A differential amplifier is a fundamental building block in analog electronics. It amplifies the **difference between two input signals** while rejecting signals that are common to both inputs (called common-mode signals).

This property is known as **Common Mode Rejection**, and it is very important in reducing noise and interference.

MOSFET differential amplifiers are widely used in:
- Operational amplators (Op-Amps)
- Comparators
- Analog signal processing circuits

---

## Working Principle

The operation of the differential amplifier depends on the input conditions:

### 1. When Vin1 = Vin2 (Common Mode Input)
- Both transistors conduct equal current
- Output voltages are equal
- No differential output is produced

### 2. When Vin1 > Vin2
- M1 conducts more current
- M2 conducts less current
- Output at M1 drain decreases
- Output at M2 drain increases

### 3. When Vin2 > Vin1
- Opposite behavior occurs
- Output difference reverses polarity

---

# Circuit Diagram  4a : NMOS Differential Amplifier with Resistive Load

<img width="1163" height="837" alt="Screenshot 2026-03-28 003530" src="https://github.com/user-attachments/assets/a68b9f62-ac32-467c-91b1-890c990887e5" />

# DC Analysis 

## Calculations Table

| Parameter | Equation | Substitution | Value |
|----------|---------|-------------|------|
| Total Current (Itotal) | I = P / V | 2.2 mW / 1.8 V | 1.22 mA |
| ID1 | ID1 = Itotal / 2 | 1.22 mA / 2 | 0.61 mA |
| ID2 | ID2 = Itotal / 2 | 1.22 mA / 2 | 0.61 mA |
| RD | RD = VDD / ID | 0.9 / 0.61 mA | 1.475 kΩ |

### Input Common Mode Range (VCM)

| Parameter     | Formula                  | Calculation              | Value   |
|--------------|--------------------------|--------------------------|---------|
| Vincm(max)   | VDD - (ID × RD) + Vth    | 0.9 - 0.9 + 0.366        | 0.366 V |
| Vincm(min)   | VSS + Vp + VGS           | -0.9 - 0.7 + 0.7         | -0.9 V  |
## Reason for Equal Current Distribution

### Output Common Mode Range (VOCM)

| Parameter     | Formula               | Calculation      | Value  |
|--------------|-----------------------|------------------|--------|
| Vout(max)    | VDD                   | 0.9              | 0.9 V  |
| Vout(min)    | VDD - (ID × RD)       | 0.9 - 0.9        | 0 V    |

When the input common-mode voltage is zero (Vincm = 0), it is defined as:

Vincm = (Vg1 + Vg2) / 2

If Vincm = 0 and no differential input is applied, then:

Vg1 = Vg2 = 0 V  

Since both MOSFETs receive the same gate voltage and are identical:
- VGS1 = VGS2  
- Both transistors operate under identical conditions  

Hence, the tail current splits equally:

ID1 = ID2 = Itotal / 2

This results in equal current distribution in the differential amplifier.

## Saturation Condition Check (NMOS)

| Parameter | Equation | Substitution | Value |
|----------|---------|-------------|------|
| VGS | Vg − Vs | 0 − (−0.7) | 0.7 V |
| VGS − VT | VGS − VT | 0.7 − 0.5 | 0.2 V |
| VDS | Vout − Vs | 0 − (−0.7) | 0.7 V |
| Condition | VDS ≥ VGS − VT | 0.7 ≥ 0.2 | Satisfied ✔️ |

## Width Calculation (NMOS)

| Parameter | Equation | Substitution | Value |
|----------|---------|-------------|------|
| ID | Itotal / 2 | 1.22 mA / 2 | 0.61 mA |
| L | Given | — | 540 nm |
| VGS | Vg − Vs | 0 − (−0.7) | 0.7 V |
| VT | Given | — | 0.366 V |
| Vov | VGS − VT | 0.7 − 0.366 | 0.334 V |
| μnCox | Given | — | 230.3 µA/V² |
| W (Calculated) | (2·ID·L) / (μnCox·Vov²) | (2 × 0.61mA × 540nm) / (230.3µA × 0.334²) | ≈ 25.67 µm |

---

| Type | Width (W) |
|------|----------|
| Calculated | 25.67 µm |
| Practical (LTspice) | 39.03388 µm |
| Observation | Practical value is higher due to second-order effects and accurate device modeling |

## Operating Point

<img width="590" height="550" alt="Screenshot 2026-03-27 230344" src="https://github.com/user-attachments/assets/986fb576-16d7-46b2-bb71-eef4e8913d0a" />

## Transient Analysis

| Parameter | Equation | Substitution | Value |
|----------|---------|-------------|------|
| Vid (10 mV case) | Vin1 − Vin2 | 10 mV − (−10 mV) | 20 mV |
| Vid (250 mV case) | Vin1 − Vin2 | 250 mV − (−250 mV) | 500 mV |
| Vov | VGS − VT | 0.7 − 0.366 | 0.334 V |
| √2 · Vov | 1.414 × Vov | 1.414 × 0.334 | 0.472 V |
| Condition (10 mV) | −√2·Vov ≤ Vid ≤ √2·Vov | −0.472 ≤ 0.02 ≤ 0.472 | Satisfied ✔️ |
| Condition (250 mV) | −√2·Vov ≤ Vid ≤ √2·Vov | −0.472 ≤ 0.5 ≤ 0.472 | Not satisfied ❌ |
| Operation | — | — | Linear (10 mV), Nonlinear (250 mV) |

---

## Explanation

| Case | Behavior |
|------|---------|
| Small Vid (20 mV) | Both transistors ON, current splits equally, linear amplification |
| Large Vid (500 mV) | One transistor ON, other OFF, current steering occurs |


- Small Vid → **Linear region (amplification)**  
- Large Vid → **Nonlinear region (distortion & saturation)**  

 As Vid exceeds √2·Vov, the circuit shifts from **current sharing → current steering**

 ## Differential Input Applied (Vid)

### Linear Region (First Waveform)

| Quantity | Value |
|---------|------|
| Vin1    | +10 mV (approx) |
| Vin2    | -10 mV (approx) |
| Vid = Vin1 - Vin2 | ≈ 20 mV |
| Condition | Vid < √2 · Vov |


<img width="1919" height="879" alt="Screenshot 2026-03-27 235113" src="https://github.com/user-attachments/assets/2aa169fa-f84e-45fd-bfd7-5749ad43240d" />


#### Graph Observation:

- Output is smooth and sinusoidal  
- Vout1 and Vout2 are symmetric  
- No distortion (proper amplification)

---

### Non-Linear Region 

| Quantity | Value |
|---------|------|
| Vin1    | +250 mV (approx) |
| Vin2    | -250 mV (approx) |
| Vid = Vin1 - Vin2 | ≈ 500 mV |
| Condition | Vid > √2 · Vov |


<img width="1915" height="871" alt="Screenshot 2026-03-28 225459" src="https://github.com/user-attachments/assets/00ed5930-93c1-46e9-aaea-1e3b2cc5be40" />

#### Graph Observation:

- Output shows clipping at peaks  
- Waveform is not purely sinusoidal  
- One side dominates (distortion occurs)

## Transient gain 
### Input 

<img width="1919" height="879" alt="Screenshot 2026-03-27 235229" src="https://github.com/user-attachments/assets/d87d85b7-4326-4fea-8493-e4557220b843" />

### output 

<img width="1919" height="904" alt="Screenshot 2026-03-27 235244" src="https://github.com/user-attachments/assets/e3c2f8b0-fd36-4a71-b230-196851223803" />

### Both waveforms (Input and output)

<img width="1919" height="879" alt="Screenshot 2026-03-27 235113" src="https://github.com/user-attachments/assets/56fb7113-892c-41d6-b89f-ee4eb67be034" />

## Transient Gain Calculation

### From Input Waveform (Vin1)

| Parameter | Value |
|----------|------|
| Vmax     | +9.984 mV |
| Vmin     | -9.986 mV |
| Vin(pp)  | 19.97 mV |

---

### From Output Waveform (Vout1)

| Parameter | Value |
|----------|------|
| Vmax     | +61.153 mV |
| Vmin     | -61.131 mV |
| Vout(pp) | 122.28 mV |

---

### Gain Calculation

| Parameter | Formula | Value |
|----------|--------|------|
| Gain (Av) | Vout(pp) / Vin(pp) | 122.28 / 19.97 |
| Gain (Av) | — | ≈ 6.12 |

---

### Gain in dB

| Parameter | Formula | Value |
|----------|--------|------|
| Gain (dB) | 20 log₁₀(Av) | 20 log₁₀(6.12) |
| Gain (dB) | — | ≈ 15.73 dB |

---
# AC Analysis
## Without Capacitor 
<img width="1919" height="906" alt="Screenshot 2026-03-28 222713" src="https://github.com/user-attachments/assets/9dc059e8-c005-47a7-90ef-90b5a0d0b554" />

## With Capacitor 
<img width="1915" height="875" alt="Screenshot 2026-03-28 221137" src="https://github.com/user-attachments/assets/424c736a-865f-4bbb-bc64-f2bb2c0886e5" />

## AC Analysis Comparison (Without Capacitor vs With Capacitor)

## AC Analysis Summary

| Parameter | Without Capacitor | With Capacitor |
|----------|------------------|----------------|
| Midband Gain (Av) | 15.747 dB | 15.747 dB |
| 3 dB Gain | 12.747 dB | 12.747 dB |
| 3 dB Frequency (Bandwidth) | ≈ 5.08 GHz | ≈ 11.5 MHz |

---

## Observation

### Without Capacitor
- Very high bandwidth (GHz range)
- Gain remains constant for large frequency range
- No dominant pole → unrealistic ideal behavior

### With Capacitor
- Bandwidth reduces significantly (MHz range)
- Clear roll-off after cutoff frequency
- Capacitor introduces **dominant pole**

---

## Key Difference

| Parameter | Without Capacitor | With Capacitor |
|----------|------------------|----------------|
| Bandwidth | Very high (GHz) | Limited (MHz) |
| Stability | Less realistic | More practical |
| Frequency response | Flat | Roll-off present |
| Pole effect | Negligible | Dominant pole exists |

---

## Final Conclusion

- Capacitor controls bandwidth and stabilizes the amplifier  
- Without capacitor → unrealistic high-speed response  
- With capacitor → practical amplifier with defined cutoff frequency  

## Theoretical Gain Calculation 

| Step | Parameter | Formula | Value |
|------|----------|--------|------|
| 1 | Vov | VGS - Vth | 0.7 - 0.366 = 0.334 V |
| 2 | gm | 2ID / Vov | (2 × 0.61mA) / 0.334 |
| 3 | gm | — | ≈ 3.65 mS |
| 4 | RD | Given | 1.475 kΩ |
| 5 | Gain (Ad) | gm × RD | 3.65m × 1475 |
| 6 | Gain (Ad) | — | ≈ 5.38 |
| 7 | Gain (dB) | 20 log₁₀(Ad) | 20 log₁₀(5.38) |
| 8 | Theoretical Gain | — | ≈ 14.6 dB |
| 9 | Practical Gain | From AC analysis | 15.747 dB |
| 10 | Difference | Practical - Theoretical | ≈ 1.15 dB |

---

## Final Result

| Quantity | Value |
|---------|------|
| Theoretical Gain | ≈ 14.6 dB |
| Practical Gain | 15.747 dB |
| Conclusion | Practical > Theoretical (due to ro effect) |

## Conclusion

The differential amplifier was successfully designed and analyzed using LTspice.  
The circuit operates properly with both transistors in the **saturation region**, ensuring correct amplification.

The **transient analysis** shows that for small input signals, the output is linear and undistorted, while for larger inputs, distortion occurs due to non-linear operation.

The **AC analysis** gives a midband gain of **15.747 dB** with a defined bandwidth, confirming proper small-signal behavior.

The **theoretical gain (≈ 14.6 dB)** is close to the **practical gain (15.747 dB)**, with a small difference due to non-ideal effects such as output resistance (ro) and parasitics.

Overall, the differential amplifier provides **good amplification, proper biasing, and expected frequency response**, validating the design.


