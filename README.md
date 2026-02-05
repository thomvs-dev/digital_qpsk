# QPSK Signal Generation and Demodulation in MATLAB/Simulink

## 1. Overview

This Simulink model demonstrates the **generation, modulation, and demodulation of a Quadrature Phase Shift Keying (QPSK) signal** using basic signal processing blocks. The objective of the model is to provide an intuitive understanding of how digital data bits are mapped onto in-phase (I) and quadrature (Q) carrier components, combined to form a QPSK waveform, and subsequently recovered at the receiver.

The model is designed for **educational clarity**, explicitly showing:

* Bit stream generation
* Bit grouping and separation into I/Q paths
* Carrier modulation
* Signal summation (QPSK waveform formation)
* Coherent demodulation of I and Q components

---

## 2. Theory Background (QPSK in Brief)

Quadrature Phase Shift Keying (QPSK) is a digital modulation scheme where **two bits are transmitted per symbol** by selecting one of four possible carrier phase states:

[
\theta \in {45^\circ, 135^\circ, 225^\circ, 315^\circ}
]

The transmitted signal can be expressed as:

[
s(t) = I(t)\cos(2\pi f_c t) - Q(t)\sin(2\pi f_c t)
]

where:

* (I(t)) and (Q(t)) take values (\pm 1)
* (f_c) is the carrier frequency

This orthogonal decomposition allows QPSK to **double spectral efficiency** compared to BPSK.

---

## 3. Model Structure and Signal Flow

### 3.1 Random Data Generation

* **Random Integer Generator**
  Generates a stream of random integers representing digital data symbols.

* **Integer-to-Bit Converter**
  Converts integer values into a binary bit stream suitable for digital modulation.

---

### 3.2 Bit Separation (Even/Odd Bits)

* The binary stream is split into:

  * **Odd bits → In-phase (I) path**
  * **Even bits → Quadrature (Q) path**

This grouping reflects the fundamental QPSK principle of **two bits per symbol**.

---

### 3.3 Symbol Mapping (±1 Levels)

* Logical bits are mapped to bipolar values:

  * `0 → -1`
  * `1 → +1`

This is implemented using:

* Constant blocks (`+1`, `-1`)
* Product blocks
* Switch blocks controlled by bit values

This step converts digital data into **baseband symbol waveforms**.

---

## 4. Carrier Generation and Modulation

### 4.1 Carrier Signals

* **Sine Wave blocks** generate:

  * (\cos(2\pi f_c t)) → In-phase carrier
  * (\sin(2\pi f_c t)) → Quadrature carrier

These carriers are **orthogonal**, ensuring independent transmission of I and Q components.

---

### 4.2 I/Q Modulation

* The bipolar I data multiplies the cosine carrier
* The bipolar Q data multiplies the sine carrier

Mathematically:
[
I(t)\cos(2\pi f_c t), \quad Q(t)\sin(2\pi f_c t)
]

---

### 4.3 QPSK Signal Formation

* The I and Q modulated signals are **summed** to produce the final QPSK waveform.

This waveform exhibits:

* Constant envelope
* Phase transitions of 90° or 180°
* Higher data rate than BPSK for the same bandwidth

---

## 5. Receiver and Demodulation

### 5.1 Coherent Demodulation

At the receiver:

* The QPSK signal is multiplied by locally generated cosine and sine carriers
* This extracts the baseband I and Q components

### 5.2 Low-Pass Filtering and Decision

* The demodulated outputs are passed through decision logic to recover:

  * In-phase bit stream
  * Quadrature bit stream

These are then recombined to reconstruct the transmitted data bits.

---

## 6. Scope Outputs and Observations

The scopes display:

1. **Input digital data (integer and bit-level)**
2. **Odd and even bit streams**
3. **In-phase carrier-modulated signal**
4. **Quadrature carrier-modulated signal**
5. **Composite QPSK waveform**
6. **Recovered I and Q bit streams at the receiver**

Key observations:

* Phase changes correspond to bit transitions
* I and Q components remain orthogonal
* Correct symbol recovery requires carrier phase synchronization

<img width="1920" height="1061" alt="image" src="https://github.com/user-attachments/assets/75660824-3555-4707-b479-f57f48d2174a" />
<img width="1920" height="1053" alt="image" src="https://github.com/user-attachments/assets/e75e6217-7cf1-4b90-8efa-7ae40042571f" />

---



## 7. Educational Objectives

This model helps users understand:

* How digital bits map to QPSK symbols
* Why I/Q modulation enables higher spectral efficiency
* The role of carrier orthogonality
* The importance of coherent detection
* The relationship between time-domain waveforms and modulation theory

---

## 8. Extensions and Experiments

Suggested extensions:

* Add **AWGN channel** to observe BER performance
* Implement **root-raised cosine filtering**
* Replace manual blocks with **built-in QPSK Modulator**
* Extend to **16-QAM**
* Measure **constellation diagrams and EVM**

---
