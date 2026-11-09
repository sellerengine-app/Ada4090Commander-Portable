# ⚡ Ada 4090 Commander v3.3.8 (SDK 310.9.16 Portable Release)

Standalone, fully portable release of **Ada 4090 Commander & SM_89 Native Tuner (v3.3.8)**.

### ✨ What's Included in this Portable Build
- **`Ada4090Commander.exe`**: Complete desktop application featuring the new **DLSS 5 Swapper-inspired Dark Aurora UI**, instant drag-and-drop game integration, and one-click profile optimizer.
- **`ada4090-sm89-tuner.addon64`**: In-game hardware tuner for ReShade & RenoDX with real-time overlay (`Home` key).
- **`renodx-mfgunlock.addon64`**: Multi-Frame Generation (MFG) multiplier unlocker (3x / 4x / 6x generation).
- **`dlss5-feed.addon64` & `renodx-dlss5.addon64`**: DLSS 5 Neural Rendering backbuffer feeds.
- **Native NGX SDK 310.9.16 Runtime DLLs**: Pre-packaged signed runtime components (`nvngx_dlss.dll`, `nvngx_dlssg.dll`, `nvngx_dlssd.dll`, `nvngx_dlssnr.dll`).
- **`scskiller` Integration**: Integrated NVMe PSO precompilation engine to eliminate DX12 shader stutter.

---

### 🚀 Key Highlights & Hardware Optimizations (AD102 / SM_89)

1. **72 MB L2 Cache Folded Residency (`DLSS.Use.Folded.Network = 1`)**:
   - Pins neural network weights entirely inside the ultra-fast on-chip 72 MB L2 cache of the RTX 4090.
   - Prevents memory-bus contention with GDDR6X VRAM, eliminating DX12 traversal stutter.
   - 64 MB reserved for inference + 8 MB reserved for DirectX 12 render targets / G-Buffers.

2. **Transformer Gen 2 Smart Presets (SDK 310.9.16)**:
   - **Preset K (11)**: Crystal-clear 4K resolution on DLAA / Quality / Balanced with zero ghosting.
   - **Preset M (13)**: High-speed inference for Performance mode.
   - **Preset L (12)**: Ultra Performance anti-shimmering filter.
   - **Preset J (10)**: Low-jitter competitive mode for maximum 1% Low FPS stability.

3. **Ray Reconstruction 2 (`nvngx_dlssd.dll` Preset F)**:
   - Overrides legacy Streamline denoisers with Transformer Model F (Preset 6).
   - Crisp reflections and noise-free global illumination with full L2 residency.

4. **Multi-Frame Generation (DLSS 4 Async Compute)**:
   - **Lite Candidate Blending**: ~40% faster frame generation by reusing adjacent optical-flow vectors.
   - **Async Create**: Asynchronous buffer creation eliminating cutscene / map hitching.
   - **Prune Unused UIR Buffers**: Frees 300 MB - 800 MB of VRAM by cutting redundant HUD passes.

---

### 📦 Installation
1. Download **`Ada4090Commander_v3.3.8_NGX310_Portable.zip`** below.
2. Unzip anywhere (NVMe recommended).
3. Run **`Ada4090Commander.exe`**.
