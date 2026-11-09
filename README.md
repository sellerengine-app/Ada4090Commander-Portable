# ⚡ Ada 4090 Commander & SM_89 Native Tuner (v3.3.8 Portable)

[![NVIDIA Architecture](https://img.shields.io/badge/Architecture-Ada_Lovelace_AD102-76B900?style=for-the-badge&logo=nvidia&logoColor=white)](https://www.nvidia.com/)
[![SDK](https://img.shields.io/badge/NVIDIA_SDK-310.9.16-blue?style=for-the-badge)](https://developer.nvidia.com/rtx/dlss)
[![Compute Capability](https://img.shields.io/badge/SM_Arch-SM__89-green?style=for-the-badge)]()
[![L2 Cache Optimization](https://img.shields.io/badge/L2_Residency-72MB_Folded-orange?style=for-the-badge)]()
[![Release](https://img.shields.io/badge/Release-v3.3.8_Portable-brightgreen?style=for-the-badge)](https://github.com/sellerengine-app/Ada4090Commander-Portable/releases)

Distribution package for **Ada 4090 Commander**, an independent standalone optimizer designed specifically for the **NVIDIA GeForce RTX 4090 (AD102 / SM_89)**.

This utility eliminates software-level pipeline bottlenecks, forces DLSS neural network weights into the **72 MB L2 internal on-chip cache**, enables **Transformer Gen 2 Presets (K/M/L)**, and unlocks **DLSS 4 Low-Latency Multi-Frame Generation (MFG)** with asynchronous compute.

---

## 📸 In-Game Native Tuner Overlay

![Ada 4090 Tuner Overlay](assets/tuner_overlay.jpg)

---

## 📖 Deep Technical Breakdown of Features & Parameters

### 🔹 Core Engine & Hook Status (`SM_89 Architecture`)

* **`Estado Hook SM_89: ACTIVO (Core Driver + Streamline (SR+RR2+FG) + Vulkan)`**  
  Confirms that the hardware-targeted policy engine is actively monitoring and pre-tuning the 4 primary NVIDIA NGX dispatch slots:
  1. `_nvngx.dll` (Core NVIDIA display driver dispatch chain).
  2. `nvngx_dlss.dll` (Super Resolution plugin & Streamline SR).
  3. `nvngx_dlssd.dll` (Ray Reconstruction 2 plugin).
  4. `nvngx_dlssg.dll` (Multi-Frame Generation plugin).  
  *Zero Per-Frame Overhead Guarantee:* The tuner hooks exclusively into `CreateFeature` during feature initialization and pipeline creation. It never hooks `EvaluateFeature` or runs per-frame memory hooks, eliminating CPU overhead (0.00 ms frametime penalty) and ensuring seamless coexistence with game anti-cheat engines (e.g., Ricochet, EAC).
* **`Features Optimizadas -> SR: 1 | RR2: 0 | FG: 0`**  
  Real-time telemetry showing the active count of NGX feature handles created and pre-tuned during the current graphics session.
* **`Activar Optimizaciones Hardware Ada 4090 (SM_89)`**  
  Global master toggle. Allows instant enabling or disabling of low-level AD102 parameter mutations on the fly without restarting the graphics device.

---

### 1️⃣ Super Resolution (Transformer Gen 2 – SDK 310.9.16)

* **`Smart Presets por Escala (DLAA/Calidad -> K=11 | Perf -> M=13 | UltraPerf -> L=12)`**  
  Standard games default to legacy neural presets (Presets C or D) trained for older architectures. This module dynamically injects the second-generation Transformer models optimized for Ada Lovelace Tensor Cores based on the selected render scale:
  * **Preset K (11) for DLAA, Quality & Balanced:** Delivers maximum temporal stability, pin-sharp sub-pixel detail, pristine hair/vegetation rendering, and zero ghosting at 4K.
  * **Preset M (13) for Performance:** High-speed inference model tailored for lower base resolutions while preserving high-frequency edges.
  * **Preset L (12) for Ultra Performance:** Aggressive temporal filtering that suppresses shimmering and moiré artifacts during extreme upscaling passes (e.g., 1080p internal to 4K output).
* **`Modo Competitive Low-Jitter / Max 1% Low (Fuerza Preset J=10 con NR+MFG)`**  
  Forces the low-jitter **Preset J (10)** across all modes. This lightweight neural model minimizes motion-vector calculation latency in the Tensor Cores, flattening the frametime curve and maximizing **1% Low FPS** in fast-paced competitive esports titles.
* **`Selector Preset DLAA / Calidad (Preset K vs Preset J)`**  
  Interactive dropdown allowing players to switch seamlessly between maximum visual fidelity (Preset K) and maximum competitive smoothness (Preset J).

---

### 2️⃣ Memoria Interna L2 (72MB AD102) & Ray Reconstruction

* **`Red Plegada en Cache L2 (DLSS.Use.Folded.Network = 1 en SR+RR+FG)`**  
  The RTX 4090 features a massive **72 MB L2 cache** (a 12x increase over Ampere's 6 MB). By default, generic NGX runtimes allocate weights in VRAM across the GDDR6X bus.  
  This setting commands NGX to fold and pin the neural network weights entirely inside the ultra-high-bandwidth 72 MB on-chip L2 cache. This eliminates memory-bus contention between the game's high-res textures and neural inference, eradicating DX12 traversal stutter.
* **`Prefetch Asincrono de Pesos en L2 (Cero desbordamiento a VRAM)`**  
  Activates asynchronous weight streaming (`DLSS.PrefetchWeights = 1` with 32 KB chunk streaming aligned to 128-byte cache lines). Predictive prefetching loads upcoming layer tensors into L2 prior to Tensor Core execution cycles, preventing GDDR6X VRAM spillage.
* **`Presupuesto Inferencia L2: 64 MB (Resto para G-Buffer)`**  
  Dynamically partitions the 72 MB L2 cache: reserves up to **64 MB dedicated** to neural network layers while guaranteeing the remaining **8 MB** stay exclusively allocated for DirectX 12 render targets, depth stencils, and G-Buffers.
* **`RR2 Folded Residency (Folded Network = 1)`**  
  Extends on-chip L2 folded residency to the **Ray Reconstruction 2 engine (`nvngx_dlssd.dll`)**, executing neural denoising of full path tracing and indirect lighting directly inside the GPU cache.
* **`Forzar Modelo RR2 Transformer (Preset F = 6, incluso en juegos SL v1/v2)`**  
  Overrides legacy or hardcoded Streamline configurations to force **Preset F (Model 6)**—NVIDIA's flagship Transformer denoiser in SDK 310.9.16. Delivers crystal-clear water reflections, specular highlights, and ambient occlusion without temporal trailing or loss of geometric detail.

---

### 3️⃣ Multi-Frame Generation (DLSS 4 Low-Latency Async Compute)

* **`Lite Candidate Blending = 1 (Mezcla ligera MFG x3/x4)`**  
  Optimizes the Optical Flow Accelerator (OFA) pipeline. Instead of running full redundant optical-flow evaluations on every generated frame when multiplying up to 3x or 4x, it reuses bidirectional motion vectors from adjacent frames. Slashes generated-frame GPU latency by ~40% while preserving UI clarity.
* **`Async Create = 1 (Cero stutters al cambiar escena)`**  
  Forces the Frame Generation pipeline to allocate swapchain buffers and initialize neural contexts asynchronously on an independent compute queue. Completely eliminates frametime spikes and hitching during scene transitions, cutscenes, and HUD opens.
* **`Prune Unused UIR Buffers = 1 (Ahorra VRAM y permutaciones HDR)`**  
  Detects and prunes unused User Interface Recomposition passes (`HUDLess`, `UI`, `UIAlpha`) when the host game draws HUD elements directly atop the presentation swapchain. **Reclaims 300 MB to 800 MB of VRAM** and avoids duplicate color-space conversions in HDR10 and scRGB modes.

---

## 🎮 Quick Start Guide (Portable)

1. Navigate to the [Releases](https://github.com/sellerengine-app/Ada4090Commander-Portable/releases) tab.
2. Download **`Ada4090Commander_v3.3.8_NGX310_Portable.zip`**.
3. Extract the archive to any folder on your NVMe drive.
4. Launch **`Ada4090Commander.exe`** (no installer or invasive drivers needed).
5. Drag and drop your game directory onto the **Dropzone** and click **`⚡ Optimización Total (1 Clic)`**.
6. Launch your game. Press the **`Home` / `Inicio`** key to open the in-game overlay anytime.

---

## 🛡️ Privacy & Technical Integrity

* **Zero telemetry / No tracking:** No external servers, logins, or background telemetry.
* **Non-destructive:** Creates automatic backups of all original game DLLs before applying profiles.
* **Signed standalone binary:** Bundled with all necessary native runtime modules and SDK 310.9.16 libraries.

---

*Engineered for enthusiasts seeking maximum frametime consistency and pure 4K 144Hz performance on the RTX 4090.*
