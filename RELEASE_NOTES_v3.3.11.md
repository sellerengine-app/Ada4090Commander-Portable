# ⚡ Ada 4090 Commander v3.3.11 Portable (Photorealistic Neural Reconstruction Edition)

Standalone, fully portable release of **Ada 4090 Commander & SM_89 Native Tuner (v3.3.11-NGX310)**.

---

### 🆕 What's New in v3.3.11

#### 1. 🎭 1-Click Photorealistic Neural Face & Micro-Texture Reconstruction
* **Elimination of the "Plastic / Wax Figure" Look**:
  * Stock DLSS and temporal upscalers aggressively smooth organic surfaces like skin, fabric, and hair.
  * In v3.3.11, the Tensor Core neural pipeline integrates calibrated high-precision weights specifically tuned for organic materials and photorealistic sensor response.
* **Unlocked ReShade UI Boundaries (`NRModelSliderMax = 3.0`)**:
  * Extends the default ReShade slider ceilings from 1.0 to 3.0, unlocking unrestricted dynamic range and control for hyperrealistic tuning.
* **Calibrated AI Weight Sensitivity Multipliers**:
  * **Skin Sensitivity (`NRModelSkinSensitivity = 1.45x`)**: Multiplies the 32 learned lane-13 skin weights by 1.45x, delivering authentic subcutaneous microvascularization, skin pore definition, and natural dermal specularity.
  * **Structure Sensitivity (`NRModelStructureSensitivity = 1.25x`)**: Multiplies the 32 learned lane-12 structure weights by 1.25x for extreme definition on tactical fabrics, leather, metals, and fine environment geometry.
  * **Tone & Style Response (`NRModelToneSensitivity = 1.20x`, `NRLocalTone = 1.65`)**: Remodels local micro-contrast and sensor exposure response to eliminate flat, washed-out shadows.
* **Dual-Pass Hyperrealistic Stack (`NRPasses = 2`, `NRPass2Intensity = 0.85`, `NRPass2Color = 0.72`)**:
  * Runs a high-density secondary refinement pass with highlight protection, eliminating temporal noise and delivering photo-grade fidelity.
* **Optical Flow Temporal Stabilization (`NRDetailStability = Auto`)**:
  * Synchronizes inference directly with the Ada Optical Flow Accelerator (OFA) to eliminate crawling and shimmering during fast camera pans.

#### 2. 🛡️ Robust DLSS Feeder Protection & Native Auto-Detection Safeguard
* **Eliminated False-Positive Native DLSS Collisions**:
  * Fixed an issue where non-native titles (such as *Final Fantasy VII Remake Intergrade*, *Elden Ring*, and older Unreal Engine 4/5 titles) could be falsely detected as native DLSS games due to loose wrapper files.
  * Ensures `dlss5-feed.addon64` and `DLSS5_Feed.fx` remain 100% active and correctly configured in `ReShade.ini`, guaranteeing immediate out-of-the-box Neural Rendering without manual intervention.

#### 3. ⚡ Low-Level DXR Ray Tracing Hardware Accelerator (Ada SM_89 / RTX 4090)
* **Smart DXR Auto-Detect**: Passive standby (0% overhead) until the engine dispatches its first DXR call.
* **Forced BVH Fast-Trace (`0x4`) & Recursion Clamping (`Depth = 2`)**: Eliminates VGPR register spills to GDDR6X VRAM.
* **72 MB AD102 L2 Folded Cache**: 64 MB tensor weights kept resident inside ultra-fast on-chip L2 SRAM.
* **Reflex VRR Hard-Clamp (140.0 FPS Ceiling)**: Eliminates frame queue latency on 144 Hz displays.

---

### ✨ What's Included in this Portable Build
- **`Ada4090Commander.exe`**: Complete desktop application (Dark Aurora UI, 1-Click Universal Deployment).
- **`ada4090-sm89-tuner.addon64`**: Recompiled C++20 hardware tuner with DXR Fast-Trace and NGX Detours.
- **`renodx-mfgunlock.addon64`**: Multi-Frame Generation multiplier with support for up to 6x.
- **Official NVIDIA NGX SDK 310.9.16 Suite**: Pre-packaged signed runtimes (`nvngx_dlss.dll`, `nvngx_dlssg.dll`, `nvngx_dlssd.dll`, `nvngx_dlssnr.dll`).
- **`dlss5-feed.addon64` & `renodx-dlss5.addon64`**: DLSS 5 Neural Rendering backbuffer feeds with HDR10/sRGB capture.
- **`scskiller` Integration**: NVMe PSO precompilation engine to eliminate DX12 shader stutter.

---

### 📦 Installation
1. Download **`Ada4090Commander_v3.3.11_NGX310_Portable.zip`** below.
2. Extract anywhere (NVMe recommended).
3. Run **`Ada4090Commander.exe`**.
