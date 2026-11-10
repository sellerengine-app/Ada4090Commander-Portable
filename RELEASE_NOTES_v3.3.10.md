# ⚡ Ada 4090 Commander v3.3.10 Portable (DXR Hardware Fast-Trace & English Edition)

Standalone, fully portable release of **Ada 4090 Commander & SM_89 Native Tuner (v3.3.10-NGX310)**.

---

### 🆕 What's New in v3.3.10

#### 1. ⚡ Low-Level DXR Ray Tracing Hardware Accelerator (Ada SM_89 / RTX 4090)
* **Smart DXR Auto-Detect (Dynamic Hardware Accelerator)**:
  * Eliminates manual guesswork: starts in passive standby mode (0% CPU/GPU overhead, zero crash risk) when games do not issue DXR calls (e.g. *Kingdom Come: Deliverance II* using CryEngine SVO voxel GI).
  * Automatically detects and engages full Ada SM_89 hardware acceleration the exact moment a game engine issues its first DXR Ray Tracing call (e.g. *Black Myth: Wukong* Path Tracing, *Cyberpunk 2077* RT Overdrive, *Call of Duty* RT Sun Shadows).
* **Hardware Scratch Overflow Guard**:
  * Prevents out-of-bounds GPU scratch memory writes by strictly respecting host engine buffer allocations pre-sized for dynamic `PREFER_FAST_BUILD`, completely eliminating `DXGI_ERROR_DEVICE_HUNG` / `DEVICE_REMOVED` TDRs.
* **DirectX 12 Low-Level VMT Interception**:
  * Directly detours `ID3D12Device5::GetRaytracingAccelerationStructurePrebuildInfo` (slot 63), `ID3D12Device5::CreateStateObject` (slot 62), and `ID3D12GraphicsCommandList4::BuildRaytracingAccelerationStructure` (slot 72) with live `OnPresent` device bootstrap.
* **Forced BVH Fast-Trace (Maximum SAH Spatial Quality)**:
  * Optimizes static BLAS and TLAS structures to `PREFER_FAST_TRACE (0x4)` to minimize ray-box and ray-triangle traversal steps on Ada 3rd Gen RT Cores.
* **Max Trace Recursion Depth Clamping (`Depth = 2`)**:
  * Clamps state object pipeline recursion in `CreateStateObject` to 2 bounces, completely eliminating VGPR register spills to GDDR6X VRAM on SM_89 execution warps.
* **Dynamic Geometry Preservation**:
  * Safely preserves `PERFORM_UPDATE` on character meshes and deformable geometry to prevent visual artifacts or frame pacing penalties.

#### 2. 🎯 Competitive Low-Jitter / Maximum 1% Lows Architecture
* **72 MB AD102 L2 Folded Network**:
  * Keeps the 64 MB tensor inference weight budget fully resident inside on-chip L2 SRAM, preventing VRAM bandwidth contention during heavy 4K ray reconstruction workloads.
* **Asynchronous 32 KB Tensor Weight Prefetching**:
  * Eliminates pipeline bubbles between render passes.
* **Reflex VRR Hard-Clamp (140.0 FPS Ceiling)**:
  * Strictly clamps frame pacing to 140 FPS (280 basis points) on 144 Hz monitors, guaranteeing that G-Sync / VRR remains permanently active with zero frame queue latency.

#### 3. 🛡️ Streaming Native DLSS Detection & Script Launcher Support
* **Streaming 32 MB Chunk Scanning**:
  * Scans executables and massive engine DLLs (such as `WHGame.dll` at 88 MB in *Kingdom Come II*) without arbitrary file-size cutoffs, guaranteeing 100% accurate native DLSS classification and preventing accidental feeder collisions.
* **Smart Script Launcher Integration**:
  * Seamlessly launches games requiring dedicated bootstrap scripts or offline anti-cheat drivers (e.g. `!start_sp26.bat` in *Call of Duty*) when clicking Play.
* **Bundled High-Resolution Cover Art**:
  * All 18 official game artworks pre-packaged in `_internal/assets/covers` and `assets/covers` for instant visual rendering in the library.

#### 4. 🌐 Full English Native UI & Unambiguous Action Controls
* **Complete Native English Interface**:
  * All views (Home, Games Library, DLSS Swapper, Shader Cache, Updates, Settings & Driver), tooltips, telemetry badges, and notifications are now rendered in clean, native English.
* **Clear Action Differentiation in Game Detail**:
  * **`⚡ Full Suite Deployment (1-Click)`**: Complete platform deployment (installs DLSS Triad DLLs, SCSKiller shader precompilation, Engine.ini tuning & Feeder).
  * **`🎯 Competitive Low-Jitter Profile (1% Lows)`**: Pure frametime pacing refresh (enforces zero-jitter presets, 140 FPS VRR clamp, 72MB L2 folded cache & DXR Fast-Trace without touching game engine files).
  * **Integrated In-App Action Guide**: Clear explanation box displayed directly beneath action buttons for instant clarity.

---

### ✨ What's Included in this Portable Build
- **`Ada4090Commander.exe`**: Complete desktop application featuring the **Dark Aurora UI**, drag-and-drop game integration, and dual action profile deployment.
- **`ada4090-sm89-tuner.addon64`**: Native C++20 hardware tuner for ReShade & RenoDX with Section 4 DXR Hardware Accelerator overlay (`Home` key).
- **`renodx-mfgunlock.addon64`**: Multi-Frame Generation (MFG) multiplier unlocker with VRR Hard-Clamp.
- **`dlss5-feed.addon64` & `renodx-dlss5.addon64`**: DLSS 5 Neural Rendering backbuffer feeds with HDR10 and sRGB capture.
- **Official NVIDIA NGX SDK 310.9.16 Suite**: Pre-packaged signed runtimes (`nvngx_dlss.dll`, `nvngx_dlssg.dll`, `nvngx_dlssd.dll`, `nvngx_dlssnr.dll`).
- **`scskiller` Integration**: Integrated NVMe PSO precompilation engine to eliminate DX12 shader stutter.

---

### 📦 Installation
1. Download **`Ada4090Commander_v3.3.10_NGX310_Portable.zip`** below.
2. Extract anywhere (NVMe recommended).
3. Run **`Ada4090Commander.exe`**.

---

### 🎯 GPU Hardware Compatibility

| Series / Architecture | Models | DLSS 5 Neural & RR2 | Multi-Frame Gen (MFG) | L2 Cache Optimization | DXR Ray Tracing Accelerator |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **RTX 40 Series (Ada Lovelace)**<br>*(SM_89 / Tier 1 - Primary Target)* | **RTX 4090 / 4090D (24GB)**<br>• AD102 Silicon | ✅ Preset K/M/L + RR2 Preset F | ✅ Native OFA Gen 5 (Up to 6x) | ✅ **72 MB Full**<br>(64MB Inference / 8MB Buffers) | ✅ **Fast-Trace + SER Clamping** |
| **RTX 40 Series (Ada Lovelace)**<br>*(SM_89 / Tier 1)* | **RTX 4080 / 4080 Super (16GB)**<br>• AD103 Silicon | ✅ Preset K/M/L + RR2 Preset F | ✅ Native OFA Gen 5 (Up to 4x) | ✅ **64 MB Adaptive**<br>(54MB Inference / 10MB Buffers) | ✅ **Fast-Trace + SER Clamping** |
| **RTX 40 Series (Ada Lovelace)**<br>*(SM_89 / Tier 1)* | **RTX 4070 Ti Super / 4070 Ti / 4070 Super / 4070**<br>• AD103 / AD104 Silicon | ✅ Preset K/M/L + RR2 Preset F | ✅ Native OFA Gen 5 (Up to 3x/4x) | ✅ **36 MB - 48 MB Adaptive** | ✅ **Fast-Trace + SER Clamping** |
| **RTX 40 Series (Ada Lovelace)**<br>*(SM_89 / Tier 1)* | **RTX 4060 Ti (8GB/16GB) / RTX 4060 (8GB)**<br>• AD106 / AD107 Silicon | ✅ Preset K/M + RR2 Preset F | ✅ Native OFA Gen 5 (Up to 3x) | ✅ **24 MB - 32 MB Adaptive** | ✅ **Fast-Trace Adaptive** |
| **RTX 30 Series (Ampere)**<br>*(SM_86 / Tier 2)* | **RTX 3090 / 3090 Ti / 3080 / 3080 Ti / 3070 / 3060**<br>• GA102 / GA104 Silicon | ✅ Preset K/M + RR2 Preset F | 🔄 Smooth Motion / Companion Mode | ⚠️ Hybrid VRAM Mode (6 MB L2) | ✅ **Fast-Trace Passthrough** |
| **RTX 20 Series (Turing)**<br>*(SM_75 / Tier 3)* | **RTX 2080 Ti / 2080 Super / 2080 / 2070 / 2060**<br>• TU102 / TU104 Silicon | ✅ DLSS Super Resolution + RR | 🔄 Lightweight Interpolation | ⚠️ Standard VRAM Mode (4-6 MB L2) | ✅ **Fast-Trace Passthrough** |
