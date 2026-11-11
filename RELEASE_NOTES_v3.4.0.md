# Ada 4090 Commander v3.4.0-NGX310 Portable

Published together with **v3.4.1**, which fixes the known issues listed below. Use v3.4.1.

## What's new
- **New interface:** Library, DLSS Swapper, Shaders, Health, Updates and Settings pages, and a game page with facts read from the game's files.
- **Health page:** reads `ReShade.log` and shows what it proves about the last session, quoting each line.
- **Safe deployment:** the original of every file the app touches is kept once in `_4090_Original`; Restore returns the game to those originals even after several deployments.
- **Frame generation route per game:** games without NVIDIA Streamline no longer get MFG Unlock (this removes the crash recorded in Final Fantasy VII Remake).
- **Photorealistic Neural Rendering profile** written on deployment (two passes, network scale 0.67, dark pedestal removal set to Always).
- **Tuner addon:** DXR Fast-Trace only where Direct3D 12 allows it, ray tracing recursion limit of 4 (0 turns it off), presets logged per DLSS feature, and the L2 cache and SER settings removed (they had no effect).
- **MFG Unlock:** crash fix in games without Streamline; Reflex "On" is now written as On (the app used to write the value for Off).
- The app no longer starts frozen when a removable drive has no media.

## Files

| File | Version | SHA-256 |
|---|---|---|
| `Ada4090Commander_v3.4.0_NGX310_Portable.zip` | — | `35fa79b65469d9f0ecfc170435adff058a2590eff48ba4687456e7cf4cac3721` |
| `ada4090-sm89-tuner.addon64` | v3.4.0 | `b409a01bb19b3b326996950c12d63e6953604dcabb26ead98f89ca0380ab1b12` |
| `renodx-mfgunlock.addon64` | 1.8.6-RTX4090-Expert v3.4.0 | `3dd5684b542dbd64de5b183bb8b1704151ee0377851eea3f512fb1835e49a7c7` |
| `nvngx_dlssnr.dll` | 310.9.16.0 (custom, not signed by NVIDIA) | `cdfa6c1ec784867182164c7836f324f087b5c9f374d0c9fe46f54999feabf3ed` |
| `nvngx_dlss.dll`, `nvngx_dlssd.dll`, `nvngx_dlssg.dll` | 310.9.16.0 (NVIDIA, unchanged) | as in v3.3.12 |

## Known issues (fixed in v3.4.1)
- Changing the multiplier, Reflex or resolution in the app rewrites the addons' settings, undoing changes made in their in-game panels.
- Health does not recognise the v3.4.0 tuner's log lines.
- Engine.ini is found by a partial name match and can be the wrong file; it also writes `r.ScreenPercentage=100`.
- Games without Streamline show a "Lossless Scaling Not Found" window at launch.
- New `ReShade.ini` files carry a preset path from another game.

## Installation
1. Download `Ada4090Commander_v3.4.0_NGX310_Portable.zip`.
2. Extract it into a new folder you can write to.
3. Run `Ada4090Commander.exe`.
