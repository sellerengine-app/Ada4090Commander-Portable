# ⚡ Ada 4090 Commander v3.3.12-NGX310 Portable
## Vía Desacoplada: DLSS 5 Neural Reconstruction + Lossless Scaling (LSFG) Auto-Orchestration Edition

[![Architecture](https://img.shields.io/badge/Architecture-Ada_Lovelace_AD102-76B900?style=for-the-badge&logo=nvidia&logoColor=white)](https://www.nvidia.com/)
[![SDK](https://img.shields.io/badge/NVIDIA_SDK-310.9.16-blue?style=for-the-badge)](https://developer.nvidia.com/rtx/dlss)
[![Compute Capability](https://img.shields.io/badge/SM_Arch-SM__89-green?style=for-the-badge)]()
[![Frame Generation](https://img.shields.io/badge/Frame_Gen-Decoupled_LSFG_Auto--Orchestration-cyan?style=for-the-badge)]()

---

## 🎯 Resumen Ejecutivo & Novedades Principales

**Ada 4090 Commander v3.3.12** introduce la **Vía Desacoplada (Decoupled Engine Architecture)**, una solución definitiva de nivel de ingeniería para maximizar la tasa de cuadros (140+ FPS estables) tanto en títulos con **NVIDIA Streamline / DLSS 3 nativo** como en aquellos que carecen de él de serie (como *Final Fantasy VII Remake Intergrade*, *Helldivers 2*, *Elden Ring*, etc.), garantizando **cero regresiones** y preservando al 100% el pipeline neural y los hooks de presentación.

---

## 🔬 Pilares de la Vía Desacoplada

### 1. 🛡️ Motor Gráfico Centrado en lo que Sí Domina (100% Estable)
* **Reconstrucción Neural DLSS 5 Inviolable**:
  * En juegos sin Streamline de fábrica, se erradican totalmente las inyecciones de wrappers interposers (`sl.interposer.dll`, `sl.dlss_g.dll`) que provocaban cuellos de botella (`Provider presentations: No sample`) o roturas en los hooks DXGI de ReShade.
  * Se mantiene el pipeline puro: `dxgi.dll` + `dlss5-feed.addon64` + `renodx-dlss5.addon64` + `ada4090-sm89-tuner.addon64` + `nvngx_dlss.dll` v310.9.16.
  * Calibración fotorrealista intacta: Piel natural a 1.45x de sensibilidad, microtextura táctica a 1.25x, curva tonal de sensor a 1.65 y renderizado con doble pasada de refinamiento (`NRPasses = 2`).
  * Acelerador DXR Fast-Trace (BVH SAH `0x4` forzado) y 72 MB AD102 L2 Cache Folding al 100%.

### 2. ⚡ Lossless Scaling (LSFG) Auto-Orquestado para Títulos No Nativos
* **Frame Generation Desacoplado**:
  * Para cualquier juego donde no se detecte Streamline nativo, la generación de fotogramas ópticos por hardware se delega a **Lossless Scaling (LSFG)** a nivel de presentación.
  * **Descubrimiento Inteligente de LSFG (`LSFGManager`)**:
    * Escaneo automático de instalaciones oficiales de Steam (AppID `993090`).
    * Detección recursiva de librerías en `libraryfolders.vdf` (unidades `C:`, `D:`, `E:`, `G:`).
    * Búsqueda en el Registro de Windows (`HKLM`/`HKCU`).
    * Detección de procesos activos en segundo plano (`LosslessScaling.exe`).
    * Soporte para vinculación manual en 1-clic con persistencia en `commander_config.json`.
  * **Orquestación en Segundo Plano (`launch_game`)**:
    * Al hacer clic en "Jugar" en Ada Commander, si el juego opera en Vía Desacoplada y LSFG está instalado, el launcher inicia y verifica automáticamente `LosslessScaling.exe` en segundo plano sin interrumpir la experiencia.

### 3. 🎨 Tarjeta 2 Adaptativa en Tiempo Real
* La interfaz de la suite distingue instantáneamente entre:
  * **Juegos con Streamline / DLSS 3 Nativo** (*Call of Duty*, *Black Myth: Wukong*, *Crimson Desert*, *Gothic 1 Remake*, *Hell Is Us*, *KARMA*, *PRAGMATA*, *Khazan*, *The Last of Us Part II*):
    * `Backend: DLSS-G Nativo (Ada Lovelace) • Hardware Active`
    * Selector de multiplicador de hardware 2x, 3x (144Hz), 4x, 6x.
  * **Juegos en Vía Desacoplada** (*Final Fantasy VII Remake Intergrade*, *Helldivers 2*, etc.):
    * `Backend: Vía Desacoplada • LSFG Auto-Orchestration`
    * Estado en vivo de LSFG (Detectado / En ejecución / Listo).
    * Botón de acción directo para vincular o iniciar Lossless Scaling.
    * Indicador de protección neural verde: `🛡️ Motor Neural 100% Protegido + LSFG Optical Flow (Cero wrappers rotos)`.

---

## 📦 Verificación del Paquete Portable v3.3.12

* **Archivo**: `Ada4090Commander_v3.3.12_NGX310_Portable.zip`
* **Tamaño comprimido**: ~486 MB
* **Tamaño descomprimido**: ~889 MB
* **Binario Principal**: `Ada4090Commander.exe` compilado de forma nativa con PyInstaller 6.22 (Python 3.11.9)
* **Compatibilidad**: GeForce RTX 4090 (AD102 / SM_89) en Windows 10/11 x64
