# VoiceAssistant-Atom 🎙️

Custom voice assistant firmware for **M5Stack Atom Echo** based on **ESPHome** and **ESP-IDF** framework.

## Project Overview

This project transforms a tiny M5Stack Atom Echo into a fully functional, local voice assistant integrated with Home Assistant. It features a modular configuration designed for stability and high performance on memory-constrained hardware.

### Key Features
* **Local Wake Word**: Powered by `micro_wake_word` (currently on `main` branch: Alexa; working on custom models in `custom-wake-word`).
* **Optimized RAM Management**: Custom `sdkconfig` to handle the 520KB RAM limit of the ESP32-PICO.
* **Media Player Integration**: Supports announcements (e.g., door alerts) while running the voice pipeline.
* **Modular YAML**: Clean separation of audio, LEDs, and voice logic.
* **Security**: Fully integrated with `secrets.yaml` for sensitive credentials.

---

## Hardware 🛠️
* **Device**: [M5Stack Atom Echo](https://shop.m5stack.com/products/atom-echo-smart-speaker-dev-kit)
* **Processor**: ESP32-PICO-D4
* **Framework**: ESP-IDF (Required for high-quality audio processing)

---

## Repository Structure 📂

```text
VoiceAssistant-Atom/
├── atom_echo.yaml        # Main entry point
├── secrets.yaml          # Private credentials (git-ignored)
└── my_echo/              # Component modules
    ├── audio.yaml        # I2S Microphone and Speaker config
    ├── leds.yaml         # SK6812 LED effects (RMT driver)
    └── voice.yaml        # Voice Assistant & Wake Word logic
