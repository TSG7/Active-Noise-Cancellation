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
How It Works
1. Audio Acquisition

The ESP32 continuously reads analog signals from the two microphones.

Primary microphone → captures speech + background noise.
Reference microphone → captures a correlated representation of the background noise.
2. Signal Normalization

The ADC readings are converted into normalized signal values in the range:

[-1.0, 1.0]

This provides a suitable input range for the subsequent signal-processing operations.

3. High-Pass Filtering

A high-pass filtering stage reduces unwanted low-frequency components and DC offset from the microphone signals.

4. Voice Activity Detection

The system uses Voice Activity Detection (VAD) based on an energy threshold to determine whether speech is present.

When speech is detected, the system avoids unnecessary adaptive filtering that could affect the desired speech signal.

5. LMS Adaptive Filtering

The reference microphone signal is provided to the adaptive LMS filter.

The filter:

Uses the reference signal to estimate the unwanted noise.
Calculates the estimated noise component.
Computes the error signal between the primary signal and estimated noise.
Updates the filter coefficients using the LMS algorithm.
Uses the resulting error signal as the noise-reduced output.

The adaptive nature of LMS allows the filter to continuously adjust to changes in the noise signal.

6. DAC Output

The processed signal is sent to the ESP32 DAC through GPIO25, providing an analog output of the noise-reduced audio signal.
