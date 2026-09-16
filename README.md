Active Noise Cancellation System Using Dual Microphones
Overview

This project implements a real-time Active Noise Cancellation (ANC) system using an ESP32 microcontroller and dual microphones.

The system uses a primary microphone to capture a combination of speech and background noise, while a reference microphone captures correlated background noise. An adaptive Least Mean Squares (LMS) filter processes these signals to estimate and reduce the unwanted noise while preserving the desired speech signal.

The system is designed for real-time audio processing and outputs the processed signal through the ESP32's built-in DAC.
