# Spectrum Meter — Windows VST3 analyzer

This source project embeds the supplied artwork as its background and draws a live FFT spectrum trace over it. The editor is resizable. It is a JUCE VST3 project intended for Windows DAWs.

## Build on Windows
1. Install Visual Studio 2022 with **Desktop development with C++**.
2. Install CMake 3.22+ and Git.
3. Extract this ZIP.
4. Open **x64 Native Tools Command Prompt for VS 2022** and change directory to this folder.
5. Run:
   ```bat
   cmake -S . -B build -A x64
   cmake --build build --config Release --target SpectrumMeter_VST3
   ```
   An internet connection is needed to download JUCE.
6. Locate `Spectrum Meter.vst3` under `build\SpectrumMeter_artefacts\Release\VST3\`.
7. Copy the entire `.vst3` folder to `C:\Program Files\Common Files\VST3\`, then rescan plugins in your DAW.

## Build with GitHub Actions
Upload all project files to a GitHub repository. Open **Actions** and run **Build Windows VST3**. Download the artifact from the successful workflow run.

## Current scope / important caveats
This is source code and a build workflow, not a precompiled VST3 binary. The live analyzer currently uses a 2048-point Hann-window FFT and a 30 FPS display. The supplied artwork is used as a background image, with a live trace drawn on top. Controls shown inside the artwork are part of the image and are not yet interactive; FFT/Curve/Waterfall/Sonogram modes, channel selection, selectable range/resolution/slope/averaging, peak hold, calibrated meter modes and commercial-level validation still need implementation. The background scales to the window and may stretch if resized to a different aspect ratio. The current frequency-bin mapping assumes 44.1 kHz, so proper sample-rate-aware calibration is also needed before calling it precision-grade.
