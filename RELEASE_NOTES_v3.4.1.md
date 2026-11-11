# Ada 4090 Commander v3.4.1-NGX310 Portable

Includes everything in v3.4.0. Only the app and the tuner addon change; the DLSS runtimes, the Neural Rendering runtime and MFG Unlock are the same files.

## What's new
- **NVIDIA Smooth Motion per game.** On deployment the app sets Smooth Motion in that game's NVIDIA driver profile: on for games without Streamline (if not already on), off for games with DLSS Frame Generation when it only comes from your global setting. It never changes the global setting; Restore puts the profile back. No administrator rights needed.
- **No more "Lossless Scaling Not Found" window.** The game page shows which frame generation is used (Smooth Motion, or Lossless Scaling if you own it).
- **Engine.ini rebuilt:**
  - found by exact project name; when unsure the app asks;
  - texture streaming pool sized to your VRAM (14336 MB on 24 GB);
  - `r.ScreenPercentage=100` is no longer written;
  - new per-game **ray tracing bounces** option (Game default / High / Ultra), off by default;
  - Restore removes only the lines the app wrote.
- **Your panel settings stay.** Only a full optimisation writes the addons' settings; the multiplier and Reflex selectors write only their own setting. Nothing is written while the game is running.
- **Tuner panel** says when each setting takes effect (when the game creates DLSS, or after a restart) and marks pending changes.
- **Health** recognises the tuner and shows the preset applied for each DLSS mode.
- Fixes: no preset path from another game in new `ReShade.ini` files; XeSS DLLs and SCSKiller's game list are backed up before being changed; the machine panel shows "GPU not detected" instead of default values; Restore's summary stays on screen; the DLSS Swapper opens instantly.

## Neural Rendering runtime: measured, unchanged
Two recompiled versions of the Neural Rendering kernels for the RTX 4090 (different L1 and L2 cache behaviour) were measured in Final Fantasy VII Remake and Black Myth: Wukong. Both were less than 1 % faster, so the runtime stays the same.

## Files

| File | Version | SHA-256 |
|---|---|---|
| `Ada4090Commander_v3.4.1_NGX310_Portable.zip` | — | `a541a74e3947593adfe2842a6dbe1a002c51f88096a6201058aab2be47a1f6b5` |
| `ada4090-sm89-tuner.addon64` | v3.4.0 + v3.4.1 panel | `02a352a9e89296a305626d9be08d7719dc5f5094894a410fcc23dc3168e250d9` |
| `renodx-mfgunlock.addon64` | 1.8.6-RTX4090-Expert v3.4.0 | `3dd5684b542dbd64de5b183bb8b1704151ee0377851eea3f512fb1835e49a7c7` |
| `nvngx_dlssnr.dll` | 310.9.16.0 (custom, not signed by NVIDIA) | `cdfa6c1ec784867182164c7836f324f087b5c9f374d0c9fe46f54999feabf3ed` |

## Known issues
- Tuner DLSS settings apply when the game creates DLSS, not instantly; DXR settings after a restart.
- The effect of the ray tracing bounces option depends on each game and has not been measured.
- Smooth Motion is 2x only.

## Installation
1. Download `Ada4090Commander_v3.4.1_NGX310_Portable.zip`.
2. Extract it into a new folder you can write to.
3. Run `Ada4090Commander.exe`.
