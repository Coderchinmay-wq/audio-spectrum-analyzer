# 🎵 Analog Audio Spectrum Display

An analog audio spectrum display system designed and implemented using an electret microphone, NE5532 pre-amplifier, TL074 active band-pass filters, LM324 peak detectors, and an LM3915 LED bar-graph driver.

The system captures ambient sound, amplifies the weak microphone signal, separates the audio into three frequency bands, detects the signal amplitude of each band, and displays the corresponding signal strength using LED bar graphs.

---

## 📌 Project Overview

Audio signals contain components at different frequencies.

This project implements an analog signal-processing chain that separates an incoming audio signal into three frequency bands and displays the amplitude of each band using an LED bar graph.

The complete signal chain is:

```text
Sound Pressure
      ↓
Electret Microphone
      ↓
NE5532 Pre-Amplifier
      ↓
TL074 Active Band-Pass Filters
      ↓
LM324 Peak Detector
      ↓
LM3915 LED Driver
      ↓
LED Bar Display

```
The project demonstrates practical applications of:

- perational amplifiers
- Signal conditioning
- Active filters
- AC-to-DC conversion
- Peak detection
- Analog signal processing
- LED level indication

## 🎯 Objectives
- Capture ambient audio using an electret microphone.
- Amplify the low-level microphone signal.
- Separate the audio signal into different frequency bands.
- Detect the amplitude of each filtered signal.
- Convert the filtered AC signal into a DC level.
- Display signal strength using an LED bar graph.
- Implement and verify the complete circuit using real hardware.

## 🧠 System Architecture
                    ┌──────────────────────┐
                    │    Sound Pressure    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Electret Microphone  │
                    │    Sensor Block      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ NE5532 Pre-Amplifier │
                    │   Gain = 19          │
                    └──────────┬───────────┘
                               │
                               ▼
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐         ┌─────────────────┐
        │ TL074 Active    │         │ Frequency       │
        │ Band-Pass       │         │ Separation      │
        │ Filters         │         │                 │
        └────────┬────────┘         └─────────────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ LM324 Peak      │
        │ Detector        │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ LM3915 LED      │
        │ Driver          │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ LED Bar Graph   │
        │ Display         │
        └─────────────────┘

## 🔧 Hardware Used
| Component           | Function                              |
| ------------------- | ------------------------------------- |
| Electret Microphone | Converts sound into electrical signal |
| NE5532              | Microphone pre-amplification          |
| TL074               | Active band-pass filtering            |
| LM324               | Precision peak detection              |
| LM3915N             | Logarithmic LED level driver          |
| Diodes              | Rectification in peak detector        |
| Capacitors          | Coupling, filtering and peak holding  |
| Resistors           | Biasing, gain and filter networks     |
| LED Bar Graph       | Visual signal-level indication        |
| ±12 V Supply        | Analog circuit power supply           |

## 🎤 1. Electret Microphone

The electret microphone converts acoustic pressure into a small AC electrical signal.

Because the microphone produces only a few millivolts of signal, the output requires amplification before further signal processing.

### Microphone Bias

The microphone is biased using: Bias resistor = 2.2 kΩ

A coupling capacitor is then used to transfer the AC audio signal while blocking the DC component.
```
Electret Microphone
        │
        │
   2.2 kΩ Bias
        │
        ▼
   Coupling Capacitor
        │
        ▼
   NE5532 Amplifier
```
## 🔊 2. NE5532 Pre-Amplifier

The weak microphone signal is amplified using an NE5532 operational amplifier.

A non-inverting amplifier configuration is used.

### Design Values

Rf = 180 kΩ, 

R1 = 10 kΩ

The voltage gain is:

$$ A_v = 1 + \frac{R_f}{R_1} $$

Therefore:

$$ A_v = 1 + \frac{180k}{10k} $$ 

$$ A_v = 19 $$

Pre-Amplifier Gain

Gain = 19

The amplified waveform was verified using a CRO during hardware testing.

## 🎚️ 3. Active Band-Pass Filters

The amplified audio signal is passed through active band-pass filters implemented using the TL074 operational amplifier.

The filter stage provides an additional gain of:

Filter Gain = 2

The audio spectrum is divided into three frequency bands.
| Band   | Frequency Range |
| ------ | --------------: |
| Band 1 | 250 Hz – 800 Hz |
| Band 2 |  800 Hz – 3 kHz |
| Band 3 |  3 kHz – 16 kHz |

These bands allow the system to distinguish low, mid and high-frequency components of an audio signal.
📈 4. Overall System Gain

The pre-amplifier provides a gain of 19.

The filter stage provides an additional gain of 2.

Therefore:

$$ A_{total} = A_{preamp} \times A_{filter} $$ 

$$ A_{total} = 19 \times 2 $$ 

$$ \boxed{A_{total} = 38} $$

The overall system gain is approximately:

38

## ⚡ 5. LM324 Peak Detector

The output of each band-pass filter is an AC signal.

The LM324 peak detector converts this filtered AC signal into a DC voltage proportional to the signal amplitude.

Peak Detector Components
LM324
Diode
Capacitor

The LM324 is used as a precision rectifier.

This compensates for the diode's forward voltage drop and allows more accurate detection of low-level audio signals.

The capacitor provides peak holding, which helps reduce rapid fluctuations and LED flickering.

### Signal Conversion
```
Filtered AC Signal
        ↓
Precision Rectification
        ↓
Peak Detection
        ↓
DC Voltage
```
## 💡 6. LM3915 LED Display Driver

The detected DC voltage is applied to the LM3915N LED driver.

The LM3915 converts the input voltage into a logarithmic LED level indication.
```
Peak Detector
      │
      ▼
  DC Voltage
      │
      ▼
   LM3915N
      │
      ▼
 LED Bar Graph
```
The number of illuminated LEDs represents the signal strength.

Higher audio amplitude results in a higher LED level.

## 🔌 Power Supply

The analog circuit uses a bipolar supply:
```
+12 V
  │
  │
 GND
  │
  │
-12 V
```
The bipolar supply is used for the op-amp based analog signal-processing stages.

## 🧪 Hardware Verification

The circuit was verified stage-by-stage.

### Observation 1 — Microphone

Expected:

Small AC microphone signal

Result:

Microphone signal observed on CRO

### Observation 2 — Pre-Amplifier

Expected:

Gain = 19

Result:

Amplified waveform observed
Gain verified

### Observation 3 — Filter

Expected:

Filter gain = 2

Result:

Filtered output observed
Frequency-band separation confirmed

### Observation 4 — Peak Detector

Expected:

DC output proportional to signal amplitude

Result:

Pulsating DC output observed
Peak detector functioning correctly

### Observation 5 — LED Display

Expected:

LED response proportional to signal amplitude

Result:

LEDs illuminated according to signal amplitude
LM3915 driver verified

## 📊 Design Parameters

| Parameter                |               Value |
| ------------------------ | ------------------: |
| Microphone Bias Resistor |              2.2 kΩ |
| Coupling Capacitor       |        1 µF / 100 V |
| Pre-Amplifier IC         |              NE5532 |
| Pre-Amplifier Gain       |                  19 |
| Feedback Resistor        |              180 kΩ |
| Input Resistor           |               10 kΩ |
| Filter IC                |               TL074 |
| Filter Gain              |                   2 |
| Band 1                   |     250 Hz – 800 Hz |
| Band 2                   |      800 Hz – 3 kHz |
| Band 3                   |      3 kHz – 16 kHz |
| Peak Detector            |               LM324 |
| Display Driver           |             LM3915N |
| Supply                   | +12 V / 0 V / -12 V |
| Overall Gain             |                  38 |

## 📷 Hardware Documentation
### Peak Detector

The peak detector uses an LM324, diode and capacitor to convert the filtered AC signal into a DC level.

### LM3915 LED Display

The LM3915N drives the LED bar graph according to the detected audio signal level.

### Circuit Diagram

### PCB Design

## 🧩 Signal Processing Blocks

The project implements the following blocks of an analog signal-processing chain:
```
┌───────────────┐
│ Sensor Block  │
│ Electret Mic  │
└───────┬───────┘
        ↓
┌──────────────────────┐
│ Signal Conditioning  │
│ NE5532 Pre-Amplifier │
└──────────┬───────────┘
           ↓
┌─────────────────────┐
│ Signal Processing   │
│ TL074 Band-Pass     │
│ Filters             │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Detection Block     │
│ LM324 Peak Detector │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Display Block       │
│ LM3915 + LED Bar    │
└─────────────────────┘
```
## 📚 Key Concepts Demonstrated

Linear Integrated Circuits

Operational Amplifier Applications

Electret Microphone Interfacing

Signal Conditioning

Non-Inverting Amplifier

Voltage Gain

Active Band-Pass Filters

Frequency Separation

Precision Rectifier

Peak Detection

AC-to-DC Conversion

Peak Holding

LED Level Indication

LM3915 Logarithmic Display

Analog Signal Processing

Hardware Debugging

CRO-Based Signal Verification

## 🛠️ Practical Design Challenges

1. Low-Level Microphone Signal

The microphone generates only a few millivolts, requiring a sufficiently high-gain but stable pre-amplifier.

2. Noise

Low-level analog signals are susceptible to environmental and electrical noise.

3. Frequency Separation

The active filters must provide appropriate frequency separation between the three bands.

4. Peak Detection

The peak detector must accurately follow the amplitude of the filtered audio signal.

5. LED Stability

The peak-hold capacitor helps prevent excessive LED flickering.

## 🚀 Future Improvements

### Possible improvements include:

Increase the number of frequency bands.

Add more LED bars for finer resolution.

Design higher-order filters for sharper frequency separation.

Add adjustable frequency bands.

Improve PCB grounding and signal routing.

Add an OLED/LCD display.

Add a microcontroller or FPGA for digital spectrum visualization.

Implement FFT-based digital spectrum analysis.

Add USB/serial data logging.

Compare analog spectrum analysis with digital FFT results.

## 🎓 Academic Context

Course: Linear Integrated Circuits (LIC)

Project: Audio Spectrum Display

Domain: Analog Electronics / Signal Processing

Implementation: Hardware

## 👨‍💻 Author

Chinmay N. Yalawatti

Electronics & Communication Engineering

## 📄 Documentation

The complete project report is available in the report/ directory.

## ⭐ Project Highlights

🎤 Electret microphone audio capture

🔊 NE5532 low-level signal amplification

🎚️ TL074 three-band active filtering

⚡ LM324 precision peak detection

💡 LM3915 logarithmic LED level display

🧪 Real hardware implementation and verification

📈 Approximately 38× overall signal gain

## 📜 License

This project is intended for educational and academic purposes.
