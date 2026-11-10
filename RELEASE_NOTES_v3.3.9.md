# ⚡ Ada 4090 Commander v3.3.9 Portable (Streamline & Vulkan Edition - Hotfix Update)

Standalone, fully portable release of **Ada 4090 Commander & SM_89 Native Tuner (v3.3.9)**.

### 🆕 What's New in v3.3.9
- **🛡️ Streamline Native ABI Preservation (Rock-Solid Baseline)**:
  Strictly preserves host games' internal Streamline modules (`sl.*.dll`) intact. Completely resolves the access violation crashes (`0xC0000005` in `sl.dlss_d.dll`) caused by generic file swappers. All hooks are performed dynamically in memory by `ada4090-sm89-tuner.addon64` and `renodx-mfgunlock.addon64` without corrupting game engine vtables.
- **⚡ Official NVIDIA NGX SDK 310.9.16 Core Suite**:
  Synchronizes verified clean, signed NGX neural runtimes (`nvngx_dlss.dll`, `nvngx_dlssd.dll`, `nvngx_dlssg.dll`, `nvngx_dlssnr.dll`), unlocking Transformer Gen 2 Presets and Ray Reconstruction 2.
- **🌋 Khronos Vulkan Explicit Layer (`VkLayer_feed_vk`)**:
  Integrated native Vulkan layer supporting direct neural backbuffer feeding on pure Vulkan engines (*Doom Eternal*, *No Man's Sky*, *Baldur's Gate 3 Vulkan*, *Red Dead Redemption 2*).
- **🔐 Elevated Installation Helper (`elevate.exe`)**:
  Allows seamless profile deployment to protected system folders (e.g. `C:\Program Files\Steam` or Game Pass installations).
- **💾 Extended Backup & Recovery**:
  Timestamped `_4090_Backup_*` manifests automatically archive original binaries and configurations prior to deployment for 100% reversible rollback.

---

### ✨ What's Included in this Portable Build
- **`Ada4090Commander.exe`**: Complete desktop application featuring the **DLSS 5 Swapper-inspired Dark Aurora UI**, instant drag-and-drop game integration, and one-click profile optimizer.
- **`ada4090-sm89-tuner.addon64`**: In-game hardware tuner for ReShade & RenoDX with real-time overlay (`Home` key).
- **`renodx-mfgunlock.addon64`**: Multi-Frame Generation (MFG) multiplier unlocker (3x / 4x / 6x generation).
- **`dlss5-feed.addon64` & `renodx-dlss5.addon64`**: DLSS 5 Neural Rendering backbuffer feeds.
- **Native NGX SDK 310.9.16 Runtime DLLs**: Pre-packaged signed runtime components (`nvngx_dlss.dll`, `nvngx_dlssg.dll`, `nvngx_dlssd.dll`, `nvngx_dlssnr.dll`).
- **`scskiller` Integration**: Integrated NVMe PSO precompilation engine to eliminate DX12 shader stutter.

---

### 📦 Installation
1. Download **`Ada4090Commander_v3.3.9_NGX310_Portable.zip`** below.
2. Unzip anywhere (NVMe recommended).
3. Run **`Ada4090Commander.exe`**.

---

### 🎯 Tarjetas Gráficas Compatibles (GPU Hardware Compatibility)

| Serie / Arquitectura | Modelos | Soporte DLSS 5 Neural & RR2 | Soporte Multi-Frame Gen (MFG) | Optimización Caché L2 |
| :--- | :--- | :---: | :---: | :---: |
| **RTX Serie 40 (Ada Lovelace)**<br>*(SM_89 / Tier 1 - Objetivo Principal)* | **RTX 4090 / 4090D (24GB)**<br>• Silicio AD102 | ✅ Preset K/M/L + RR2 Preset F | ✅ Nativo OFA Gen 5 (Hasta 6x) | ✅ **72 MB Completa**<br>(64MB Inferencia / 8MB Buffers) |
| **RTX Serie 40 (Ada Lovelace)**<br>*(SM_89 / Tier 1)* | **RTX 4080 / 4080 Super (16GB)**<br>• Silicio AD103 | ✅ Preset K/M/L + RR2 Preset F | ✅ Nativo OFA Gen 5 (Hasta 4x) | ✅ **64 MB Adaptativa**<br>(54MB Inferencia / 10MB Buffers) |
| **RTX Serie 40 (Ada Lovelace)**<br>*(SM_89 / Tier 1)* | **RTX 4070 Ti Super / 4070 Ti / 4070 Super / 4070**<br>• Silicio AD103 / AD104 | ✅ Preset K/M/L + RR2 Preset F | ✅ Nativo OFA Gen 5 (Hasta 3x/4x) | ✅ **36 MB - 48 MB Adaptativa** |
| **RTX Serie 40 (Ada Lovelace)**<br>*(SM_89 / Tier 1)* | **RTX 4060 Ti (8GB/16GB) / RTX 4060 (8GB)**<br>• Silicio AD106 / AD107 | ✅ Preset K/M + RR2 Preset F | ✅ Nativo OFA Gen 5 (Hasta 3x) | ✅ **24 MB - 32 MB Adaptativa** |
| **RTX Serie 30 (Ampere)**<br>*(SM_86 / Tier 2)* | **RTX 3090 / 3090 Ti / 3080 / 3080 Ti / 3070 / 3060**<br>• Silicio GA102 / GA104 / GA106 | ✅ Preset K/M + RR2 Preset F | 🔄 Modo Smooth Motion / Companion | ⚠️ Modo Híbrido VRAM (6 MB L2) |
| **RTX Serie 20 (Turing)**<br>*(SM_75 / Tier 3)* | **RTX 2080 Ti / 2080 Super / 2080 / 2070 / 2060**<br>• Silicio TU102 / TU104 / TU106 | ✅ DLSS Super Resolution + RR | 🔄 Modo Interpolación Liviana | ⚠️ Modo VRAM Estándar (4-6 MB L2) |

> [!TIP]
> **Compatibilidad de Procesadores (CPU Target):**
> * **Intel:** Core 12ª, 13ª y 14ª generación (i5, i7, i9) optimizados con instrucciones vectoriales nativas AVX2 / FMA3.
> * **AMD:** Ryzen serie 5000, 7000, 9000 y modelos con 3D V-Cache (5800X3D, 7800X3D, 9800X3D) con soporte completo de paralelismo AVX2.
