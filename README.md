Active Noise Cancellation System Using Dual Microphones
Overview

This project implements a real-time Active Noise Cancellation (ANC) system using an ESP32 microcontroller and dual microphones.

The system uses a primary microphone to capture a combination of speech and background noise, while a reference microphone captures correlated background noise. An adaptive Least Mean Squares (LMS) filter processes these signals to estimate and reduce the unwanted noise while preserving the desired speech signal.

The system is designed for real-time audio processing and outputs the processed signal through the ESP32's built-in DAC.
Features
Dual-Microphone Setup: Uses a primary microphone to capture speech and noise, and a reference microphone to capture correlated noise.
Adaptive LMS Filtering: Uses a Least Mean Squares (LMS) adaptive filter to estimate and reduce unwanted noise.
Voice Activity Detection (VAD): Detects speech activity to help prevent excessive filtering and speech distortion.
High-Pass Filtering: Reduces low-frequency noise and DC offset before adaptive filtering.
Real-Time Processing: Processes microphone signals continuously and produces the noise-reduced output in real time.
ESP32 DAC Output: Sends the processed audio signal through the ESP32 DAC for analog output.
Hardware Requirements
ESP32 Microcontroller
Primary Microphone
GPIO34 / ADC1_CHANNEL_6
Reference Microphone
GPIO32 / ADC1_CHANNEL_5
DAC Output
GPIO25 / DAC_CHANNEL_1
Breadboard
Connecting wires
Software / Libraries
Arduino IDE or PlatformIO
ESP32 ADC and DAC drivers
driver/adc.h
driver/dac.h
Standard C++ libraries
System Architecture
                ┌─────────────────────┐
                │   Primary Microphone│
                │   Speech + Noise    │
                └──────────┬──────────┘
                           │
                           ▼
                    ┌──────────────┐
                    │ Preprocessing│
                    │ Normalization│
                    │ High-Pass    │
                    └──────┬───────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   LMS Adaptive      │
                │      Filter         │◄──────────┐
                └──────────┬──────────┘           │
                           │                      │
                           ▼                      │
                    ┌──────────────┐              │
                    │ Noise Reduced│              │
                    │    Signal    │              │
                    └──────┬───────┘              │
                           │                      │
                           ▼                      │
                    ┌──────────────┐              │
                    │  ESP32 DAC   │              │
                    └──────────────┘              │
                                                  │
                ┌─────────────────────┐           │
                │ Reference Microphone│           │
                │   Correlated Noise  │───────────┘
                └─────────────────────┘  
