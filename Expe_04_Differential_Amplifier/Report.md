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
