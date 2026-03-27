# Experiment 04  
# Differential Amplifier Analysis

---

## Aim

To design and simulate a MOSFET differential amplifier using LTspice and analyze its performance using DC analysis , transient, and AC analysis.
## Design Specifications

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
| Vincm(max) | VDD - (ID × RD) + Vth | 0.9 - 0.9 + 0.366 | 0.366 V |
| Vincm(min) | VSS + Vp + VGS | -0.9 - 0.7 + 0.7 | -0.9 V |
| Vout(max) | VDD | 0.9 | 0.9 V |
| Vout(min) | VDD - (ID × RD) | 0.9 - 0.9 | 0 V |

## Reason for Equal Current Distribution

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

### Key Point

- Small Vid → **Linear region (amplification)**  
- Large Vid → **Nonlinear region (distortion & saturation)**  

✔️ As Vid exceeds √2·Vov, the circuit shifts from **current sharing → current steering**
