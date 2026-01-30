# Day 3 – Design and Performance Evaluation of Bandgap Reference and Differential Amplifier
**Cadence Virtuoso**

## Aim of the Experiment
The goal of Day 3 is to design, simulate, and evaluate a Bandgap Reference (BGR) and a Differential Amplifier, with emphasis on:
- Generation of a temperature-stable reference voltage
- Verification of PTAT and CTAT characteristics
- DC temperature sweep validation
- Time-domain (transient) behavior analysis
- Frequency-domain (FFT) evaluation
- Extraction of key performance parameters such as SINAD, SNR, ENOB, and SFDR

## Simulation Environment
The following tools were used throughout the analysis:
- Cadence Virtuoso (Schematic & Layout)
- ADE L / ADE XL for simulation control
- Spectre Simulator for analog simulation
- Calculator & Spectrum Analyzer for data extraction and FFT analysis

## 1.Bandgap Reference Circuit Design
### Overview of the BGR Architecture
<img width="1366" height="768" alt="BGR" src="https://github.com/user-attachments/assets/66e4ed67-30aa-49a6-ba31-12d3ffe8446f" />

The Bandgap Reference circuit is designed to produce a temperature-independent voltage by combining two complementary temperature-dependent components:
- CTAT Voltage: Base-emitter voltage of BJT, which decreases with temperature
- PTAT Voltage: Voltage proportional to absolute temperature, which increases with temperature
- By properly scaling and summing these two voltages, a stable reference voltage of approximately 1.23 V is obtained.

## 2. DC Temperature Sweep Analysis of BGR
### Reference Voltage Variation with Temperature
<img width="1366" height="768" alt="BGR_op1" src="https://github.com/user-attachments/assets/d8084d31-27c3-441c-a233-b8a4cf6adaac" />

A DC sweep is performed over a temperature range of 0 °C to 100 °C to observe the stability of the reference voltage.
### Node Voltage Behavior
<img width="1366" height="768" alt="BGR_op2" src="https://github.com/user-attachments/assets/02563927-17fe-484c-afa8-70dfceb1e46c" />

Internal node voltages are monitored to confirm correct PTAT and CTAT generation and summation.
### Output Voltage Stability
<img width="1366" height="768" alt="BGR_op3" src="https://github.com/user-attachments/assets/6ae35f7a-b6a5-4215-924d-2f593c21de2f" />

The final output voltage remains close to 1.23 V across the temperature range, with only a slight negative slope.
### Key Observations
- CTAT voltage shows a linear decrease with temperature.
- PTAT voltage shows a linear increase with temperature.
- Proper cancellation results in a nearly constant reference voltage.

## 3. Analysis of PTAT Voltage Characteristics
The PTAT voltage increases steadily with temperature, confirming correct proportional behavior.
### Measured PTAT Values
Temperature (°C)
PTAT Voltage (V)
<img width="1366" height="768" alt="calculator data" src="https://github.com/user-attachments/assets/a31f2df6-962e-42ce-be45-e9b165ce3e92" />

### Inference
PTAT slope ≈ 0.4 mV per 100 °C
Confirms accurate PTAT generation using device mismatch and resistor scaling.

## 4. Temperature Coefficient Evaluation (Vref in ppm)
### Vref ppm Analysis
<img width="1366" height="768" alt="calculator" src="https://github.com/user-attachments/assets/3c5e0d01-e82e-45b3-bfda-fd7f89b2a4e0" />

The temperature coefficient of the reference voltage is calculated and plotted in parts per million (ppm).
### Observations
- Temperature coefficient ≈ −59 to −62 ppm/°C.
- Indicates good first-order temperature compensation.
- Minor trimming or curvature correction can further improve performance.

## Frequency Domain Analysis Using FFT
### FFT of Differential Input
<img width="1366" height="768" alt="diff_spect1" src="https://github.com/user-attachments/assets/bc6b7e6c-2d88-428e-903f-a5aeac192fc4" />

The FFT of the input signal shows a low-amplitude signal with limited spectral purity.
### FFT of Differential Output
<img width="1366" height="768" alt="diff_spect2" src="https://github.com/user-attachments/assets/edb47155-f5f9-4d1e-9d5a-9ccca2fbf402" />

The output FFT indicates amplification but is still dominated by noise components.
### Noise Spectrum
<img width="1366" height="768" alt="diff_spect3" src="https://github.com/user-attachments/assets/f58304f8-5c00-4bbf-8aae-92103f462f78" />

The noise spectrum highlights a relatively high noise floor compared to signal amplitude.

## 7. Extracted FFT Performance Metrics
The following values are directly obtained from the ADE Spectrum “Outputs” panel
### Differential Input (Din1)
ENOB: −1.8559 bits
SINAD: −9.4126 dB
SNR: −9.4126 dB
SFDR: 0.0895 dBc
#### Inference: Input signal is extremely weak and noise-dominated.

### Differential Output (Dout) – Case 1
SINAD: −6.1596 dB
SNR: −6.1596 dB
SFDR: 0.6834 dBc
THD: 0 %
#### Inference: Slight improvement over input, but overall performance remains noise-limited.

### Differential Output Power Analysis – Case 2
Signal Power: −101.77 dB
DC Power: −58.37 dB
Noise Floor: −102.36 dB
Integrated Noise: −118.89 dB

### Differential Output Power Analysis – Case 3
Signal Power: −122.71 dB
DC Power: −28.70 dB
Noise Floor: −126.55 dB
Integrated Noise: −143.09 dB

## 8. Key Insights from the Experiment
- Bandgap Reference successfully generates a stable ~1.23 V reference
- PTAT and CTAT components effectively cancel temperature dependency
- Temperature coefficient is within acceptable range for basic BGR design
- Differential amplifier operates correctly in time domain
- FFT results indicate noise-dominated performance, suggesting:
- Insufficient signal amplitude
- Need for higher gain
- Improved biasing and filtering required
## Overall Conclusion (Day 3)
Day 3 successfully demonstrates the design, simulation, and validation of a Bandgap Reference and Differential Amplifier. While the BGR shows good temperature stability, FFT analysis of the differential amplifier highlights opportunities for optimization in gain, noise reduction, and biasing for improved dynamic performance.

