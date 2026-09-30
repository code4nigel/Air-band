# Air Band - Computer Vision Virtual Instrument System
> **A marker-less virtual music studio turning standard webcams into playable instruments.**

[![Python](https://img.shields.io/badge/Python-3.9%20%7C%203.10-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?logo=opencv&logoColor=white)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Hand%20Tracking-0097A7)](https://developers.google.com/mediapipe)
[![Pygame](https://img.shields.io/badge/Pygame-Audio%20Engine-brightgreen)](https://www.pygame.org/)
[![Patent Status](https://img.shields.io/badge/Indian%20Patent-Published-gold)](https://ipindiaservices.gov.in/)

---

## Official Patent Publication

This project has been officially published as an Indian Patent by the Patent Office:

| Detail | Information |
| :--- | :--- |
| **Title of Invention** | **MUSICAL TRAINING AND INTERACTION DEVICE** |
| **Application Number** | `202621021424 A` |
| **Journal Publication** | **The Patent Office Journal No. 15/2026** (Dated: 10/04/2026) |
| **Applicant** | Lakshmi Narain College of Technology Excellence (LNCTE), Bhopal |
| **Inventors** | Shivanshu Yadav, Uday Singh Prajapati, Vishal Kumar Gupta, Prof. Anju Taiwade, Dr. Kirti Verma |

---

## Overview

Traditional musical instruments are expensive, bulky, and difficult to practice in noise-restricted or shared home environments. 

**Air Band** abstracts musical hardware into intelligent software. Using a standard laptop RGB webcam with zero external sensors or physical gloves, Air Band tracks 21 skeletal hand landmarks in real time to simulate playing physical instruments with sub-50ms latency.

---

## Features & Instruments

### 1. Virtual Polyphonic Guitar
- **Dual-Hand Coordination:** Left hand handles chord fretting by detecting finger extension counts; right hand tracks vertical velocity across a virtual strum-line.
- **Dynamic DSP Fallback:** Plays real studio guitar samples (`.wav`/`.mp3`), with an automated mathematical sine/exponential decay audio synthesizer fallback.

### 2. Spatial Drum Kit
- **Arc Layout:** Snare, Kick, Hi-Hat, Crash, Ride, and Tom-Toms arranged in realistic spatial hit zones.
- **Velocity Sensitivity:** Tracks downwards hand speed to scale strike volume and trigger realistic visual impact animations without false double-triggers.

### 3. Hybrid Multimodal Harmonium
- **Tactile + Gestural Control:** Combines keyboard key triggers for melodic precision with Farneback Dense Optical Flow tracking hand motion to dynamically simulate pumping the air bellows (volume pressure).

### 4. Recursive Loop Station
- **Event-Based Layering:** Captures musical event timestamps rather than noisy microphone audio.
- Reconstructs and mixes multi-track compositions using NumPy floating-point buffers and exports clean `.wav` audio files.

---

## System Architecture & Tech Stack

```text
 Webcam (720p 30 FPS)
         │
         ▼
 [OpenCV / Video Capture] ───► Bitwise Mirror (cv2.flip) & Color Conversion
         │
         ▼
 [MediaPipe Hands Pipeline] ──► 21 3D Landmark Regression per Hand
         │
         ├────────────────────────────────────────┐
         ▼                                        ▼
[Interaction Logic]                      [Pressure Engine]
 • Guitar Fretting / Strumming            • Farneback Dense Optical Flow
 • Drum Spatial Collision                 • Real-time Bellows Pressure
         │
         ▼
 [Audio Engine (Pygame Mixer + NumPy)]
 • 64-Channel Polyphonic Audio
 • Mathematical Waveform Synthesis (Sine / Square / Noise)
 • Exponential Decay Envelopes
         │
         ▼
 [Looper Station & WAV Exporter] ──► ./Recordings/track.wav
```

- **Core Logic:** Python 3.10
- **Computer Vision:** OpenCV (cv2)
- **Hand Tracking:** Google MediaPipe (`mp.solutions.hands`)
- **Digital Signal Processing (DSP):** NumPy
- **Audio Mixing & Channels:** Pygame Mixer
- **Event Hooks:** Pynput Keyboard Listener

---

## Quick Start Guide

### Prerequisites
- Python **3.10** (Recommended for MediaPipe Solutions compatibility).
- A standard laptop webcam.

### 1. Clone the Repository
```bash
git clone https://github.com/code4nigel/Air-band.git
cd Air-band
```

### 2. Set Up Virtual Environment & Dependencies
```bash
# Using standard Python
python -m venv .venv310
.\.venv310\Scripts\activate

# Install required dependencies
pip install -r requirements.txt
pip install "mediapipe<=0.10.14"
```

*(Alternatively, if using [uv](https://github.com/astral-sh/uv): `uv venv .venv310 --python 3.10 && uv pip install -r requirements.txt "mediapipe<=0.10.14"`)*

### 3. Launch Air Band
Double-click `run_airband.bat` or run:
```bash
python "air_instruments_63 Final.py"
```

---

## Controls & Hotkeys

| Key | Action |
| :---: | :--- |
| `g` | Switch to **Guitar** mode |
| `d` | Switch to **Drums** mode |
| `h` | Switch to **Harmonium** mode |
| `r` | Start / Stop **Loop Recording** |
| `l` | Toggle playback of the last recorded loop |
| `o` | Stop all active loops |
| `m` | Toggle GUI menu overlay |
| `Esc` | Exit application |

---

## Contributors

- **Shivanshu Yadav** - [GitHub](https://github.com/code4nigel)
- **Uday Singh Prajapati** - [GitHub](https://github.com/Uday75906)
- **Vishal Kumar Gupta** - [GitHub](https://github.com/vishal123-aiml)

---

## License
This project was developed as an academic Minor Project and patent-published intellectual property. All rights reserved.
