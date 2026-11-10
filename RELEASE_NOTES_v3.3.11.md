# ⚡ Ada 4090 Commander v3.3.11 Portable (Universal Streamline & Auto-MFG Edition)

Standalone, fully portable release of **Ada 4090 Commander & SM_89 Native Tuner (v3.3.11-NGX310)**.

---

### 🆕 What's New in v3.3.11

#### 1. 🚀 Universal Streamline & Auto-MFG Fallback (1-Click Frame Generation)
* **Smart Streamline Auto-Detection & Deployment**:
  * Eliminates the restriction where non-native DLSS 3 titles (such as *Final Fantasy VII Remake Intergrade*, *Elden Ring*, *Kingdom Come: Deliverance II*, older Unreal Engine 4/5 titles) had Multi-Frame Generation disabled (`Streamline: Not detected`).
  * On **`⚡ Full Suite Deployment (1-Click)`**, the app detects whether the game has Streamline natively. If absent, it automatically bundles and deploys the official **NVIDIA Streamline Interposer Suite** (`sl.interposer.dll`, `sl.dlss_g.dll`, `sl.common.dll`, `sl.dlss.dll`, `sl.reflex.dll`, `sl.pcl.dll`, `sl.nis.dll`).
* **Proactive Native C++ Bootstrap Loader (`ada4090-sm89-tuner.addon64`)**:
  * Proactively loads and binds `sl.interposer.dll` and `nvngx_dlssg.dll` into the process address space during early initialization.
  * Allows `renodx-mfgunlock.addon64` to recognize Streamline as **`Active`** and enables full multi-frame multiplier control (**2x, 3x, 4x, 5x, 6x**) across non-native games in 1-Click!

#### 2. 🎭 1-Click Hyperrealistic Neural Face & Skin Reconstruction (Custom Viral Bodycam Edition)
* **Unlocked ReShade UI Boundaries (`NRModelSliderMax = 3.0`)**:
  * Raises stock ReShade slider limits up to 3.0, allowing unrestricted dynamic headroom for hyperrealistic neural tuning.
* **Unrestricted AI Weight Sensitivity Multipliers**:
  * **Skin Sensitivity (`NRModelSkinSensitivity = 1.45x`)**: Multiplies the 32 learned lane-13 input weights by 1.45x, unlocking authentic high-fidelity skin pores, subcutaneous microvascularization, specularity, and facial micro-relief.
  * **Structure Sensitivity (`NRModelStructureSensitivity = 1.25x`)**: Multiplies the 32 learned lane-12 structure weights by 1.25x for extreme tactical gear, fabric weave, and weapon definition.
  * **Tone & Style Sensitivities (`Tone = 1.20x`, `Style = 1.15x`, `LocalTone = 1.65`)**: Remodels dynamic range and micro-shadow contrast for the signature viral bodycam look.
* **Dual-Pass Hyperrealistic Stack (`Passes = 2`, `Pass2Intensity = 0.85`, `Pass2Color = 0.72`)**:
  * Re-injects an ultra-dense secondary refinement pass with highlight protection, eliminating temporal noise and delivering maximum photo-grade realism.
* **Optical Flow Temporal Stabilization (`DetailStability = Auto`)**:
  * Synchronizes inference with the Ada Optical Flow Accelerator to eliminate shimmering/swimming on moving cameras.

#### 3. ⚡ Low-Level DXR Ray Tracing Hardware Accelerator (Ada SM_89 / RTX 4090)
* **Smart DXR Auto-Detect**: Passive standby (0% overhead) until the engine dispatches its first DXR call.
* **Forced BVH Fast-Trace (`0x4`) & Recursion Clamping (`Depth = 2`)**: Eliminates VGPR register spills to VRAM.
* **72 MB AD102 L2 Folded Cache**: 64 MB tensor weights resident inside on-chip L2 SRAM.
* **Reflex VRR Hard-Clamp (140.0 FPS Ceiling)**: Eliminates frame queue latency on 144 Hz displays.

---

### ✨ What's Included in this Portable Build
- **`Ada4090Commander.exe`**: Complete desktop application (Dark Aurora UI, 1-Click Universal Deployment).
- **`ada4090-sm89-tuner.addon64`**: Recompiled C++20 hardware tuner with Proactive Streamline & DLSS-G Bootstrap Loader.
- **`renodx-mfgunlock.addon64`**: Multi-Frame Generation multiplier with support for up to 6x.
- **NVIDIA Streamline Interposer Suite**: Pre-packaged official runtime (`sl.interposer`, `sl.dlss_g`, `sl.common`, `sl.reflex`, `sl.dlss`, `sl.pcl`, `sl.nis`).
- **Official NVIDIA NGX SDK 310.9.16 Suite**: Pre-packaged signed runtimes (`nvngx_dlss.dll`, `nvngx_dlssg.dll`, `nvngx_dlssd.dll`, `nvngx_dlssnr.dll`).
- **`dlss5-feed.addon64` & `renodx-dlss5.addon64`**: DLSS 5 Neural Rendering backbuffer feeds with HDR10/sRGB capture.
- **`scskiller` Integration**: NVMe PSO precompilation engine to eliminate DX12 shader stutter.

---

### 📦 Installation
1. Download **`Ada4090Commander_v3.3.11_NGX310_Portable.zip`** below.
2. Extract anywhere (NVMe recommended).
3. Run **`Ada4090Commander.exe`**.
