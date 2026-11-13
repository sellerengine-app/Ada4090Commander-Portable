# Ada 4090 Commander v3.4.2-NGX310 Portable

Includes everything in v3.4.1. The app, the tuner addon, MFG Unlock and the Neural Rendering runtime change; the DLSS Super Resolution, Ray Reconstruction and Frame Generation runtimes are the same files.

## Neural Rendering runtime: 1.8 % faster on RTX 40, same image
The RTX 40 kernels no longer wait after each memory copy (316 copies in the heaviest kernels); they wait where NVIDIA's own code waits. On a bench that runs the runtime without a game (4K, two passes, scale 0.67), the output is bit-for-bit identical to v3.4.1 over 66,000 evaluations and the whole evaluation is 1.78 % faster. Not measured in a game. The kernels for RTX 20, 30 and 50 are byte-for-byte the same as in v3.4.1.

## What's new
- **DXR Fast-Trace off by default** in the tuner (`DxrFastTrace=0`). The tuner also logs DXR telemetry; its NVIDIA API watch is off by default.
- **MFG Unlock:**
  - the XMX generator is no longer in the build;
  - a pacing line in the log every 10 s (real frame interval, frames presented, and why a reset happened);
  - Waitable is greyed out while frame generation is on;
  - the adaptive quality suite and the validated blend are **experimental and off by default**. The validated blend never ran on an RTX 4090 before (the driver loaded NVIDIA's original code); that is fixed, but turning it on changes the generated frames and has not been checked in a game.
- **Keep neural rendering work memory**, a new per-game option, **off by default**. It writes `NRWorksetFreePolicy=1` for the DLSS 5 addon so it keeps its work sets instead of releasing them after 5 s. It may remove hitches when the game switches outputs and uses more VRAM. Not proven in a game session. Health shows a new row for it.
- **Engine.ini:** `sg.TextureQuality` and `sg.ShadowQuality` are written only if your in-game setting is lower; games that are not Unreal show no Engine.ini controls.
- **Frame generation route:** native only with proof on disk; the game page says which signal decided it.
- **New interface:** the game page is rebuilt (compact header, settings first, diagnostics folded under "Files in the game folder"); DLSS Swapper and Shaders use the same layout as the other pages; switches replace checkboxes; deleting shader caches is no longer a red button on the Library page. Buttons and dialogs have plain names: "Optimise game" (was "Full Suite Deployment (1-Click)"), "Apply low-latency profile", "Restore original files", "Update all games", "Precompile", "Delete shader cache".
- **Honest texts:** the interface is in English, with no emojis; no "0 Stutter" on the Shaders page; the summary after optimising lists what the tuner really does; Lossless Scaling is described as optional.
- **Fixes:** a damaged backup store no longer leaves scans, "Update all games", the Swapper, Health or the diagnostic waiting forever; an infinite value in `GameUserSettings.ini` no longer stops an optimisation.
- **Auto multiplier:** at a full optimisation the app picks 2x, 3x or 4x from the real frame rate of the last session (the smallest that reaches the output cap) and sets the cap from the refresh rate seen in the log (138 fps on 144 Hz). If the cap was already limiting that session, Auto keeps the current multiplier. A multiplier picked by hand is never changed. A game optimised with an earlier version keeps the 2x or 4x it had; the old default, 3x, becomes Auto.
- **Ray tracing options per game**, off by default: Ray Reconstruction and Hit Lighting (Engine.ini) and ray tracing quality High (Call of Duty). Each is offered only when the game shows it reads the setting; the game page says when the effect is not proven in a game session yet. Restore puts back what was there.
- **Restore report:** says when it gives back a DLSS DLL of uncertain origin to a game that does not use DLSS, and lists the files for which no original was kept.
- **Measured, not assumed:** on the bench, `DLSS.Use.Folded.Network = 1` changes neither the cost nor the image of Super Resolution; the README has the cost of each DLSS preset on an RTX 4090.
- `THIRD-PARTY-NOTICES.txt` is now included.

## In development, not enabled in this version
**MFG for Legacy Games:** our own frame generation (2x, 3x, 4x) for games without NVIDIA Streamline and without an upscaler, such as Final Fantasy VII Remake. It runs in a separate program, so nothing is injected into the game. The app already detects which games would use it, and the code is in this version, but it is switched off and has no controls: the integration in the app and a test in a game are not done. On a real 4K 144 Hz display with a test image, 2x, 3x and 4x keep a regular rhythm from 46 and 34 fps sources. On a bench without a game, at 4K: 5.2 ms of GPU time per real frame for 3x under load, and generated frames 6 dB (SDR) to 9 dB (HDR) better than a plain blend. Those games keep NVIDIA Smooth Motion (2x) in this version.

## Files

| File | Version | SHA-256 |
|---|---|---|
| `Ada4090Commander_v3.4.2_NGX310_Portable.zip` | — | `94a0260d6acdf8768ba5b5bb56c50f729aefee2eee026dccf4aed4c8e79f9b38` |
| `ada4090-sm89-tuner.addon64` | v3.4.2 | `d25c1af48c0aed5878373fd737ffc33af63528c1a27e9e1daa8fee0f13634682` |
| `renodx-mfgunlock.addon64` | v3.4.2 | `bf8b12fcd0ac4316cefa00eb99f5fdba3ee7a9f0cfc3770a712d43d5140a02eb` |
| `nvngx_dlssnr.dll` | 310.9.16.0 (custom, not signed by NVIDIA) | `9e731bce274065a475f725ae72bd030f9eb2ef83246b40e6ddf3972ec8305f53` |

## Known issues
- In `Engine.ini`, a value you change by hand on a line the app manages is overwritten at the next optimisation.
- A game optimised with an earlier version keeps `DxrFastTrace=1` until its next full optimisation ("Optimise game" or "Update all games").
- Tuner DLSS settings apply when the game creates DLSS, not instantly; DXR settings after a restart.
- The effect of the ray tracing bounces option depends on each game and has not been measured.
- Smooth Motion is 2x only.
- Call of Duty: if the game's settings file has two `DxrMode@1` lines, the ray tracing card says so and writes nothing; its switch cannot be changed until the file has one line again.

## Installation
1. Download `Ada4090Commander_v3.4.2_NGX310_Portable.zip`.
2. Extract it into a new folder you can write to.
3. Run `Ada4090Commander.exe`.
