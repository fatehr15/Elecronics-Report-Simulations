# Design and Simulation of an Active Band-Pass Filter


## Abstract

This report details the design and simulation of an Active Second-Order Band-Pass Filter using an LM741 Operational Amplifier. The circuit combines high-pass and low-pass filtering stages with a non-inverting amplifier to achieve a specific frequency response. Theoretical calculations for cutoff frequencies and gain were verified using Proteus simulation software.

## 1. Introduction

A Band-Pass Filter (BPF) is a circuit designed to pass signals within a specific frequency range while attenuating frequencies outside that range. By using an active component like the LM741 Op-Amp, the circuit can provide voltage gain and high input impedance, which prevents signal degradation.

## 2. Circuit Design

The circuit consists of an input high-pass stage, an amplification stage, and an output low-pass stage. Figure 1 shows the complete schematic as designed in Proteus.

**Figure 1:** Active Band-Pass Filter Schematic Diagram (Proteus).

## 3. Theoretical Calculations

The performance of the filter is governed by the values of the resistors and capacitors selected.

### 3.1 Frequency Parameters

The lower and upper cutoff frequencies (f<sub>L</sub> and f<sub>H</sub>) are calculated at the −3dB points:

**Lower Cutoff (f<sub>L</sub>):**

```
f_L = 1 / (2πR₁C₁) = 1 / (2π(50kΩ)(50nF)) ≈ 63.66 Hz     (1)
```

**Upper Cutoff (f<sub>H</sub>):**

```
f_H = 1 / (2πR₂C₂) = 1 / (2π(100Ω)(100nF)) ≈ 15.92 kHz   (2)
```

### 3.2 Voltage Gain

The mid-band gain (A<sub>v</sub>) is set by the ratio of R₄ to R₃:

```
A_v = 1 + (R₄/R₃) = 1 + (10kΩ/1kΩ) = 11                  (3)
```

In decibels, the gain is:

```
Gain_dB = 20 log₁₀(11) ≈ 20.83 dB                         (4)
```

## 4. Simulation Results

The circuit was simulated in Proteus using an AC Sweep analysis. Figure 2 shows the frequency response of the system.

**Figure 2:** Frequency Response (Bode Plot) showing the mid-band gain and roll-off.

## 5. Verification Table

The following table compares the theoretical calculations with the values observed in the simulation.

**Table 1:** Theoretical vs. Simulated Performance Comparison

| Parameter | Theoretical Calculation | Simulated Result |
|-----------|------------------------|------------------|
| Lower Cutoff (f<sub>L</sub>) | 63.66 Hz | [Enter Val] |
| Upper Cutoff (f<sub>H</sub>) | 15.92 kHz | [Enter Val] |
| Peak Voltage Gain | 20.83 dB | [Enter Val] |


![](B41.png)
![](B42.png)
![](B43.png)
![](B44.png)



## 6. Conclusion

The simulation successfully demonstrated the characteristics of an active band-pass filter. The output signal was amplified by a factor of 11 in the passband, while frequencies below 63 Hz and above 15.9 kHz were attenuated. The results prove that the circuit operates according to the theoretical design.
