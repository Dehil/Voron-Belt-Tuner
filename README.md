# 🎸 Voron Belt Tuner

A lightweight, browser-based web application to measure and tune the belt tension of your Voron 3D printer. It uses your device's microphone and the Web Audio API to detect the fundamental frequency of the plucked belt, functioning exactly like a digital guitar tuner.

Hosted entirely on **GitHub Pages**, it requires no backend, no installation, and works directly on your mobile phone's browser.

**→ [Open the app](https://dehil.github.io/Voron-Belt-Tuner/)**

![Voron Belt Tuner Preview](https://img.shields.io/badge/Voron-2.4-red)
![License](https://img.shields.io/badge/license-GPL--3.0-blue)
![No install](https://img.shields.io/badge/no%20install-required-green)

---

![App Screenshot](app.png)

---

## ✨ Key Features

- **Harmonic Rejection Algorithm**: Automatically detects and corrects 2nd/3rd harmonics, ensuring you are measuring the true fundamental frequency of the belt.
- **Pluck Detection Filter**: Uses an RMS amplitude threshold to ignore background noise and only register a reading when the belt is actually plucked.
- **Auto-Save on Stability**: Automatically saves the measurement to the channel after ~1 second of stable frequency reading.
- **Belt Spread Analysis**: Compares all measured belts (e.g., Z0-Z3) and calculates the Hz spread to tell you if your belts are balanced (✓ BALANCED) or need adjustment (✗ RE-TENSION).
- **Custom Configuration**: Fully customizable Target Hz, Range Min/Max, and Gauge Min/Max for non-Voron printers or custom setups.
- **Mobile-Optimized UI**: Sticky bottom action button, real-time signal strength indicator, and live spectrum analyzer.

## 🎯 Official Voron Tension Targets

Based on the official Voron documentation, the recommended tension frequencies remain consistent across all printer sizes (250/300/350):

| Belt Type | Target Frequency | Acceptable Range |
| :--- | :---: | :---: |
| **Z Belts (Z0-Z3)** | 55 Hz | 50 - 60 Hz |
| **A/B Belts (CoreXY)** | 110 Hz | 100 - 120 Hz |

*Note: Proper tension ensures dimensional accuracy, prevents ghosting/skipped steps, and reduces wear on the printer's kinematics.*

## 🚀 How to Use

1. **Select Belt Type**: Tap the **Z Belts**, **A/B Belts**, or **Custom** tab at the top.
2. **Select Channel**: Tap the specific belt you are measuring (e.g., Z0, Z1, A, B).
3. **Start Measuring**: Tap the sticky **◎ MEASURE** button at the bottom of the screen and allow microphone access.
4. **Pluck the Belt**: Firmly pluck the belt midway between the motor pulley and the carriage. 
   - *Watch the **Signal Indicator** bars above the frequency display to ensure your pluck is strong enough to pass the filter.*
5. **Auto-Save**: Hold the phone steady. Once the frequency stabilizes for ~1 second, it will automatically save to the channel.
6. **Check Spread**: After measuring all belts, check the **SPREAD** value in the Comparison section to ensure they are balanced.

## ️ Custom Mode Explained

If you are tuning a different printer (like a Trident, Switchwire, or non-Voron CoreXY), select the **Custom** tab to input your specific parameters:

- **Target Hz**: The ideal frequency you are aiming for.
- **Range Min / Range Max Hz**: Defines the "Perfect" green zone on the gauge and status badge.
- **Gauge Min / Gauge Max Hz**: Defines the absolute minimum and maximum bounds of the visual slider track.

## 💡 Tips for Best Results

- **Quiet Environment**: Turn off printer fans, exhaust systems, and nearby appliances. 
- **Plucking Technique**: Use your fingernail or a guitar pick for a clean, sharp pluck. Avoid muting the belt with your other hand.
- **Microphone Placement**: Hold your phone's microphone 2–4 inches away from the belt segment you are plucking.
- **Harmonics**: If your belt is very tight, it might naturally ring at a harmonic (e.g., 165 Hz instead of 55 Hz). The app's harmonic rejection handles this, but plucking closer to the center of the belt segment emphasizes the fundamental frequency.

## 🛠️ Technical Details

- **Pitch Detection**: Uses the `Web Audio API` (`AnalyserNode`) combined with a time-domain **autocorrelation algorithm** and parabolic interpolation.
- **Harmonic Rejection**: Calculates the ratio of the detected frequency to the target frequency. If it closely matches an integer multiple (e.g., 3.0x), it divides the frequency to find the true fundamental.
- **Pluck Filter**: Calculates the Root Mean Square (RMS) of the audio buffer. Pitch detection is only processed if the RMS exceeds the `PLUCK_THRESHOLD` constant.
- **Deployment**: Static HTML/JS/CSS, deployable to any static host (GitHub Pages, Cloudflare Pages, Netlify, Vercel).

## ⚠️ Disclaimer

This tool is provided as-is for community convenience. Always double-check your belt tension using the official manufacturer guidelines. The creator is not responsible for any hardware damage resulting from over-tensioning or under-tensioning.

## 🙌 Credits & Inspiration

- **Voron Design**: For the amazing open-source 3D printer ecosystem.
- **Web Audio API Community**: For the foundational pitch-detection algorithms (inspired by Chris Wilson's [Pitch Detect](https://github.com/cwilso/PitchDetect)).

---
*Made with ❤️ for the 3D Printing Community.*
