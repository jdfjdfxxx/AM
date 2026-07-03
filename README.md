# High-Performance Low-Power AM Transmitter System

An industrial-grade, highly optimized Low-Power Amplitude Modulation (AM) Transmitter engineering project. This system integrates digital controls, precision frequency synthesis, multi-stage small-signal amplification, high-performance balanced modulation, and a broadband RF power amplifier stage. Designed and simulated comprehensively in **NI Multisim**, achieving exceptional flat-gain profiles and strict impedance matching over high-frequency spectrums.

---

## 🛠️ Key Technical Specifications & Simulation Results

Based on empirical curves and rigorous transient analyses executed across individual sub-modules, the complete system exhibits the following validated RF parameters:

*   **AC Frequency Response**: Exceptionally stable and flat within the **$50\text{MHz} \sim 400\text{MHz}$** ultra-broadband range.
*   **Voltage Gain Flatness**: Achieves a highly uniform voltage gain constrained strictly between **$14.2\text{dB} \sim 14.8\text{dB}$**, demonstrating a maximum ripple of only $\pm0.3\text{dB}$.
*   **Impedance Matching & Port VSWR**: 
    *   **Input Return Loss ($S_{11}$)**: Better than **$-12\text{dB}$** in the $100\text{MHz} \sim 500\text{MHz}$ window, ensuring near-perfect source-to-stage power transfer.
    *   **Output Return Loss ($S_{22}$)**: Better than **$-10\text{dB}$**, matching seamlessly to standard $50\,\Omega$ RF transmission lines/instruments.
*   **Power Delivery**: The output $1\text{dB}$ Compression Point ($P_{1\text{dB}}$) reaches approximately **$+18\text{dBm}$**, optimizing the AH101 driver matrix for medium-power linearity.
*   **Spectral Purity**: 
    *   2nd Harmonic Suppression: **$-35\text{dBc}$**
    *   3rd Harmonic Suppression: **$-42\text{dBc}$**
    *   Delivers highly efficient wideband small-signal linear amplification with minimal intermodulation distortions.

---

## 📐 System Architecture & Module Breakdown

The complete end-to-end system architecture is partitioned into encapsulated sub-blocks for structural signal fidelity:

### 1. Carrier & Digital Synthesis Stage (DDS Core)
*   **Hardware Architecture**: Controlled via an **STM32 MCU** processing digital control words dynamically transferred over high-speed **SPI**.
*   **Synthesis Engine**: Utilizes the **AD9833** Direct Digital Synthesis (DDS) architecture to output pristine, agile carrier sine waves. The user interface handles on-the-fly frequency stepping via hardware debounced buttons and drives real-time display telemetry via digital nixie-tube matrices.

### 2. Double-Balanced AM Modulation Block
*   **Core Driver**: Built around the industry-proven **MC1496** Balanced Modulator/Demodulator integrated circuit.
*   **Mechanism**: Configured in a fully symmetric double-balanced differential amplifier topology. By applying the baseband signal and the amplified DDS carrier to its respective internal differential quadrants, it suppresses the carrier dynamically to yield highly accurate Double-Sideband Suppressed Carrier (DSB-SC) or Full AM signals depending on bias resistor provisioning.

### 3. Pre-Amplifier & Signal Conditioning Stage
*   **Circuit Topology**: Discrete common-emitter amplifier network utilizing twin **S9018 Ultra-High Frequency (UHF) NPN Silicon Transistors**.
*   **Purpose**: The S9018 features a high transition frequency ($f_T \approx 1.1\text{GHz}$), making it ideal for restoring and stepping up the raw voltage output from the modulation node to feed the input impedance boundary of the subsequent power stage without entering saturation.

### 4. RF Power Amplification Network (PA Stage)
*   **Core Component**: Integrated **AH101** GaAs MMIC True-Broadband Medium-Power Amplifier chip module.
*   **Matching & Bias**: Deployed with custom-calculated multi-element LC networks to establish rigorous $50\,\Omega$ characteristic port matching. It boosts the modulated AM stream to high energy density levels, empowering robust, distortion-free wireless transmission over the specified medium.

### 5. Multi-Rail Linear Regulated Power Supply
*   **Design**: Features independent linear regulation pathways driven by **LM317** (Adjustable Positive), **LM337** (Adjustable Negative), and **LM7805** (Fixed +5V) to deliver ultra-low noise, high-rejection DC rails to the high-gain analog frontends, eliminating power-grid ripple modulations.

---

## 📈 Multi-Domain Simulation Verification

Simulation testbenches executed in **NI Multisim** validate the execution profiles across individual milestones:

1.  **Modulation Envelope Fidelity**: The simulated time-domain oscilloscope plots exhibit perfectly symmetrical, crisp AM envelopes without phase reversal or cross-over clipping, matching theoretical modulation indexes ($m \le 1$).
2.  **Carrier Purity**: Transient analysis profiles present stable time-base sinusoidal structures at chosen frequency targets, proving the spectral consistency of the pre-driver and conditioning nodes.

---

## 📂 Repository Structure Recommendation

To cleanly host this project on your profile, organize your files as follows:

```text
├── docs/                      # Technical reports, datasheets, and schematic printouts
│   └── Lab_Report_Final.pdf   # Complete course design specification manual
├── firmware/                  # Embedded software directory
│   ├── Core/                  # STM32 driver scripts, SPI setup, and AD9833 registers
│   └── main.c                 # Primary system execution loop
├── simulation/                # Computer-Aided Engineering files
│   ├── Full_System_AM.ms14    # Complete Multisim 14.0 schematic blueprint file
│   └── sub_modules/           # Sectioned schematics (Power, Modulator, PA)
└── README.md                  # Front-facing documentation index


📚 References & Academic Foundation
The architectural design rules and engineering methodologies applied across this framework are rooted in established electronic paradigms:
Kang Huaguang. Fundamentals of Electronic Technology (Analog Part) [M]. 6th Edition. Beijing: Higher Education Press, 2013.
Hu Shunu. Analog Electronic Technology Foundation [M]. 4th Edition. Beijing: Higher Education Press, 2011.
Sedra A S, Smith K C. Microelectronic Circuits [M]. 7th Edition. New York: Oxford University Press, 2015.
Nanjing Semiconductor Device Factory. S9018 NPN High-Frequency Small-Signal Transistor Datasheet [R]. Nanjing, 2012.
Zhang Suxia. High-Frequency Electronic Circuits [M]. 6th Edition. Beijing: Higher Education Press, 2023.
Li Xiaofeng et al. Principles of Communications [M]. 2nd Edition. Beijing: Tsinghua University Press, 2014.
Texas Instruments. MC1496 Balanced Modulator-Demodulator Datasheet [R]. Texas Instruments Incorporated, 2016.
National Instruments. Multisim 14 User Manual [R]. National Instruments Corporation, 2017.
