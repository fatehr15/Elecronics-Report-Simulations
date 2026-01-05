# RAPPORT Single-Ramp Analog-to-Digital Converter (C1)

## 1. Exercise Objectives

This investigation addresses Exercise N°1 from the Fundamental Electronics II TD Series. The primary objectives include:

- Determining the digital code corresponding to an analog input voltage VA = 0.12V
- Analysing voltage waveforms at critical circuit nodes (points A, B, C, D, and E)
- Validating theoretical predictions through circuit simulation

The converter operates with the following parameters:

- **Resolution:** 8 bits (256 discrete levels)
- **Reference Voltage (Vref):** 8V
- **Comparator Saturation Voltage (Vsat):** 5V
- **Initial Counter State:** Reset to zero (00000000)
- **Target Sample:** VA = 0.12V

## 2. Circuit Description

The single-ramp ADC implements a successive comparison technique, where a digitally controlled staircase voltage is generated and compared against the input analogue sample. The circuit comprises five primary functional blocks:

- **Counter:** Binary counter generating sequential digital codes
- **Digital-to-Analog Converter (DAC):** Converting digital codes to analog reference voltages
- **Comparator:** Determining voltage magnitude relationships
- **Clock Generator:** Providing timing signals
- **Control Logic:** Managing conversion sequencing

## 3. Component Specifications

### 8-Bit Digital-to-Analog Converter DAC0808

The DAC0808 is an 8-bit current-output DAC, configured with an operational amplifier to produce a voltage output. It translates the 8-bit binary value supplied by the counter into a corresponding analog voltage **VE** based on a weighted conversion principle.

- **Resolution:** 8 bits (256 discrete levels)
- **Reference Voltage Range:** ±10 V
- **Output Voltage Range:** 0 to **Vref** (depending on configuration)
- **Supply Voltage:** ±4.5 V to ±18 V
- **Reference Current:** 2 mA

In this setup, **Vref = 8 V**, and the DAC input lines **B1 (MSB)** through **B8 (LSB)** are driven by the counter outputs **Q8 to Q1**, with **Q8** serving as the most significant bit.

### Voltage Comparator LM311

**Role in the Circuit:** The voltage comparator evaluates the analog input voltage VA at the non-inverting terminal (V+) against the DAC-generated voltage VE at the inverting terminal (V−). Based on this comparison, it produces a binary output VB, which is used to control and guide the conversion process.

**Key Specifications:**
- **Supply Voltage:** Operates within a range of 5 V to 36 V
- **Input Offset Voltage:** Typically 2 mV
- **Input Bias Current:** Approximately 100 nA
- **Input Offset Current:** Around 20 nA
- **Common-Mode Rejection Ratio (CMRR):** 100 dB
- **Response Time:** 200 ns
- **Output Voltage Levels:**
  - High Level (Vsat): 5 V via pull-up resistor
  - Low Level: 0 V with the open-collector output pulled to ground
- **Strobe Current:** Up to 150 mA (when used)

### 8-Bit Binary Counter -- CD4020

**Component Overview:** The CD4020 is a CMOS 14-stage binary counter, configured here to operate as an 8-bit counter.

**Function in the Circuit:** It produces a continuous sequence of binary values ranging from 00000000 to 11111111. These outputs are fed directly to the DAC inputs, defining the step-by-step timing and progression of the conversion process.

**Key Electrical Specifications:**
- **Operating Supply Voltage:** 3 V to 18 V
- **Logic Levels (VDD = 5 V):**
  - Logic High (1): VIH ≥ 3.5 V, VOH ≥ 4.95 V
  - Logic Low (0): VIL ≤ 1.5 V, VOL ≤ 0.05 V
- **Maximum Clock Frequency:** 2.5 MHz at 5 V
- **Typical Propagation Delay:** 160 ns
- **Output Current Capability:** 1.5 mA
- **Quiescent Power Consumption:** Approximately 10 µW at 5 V

**Operational Description:**

The counter advances its binary count on every rising edge of the clock signal applied to the CLK input. Activating the R (reset) input asynchronously forces all outputs to a logic-low state. In this configuration, outputs Q1 through Q8 deliver the 8-bit binary sequence required to drive the DAC.

**Timing Parameters:**
- **Minimum Setup Time:** 40 ns
- **Minimum Hold Time:** 20 ns
- **Minimum Reset Pulse Width:** 100 ns

### Logic Gate 74LS08

**Component:** 74LS08 (Quad 2-Input AND Gate, LS-TTL)

**Function in Circuit:** Controls the clock signal sent to the counter. Clock pulses are passed only when the comparator output **VB** is HIGH, stopping the conversion process when **VA < VE**.

**Specifications:**
- **Supply Voltage:** 5 V (±0.25 V)
- **Logic Levels:**
  - Input HIGH (VIH): ≥ 2 V
  - Input LOW (VIL): ≤ 0.8 V
  - Output HIGH (VOH): ≥ 2.7 V
  - Output LOW (VOL): ≤ 0.5 V
- **Propagation Delay:** ~15 ns
- **Power Consumption:** ~4.4 mW per gate
- **Fan-out:** Up to 20 LS-TTL loads

**Operational Principle:** The AND gate combines the system clock with the comparator output **VB**. The counter advances only when **VB = 1**, enabling conditional counting required for the single-ramp ADC operation.

## 4. The Conversion Process

| Step | Counter (Decimal) | Binary Code | VE (V)  | VA − VE (V) | Comparator State (VB) |
|------|-------------------|-------------|---------|-------------|-----------------------|
| 0    | 0                 | 00000000    | 0.0000  | 0.12000     | 5 V                   |
| 1    | 1                 | 00000001    | 0.03125 | 0.08875     | 5 V                   |
| 2    | 2                 | 00000010    | 0.06250 | 0.05750     | 5 V                   |
| 3    | 3                 | 00000011    | 0.09375 | 0.02625     | 5 V                   |
| 4    | 4                 | 00000100    | 0.12500 | −0.00500    | 0 V                   |

## 5. Simulation

**Simulation Tool:** Proteus Design Suite Professional (v8.15)

**Type of Simulation:** Transient analysis incorporating interactive components

### Simulation Waveforms

Figure C.1 shows a composite timing diagram generated using Falstad, depicting the voltage variations at all key nodes (A, B, C, D, and E) throughout the conversion process. A simplified clock waveform was deliberately employed in this simulation to offer a clear and comprehensive visualization of signal interactions and timing relationships during operation.

**Signal Descriptions:**

- **A:** Maintains a constant analog input voltage

![]('./Screenshot 2026-01-05 104609.png')
- **B:** Output of the comparator, responsible for controlling the conversion process

![]('./Screenshot 2026-01-05 104546.png')
- **C:** Clock signal passed through gating logic

![]('./Screenshot 2026-01-05 104658.png')
- **D:** Control signal applied to the AND gate

![]('./Screenshot 2026-01-05 104645.png')
- **E:** Staircase output voltage from the Digital-to-Analog Converter (DAC)

![]('./Screenshot 2026-01-05 104558.png')

