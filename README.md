# Ada 4090 Commander (v3.4.1 Portable)

[![Release](https://img.shields.io/badge/Release-v3.4.1_Portable-brightgreen?style=for-the-badge)](https://github.com/sellerengine-app/Ada4090Commander-Portable/releases/latest)
[![Platform](https://img.shields.io/badge/Platform-Windows_10%2F11-blue?style=for-the-badge)]()
[![GPU](https://img.shields.io/badge/Built_for-RTX_40_(Ada)-76B900?style=for-the-badge)]()

Primary target: GeForce RTX 4090.

Ada 4090 Commander is a portable Windows app. It installs a DLSS, frame generation and ReShade pack into your PC games and shows what is really happening in each game. It was built and tested on a GeForce RTX 4090 with a 4K 144 Hz display. Where something has not been measured in a game, this page says so.

## What the app does

| Page | What it does |
|---|---|
| **Library** | Finds installed games and shows, for each one, whether the pack is installed and which profile is detected. |
| **DLSS Swapper** | Switches a game between the pack's DLSS profiles. |
| **Shaders** | Precompiles a game's shaders with scskiller, a bundled third-party tool. |
| **Health** | Reads the game's `ReShade.log` and shows what it proves about the last session, quoting the log line. Anything the log cannot prove is shown as "Cannot be known". |
| **Updates** | Lists this repository's published releases. It never downloads or installs anything. |
| **Settings** | Windows multimedia scheduler, NVIDIA shader cache size, activity log and the online update check switch. |

Opening a game shows its **game page**: graphics API, whether NVIDIA Streamline is present, the DLSS DLL versions in the game folder, an anti-cheat notice when one is detected (it never blocks anything), and the cards below.

### Safe deployment and Restore
Before the first write, the app keeps the original of every file it touches in `_4090_Original` inside the game folder. **Restore** returns the game to those originals, even after several deployments. It also undoes the app's Engine.ini lines and its NVIDIA driver profile change (see below).

### Frame generation route, chosen per game
- **Games with Streamline:** DLSS Frame Generation with MFG Unlock (multipliers above 2x on RTX 40) and a frame rate cap through Reflex when VRR is active (refresh rate minus 2.8 %, 139.96 FPS on 144 Hz).
- **Games without Streamline** (for example Final Fantasy VII Remake): MFG Unlock is not installed. Frame generation comes from **NVIDIA Smooth Motion**, the driver's own 2x frame generation. If you own Lossless Scaling, the app can start it instead.

### NVIDIA driver profile (Smooth Motion)
On deployment the app may change one setting, **Smooth Motion**, in the NVIDIA driver profile of that game only:
- games without Streamline: turned **on** if it is not already on;
- games with DLSS Frame Generation: turned **off** if it only comes from your global setting, so the two frame generations do not stack.

It never changes your global setting, it does not write while the game is running, and Restore puts the game's profile back as it was. No administrator rights are needed.

### Engine.ini (Unreal Engine games)
- The app finds the game's own `Engine.ini` by exact project name. If it is not sure, it asks you instead of writing.
- With "Tune Engine.ini" on, it writes `t.MaxFPS=0`, `r.DynamicRes.OperationMode=0`, `sg.TextureQuality=3`, `sg.ShadowQuality=3` and a texture streaming pool sized to your VRAM (14336 MB on 24 GB). It no longer writes `r.ScreenPercentage=100`.
- **Ray tracing bounces** (Game default / High / Ultra), offered only when the game's executable contains the matching setting. Default: Game default. The effect depends on the game and is not measured.
- The card shows each line and its value as it is in the file, and who set it.

### Your settings stay yours
Only a full optimisation (1-click deploy, Update All) writes the pack's addon settings. Changing the multiplier or Reflex in the app writes only that setting, so what you change in an addon's in-game panel is kept. Nothing is written to `ReShade.ini` while the game is running.

## What is in the pack

| File | What it is |
|---|---|
| `nvngx_dlss.dll`, `nvngx_dlssd.dll`, `nvngx_dlssg.dll` | NVIDIA DLSS Super Resolution, Ray Reconstruction and Frame Generation 310.9.16, signed by NVIDIA, unchanged |
| `nvngx_dlssnr.dll` | Custom build of NVIDIA's 310.9.16 Neural Rendering runtime with native kernels for RTX 20, 30 and 40. Not signed by NVIDIA; network weights unchanged |
| `ada4090-sm89-tuner.addon64` | ReShade addon: DLSS presets (K for DLAA to Balanced, M for Performance, L for Ultra Performance, F for Ray Reconstruction), `DLSS.Use.Folded.Network = 1`, Frame Generation creation settings, DXR Fast-Trace only where Direct3D 12 allows it, and a ray tracing recursion limit of 4 (`DxrRecursionClampDepth=0` turns it off for a game). Its in-game panel says when each setting takes effect |
| `renodx-mfgunlock.addon64` | ReShade addon: Frame Generation multipliers above 2x on RTX 40 and the VRR frame rate cap |
| `renodx-dlss5.addon64`, `dlss5-feed.addon64`, `dxgi.dll` (ReShade 6.8.0), `scskiller\` | Third-party binaries |

### Neural Rendering cost on an RTX 4090
Final Fantasy VII Remake, 4K, two network passes: about 14.2 ms of GPU time for the whole neural feed at scale 0.67, against 24.9 ms at 1.00. In v3.4.1 two recompiled versions of the Neural Rendering kernels with different cache behaviour were measured in Final Fantasy VII Remake and Black Myth: Wukong. Both were less than 1 % faster, so the runtime is unchanged.

## What this pack does not do
- **No setting controls the GPU's L2 cache.** Earlier versions of this page claimed otherwise.
- **No "SER clamping".** Shader Execution Reordering is used by a game's own shaders; an addon cannot turn it on.
- **Settings of the tuner's DLSS section apply when the game creates DLSS** (at start, or when you change resolution or DLSS mode in the game's menu), not instantly. DXR settings apply after restarting the game.

## Requirements and safety
- Windows 10 or 11, NVIDIA GeForce RTX 40 series. Only tested on an RTX 4090.
- **Do not use the pack in online games with anti-cheat.** ReShade and its addons inject into the game.
- Portable: extract it into a folder you can write to, not under Program Files.

## Installation
1. Download **`Ada4090Commander_v3.4.1_NGX310_Portable.zip`** from the [latest release](https://github.com/sellerengine-app/Ada4090Commander-Portable/releases/latest).
2. Extract it into a new folder.
3. Run **`Ada4090Commander.exe`**.
