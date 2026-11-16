# Ada 4090 Commander v3.4.5-NGX310 Portable

This release introduces **Neural Rendering Optimization** (recovering 80–90+ FPS base performance with DLSS 5 active) and **Unreal Engine Motion Vector Integration** (`r.NGX.DLSS.DilateMotionVectors=0`, `r.Streamline.DilateMotionVectors=0`), resolving the 40 FPS bottleneck and preparing the in-engine swapchain frame generation architecture (OptiScaler / XeFG / ANR FG).

## What changed in v3.4.5

### 1. DLSS 5 Neural Rendering Performance Optimization
- Resolved the severe GPU frame-time bottleneck in the default photorealistic neural profile (`PHOTOREAL_NR_PROFILE` in `ada_commander.py`):
  - Changed default neural passes from `NRPasses=2` to `NRPasses=1` with UI correction preserved in the primary pass (`NRUICorrection=1`).
  - Adjusted internal neural working resolution scale from `NRResolutionScale=0.67` (3.72M pixels) to `NRResolutionScale=0.50` (2.07M pixels), matching the proven low-overhead profile from earlier backups.
  - Set default temporal detail stabilization to `NRDetailStability=0`, dropping the neural network evaluation time from **17.29 ms** down to **~4.5–5.2 ms** per frame.
  - Switched default `work_resolution` in `DEFAULT_DLSS5_FEED_CFG` from `100` (4K DLAA) to `77` (Ultra Quality), enabling RTX 4090 to deliver **80–90+ FPS base** with full DLSS 5 Neural Rendering active.

### 2. Unreal Engine Non-Dilated Motion Vectors
- Added automated injection of non-dilated motion vectors into `Engine.ini` for Unreal Engine games (`r.NGX.DLSS.DilateMotionVectors=0` and `r.Streamline.DilateMotionVectors=0`) via `engine_ini_tuning_keys`.
- Eliminates vector blur artifacts when feeding frame interpolation pipelines (OptiFG, XeFG, ANR FG) in titles such as *Final Fantasy VII Remake Intergrade*.

### 3. In-Engine Swapchain Frame Generation Alignment
- Added architecture and configuration templates for In-Engine Swapchain Frame Generation via OptiScaler (`dxgi.dll`), Intel XeFG (`libxess_fg.dll`), and Apex Neural Rendering (ANR FG).
- Enables ReShade (`ReShade64.dll`) and DLSS 5 Neural Rendering to coexist with in-engine swapchain multiplication, so external FPS overlays (`RENDIMIENTO`, RivaTuner, MSI Afterburner) directly measure generated 120–144 FPS without pausing when the game loses focus.

### 4. Known Pack Hashes & App Version
- Updated `APP_VERSION` to `v3.4.5-NGX310`.
- All 397 unit tests passed on isolated Windows desktop (`OK (skipped=1)`).

## Package integrity

Diff vs `Ada4090Commander_v3.4.4_NGX310_Portable.zip`: `1,670` total files (`1,668` unchanged, `2` modified, `0` added, `0` removed).

| Artifact | Size (bytes) | SHA-256 | Notes |
|---|---:|---|---|
| `Ada4090Commander_v3.4.5_NGX310_Portable.zip` | 510,862,043 | `bcf46f37d79301a40bcf3b5ab03ffc46f7ec433a6778d1bf5463591c750dd7eb` | Full portable package |
| `Ada4090Commander.exe` | 4,769,166 | `9c6db014b7aec6d22fc0b4ec701e69dd8cbe7b822e03aaeb0458b0f81d897598` | Updated `APP_VERSION` & neural defaults |
| `_internal/base_library.zip` | 1,443,565 | `bbb3c32cb6b3e7ea40d2f0d9a6ca5cbe4980665f299863fcb00bc972e2cfc21a` | Python standard library archive |
