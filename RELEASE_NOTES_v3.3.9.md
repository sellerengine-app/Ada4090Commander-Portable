# ⚡ Ada 4090 Commander v3.3.9 (Streamline & Vulkan Portable Release)

Standalone, fully portable release of **Ada 4090 Commander & SM_89 Native Tuner (v3.3.9)**.

### 🆕 What's New in v3.3.9
- **Official NVIDIA Streamline SDK 310.9.16 Suite**:
  Direct integration of verified clean Streamline modules (`sl.common.dll`, `sl.interposer.dll`, `sl.dlss.dll`, `sl.dlss_g.dll`, `sl.dlss_nr.dll`, `sl.reflex.dll`, `sl.nis.dll`, `sl.pcl.dll`). Guarantees rock-solid stability and zero crashes on Streamline-driven games (such as *Cyberpunk 2077*, *Alan Wake 2*, *Call of Duty*).
- **Khronos Vulkan Explicit Layer (`VkLayer_feed_vk`)**:
  Integrated native Vulkan layer supporting direct neural backbuffer feeding on pure Vulkan engines (*Doom Eternal*, *No Man's Sky*, *Baldur's Gate 3 Vulkan*, *Red Dead Redemption 2*).
- **Elevated Installation Helper (`elevate.exe`)**:
  Allows seamless profile deployment to protected system folders (e.g. `C:\Program Files\Steam` or Game Pass installations).
- **Extended Backup & Recovery**:
  Timestamped `_4090_Backup_*` manifests now automatically archive preexisting Streamline and Vulkan files prior to deployment for 100% reversible rollback.

---

### ✨ What's Included in this Portable Build
- **`Ada4090Commander.exe`**: Complete desktop application featuring the **DLSS 5 Swapper-inspired Dark Aurora UI**, instant drag-and-drop game integration, and one-click profile optimizer.
- **`ada4090-sm89-tuner.addon64`**: In-game hardware tuner for ReShade & RenoDX with real-time overlay (`Home` key).
- **`renodx-mfgunlock.addon64`**: Multi-Frame Generation (MFG) multiplier unlocker (3x / 4x / 6x generation).
- **`dlss5-feed.addon64` & `renodx-dlss5.addon64`**: DLSS 5 Neural Rendering backbuffer feeds.
- **Native NGX SDK 310.9.16 Runtime DLLs**: Pre-packaged signed runtime components (`nvngx_dlss.dll`, `nvngx_dlssg.dll`, `nvngx_dlssd.dll`, `nvngx_dlssnr.dll`).
- **`scskiller` Integration**: Integrated NVMe PSO precompilation engine to eliminate DX12 shader stutter.

---

### 🚀 Key Hardware Optimizations (AD102 / SM_89)

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
1. Download **`Ada4090Commander_v3.3.9_NGX310_Portable.zip`** below.
2. Unzip anywhere (NVMe recommended).
3. Run **`Ada4090Commander.exe`**.
