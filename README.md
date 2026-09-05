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
