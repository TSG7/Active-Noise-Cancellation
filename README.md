# Active Noise Cancellation System Using Dual Microphones

## Overview
This project implements an **Active Noise Cancellation (ANC) system** using a microcontroller (ESP32) and **dual microphones**.
The system captures audio from a **primary microphone** (containing both speech and noise) and a **reference microphone** (capturing correlated noise). An **adaptive LMS filter** is used to reduce noise while preserving the desired speech signal.

---

## Features
- **Dual-Mic Setup**: Uses a primary microphone for combined speech + noise and a reference microphone for noise estimation.  
- **Adaptive LMS Filtering**: Implements a **Least Mean Squares (LMS) filter** to adaptively estimate and cancel noise.  
- **Voice Activity Detection (VAD)**: Prevents noise cancellation from distorting speech by detecting when speech is present.  
- **High-Pass Filtering**: Reduces low-frequency noise and DC offset for better filter performance.  
- **Real-Time Processing**: Audio is processed in real-time and output via the ESP32 **DAC**.

---

## Hardware Requirements
- **ESP32 Microcontroller**  
- **Primary Microphone** (GPIO34 / ADC1_CHANNEL_6)  
- **Reference Microphone** (GPIO32 / ADC1_CHANNEL_5)  
- **DAC Output** (GPIO25 / DAC_CHANNEL_1)  
- Breadboard and connecting wires  

---

## Software / Libraries
- **Arduino IDE / PlatformIO** for ESP32 development  
- ESP32 ADC & DAC drivers (`driver/adc.h`, `driver/dac.h`)  
- Standard C++ libraries  

---

## How It Works
1. **Audio Acquisition**: Read analog signals from primary and reference microphones.  
2. **Normalization**: Convert ADC readings to the range `[-1.0, 1.0]`.  
3. **High-Pass Filtering**: Removes low-frequency noise.  
4. **Voice Activity Detection (VAD)**: Checks if speech is present using energy threshold.  
5. **LMS Adaptive Filtering**:
   - Computes noise estimate using reference mic and current filter weights.  
   - Updates filter weights using LMS algorithm to adapt to changing noise.  
   - Passes primary input unchanged if speech is detected.  
6. **DAC Output**: Sends processed audio to DAC for analog output.  

---

## Code Highlights
- **Adaptive Filter Parameters**:
  - Filter length: 64 taps  
  - Learning rate: 0.0005  
- **VAD Threshold**: 0.05  
- **Circular buffers** store recent samples for LMS computation.  
- **Error signal** is used as the noise-reduced audio output.  
