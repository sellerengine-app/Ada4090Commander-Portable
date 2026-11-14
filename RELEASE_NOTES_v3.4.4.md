# Ada 4090 Commander v3.4.4-NGX310 Portable

This release fixes the frame rate drop (11–21 FPS) and false *"frame rate is not steady"* shutdowns reported in **v3.4.3** when running **MFG for Legacy Games** in heavy 4K DirectX 12 games such as *Final Fantasy VII Remake*.

## What changed in v3.4.4

### 1. Decoupled WGC capture mailbox (`mfgl_host.exe`)
- Expanded Windows Graphics Capture `Direct3D11CaptureFramePool` from 2 to 3 buffers and decoupled `OnFrameArrived` from the optical-flow / interpolation engine thread via a 1-slot lock-guarded mailbox (`capMu_` / `capCv_` / `capFrame_`).
- `OnFrameArrived` now performs only a fast texture copy into the capture pool and returns immediately so WGC never stalls the game's DWM/DXGI presentation queue under 4K GPU load.

### 2. GPU, process & MMCSS scheduling priority (`mfgl_host.exe`)
- Promoted `mfgl_host.exe` to `HIGH_PRIORITY_CLASS` and opted out of Windows 11 EcoQoS (`ProcessPowerThrottling`).
- Registered `EngineLoop` with COM MTA and MMCSS `"Games"` (`AVRT_PRIORITY_HIGH`), set `IDXGIDevice1::SetGPUThreadPriority(7)`, added explicit `ID3D11DeviceContext::Flush()` after frame submission, and bounded swapchain waitable wait timeout to 8 ms (`WaitForSingleObjectEx(waitable_, 8, FALSE)`), preventing GPU queue starvation alongside demanding DX12 workloads.

### 3. On-demand optical flow & 4K L1 tuning (`mfgl_engine_d3d11.cpp`)
- Added `mfgl_push_frame_ex(eng_, tex, pts, computeFlow)` so the 5-level luma pyramid, bidirectional optical flow, and disocclusion inpainting passes are skipped when the pacer is paused, holding, or running at `1x`.
- Tuned L1 flow propagation from 2 iterations to 1 at `width >= 2560`.

### 4. Known Pack Hashes & App Version
- Updated `APP_VERSION` to `v3.4.4-NGX310`.
- Updated `BINARIES.sha256` and `KNOWN_PACK_SHA256` (`ada_commander.py`, 33 historical binary hashes) to recognize both v3.4.3 and v3.4.4 builds of `mfgl_host.exe`.

## Verification

- **No-XMX check:** `tools/check_no_xmx.py assets/renodx-mfgunlock.addon64` — clean (`0` hits).
- **Binary manifest check:** `BINARIES.sha256` — `526/526` checked entries match, `0` errors.
- **Python unit tests (isolated Windows desktop):** `396/396` active tests passed (`1` optional skipped: `test_scan` in `test_engine_ini.WukongReadOnly`, which requires `ADA_WUKONG_EXE`).
- **Native C++ unit tests (`native_mfg_legacy`):** `9/9` passed (`TOTAL_FAILED=0`).
- **4K GPU synth benchmarks (`run_f0.py` & `mfgl_host.exe --capture-source synth --test-focus-any --seconds 4 --mode x2`):**
  - SDR M=2 idle `p50_ms=3.224` | HDR M=2 idle `p50_ms=3.390` | SDR `--load 15` M=2 `p50_ms=2.582`
  - `hud_opaque_engine=99.000 dB` | scene cuts `10/10` | flash `false_cut_detections=0`
  - 3840x2160 HDR live host run: `in_fps=46.00`, `out_fps=81.96`, `m=2`, `gpu_engine_ms_p50=1.639`, `gpu_engine_ms_p95=2.448`, `errors=0`
- **Portable app startup smoke test (isolated Windows desktop):** stayed alive cleanly (`commander.log` logged library scan with `0` tracebacks).
- **Live in-game verification (*Final Fantasy VII Remake Intergrade*, `3840x2160` HDR10, 144 Hz display, DLSS 5 Neural Rendering active):**
  - `2x`: `40.66–53.52 FPS` base -> `84.49–102.73 FPS` output (`gpu_ms_per_real = 2.36–2.56 ms`, `pace_p99_ms = 0.00–0.02 ms`).
  - `4x`: `37.60–41.14 FPS` base -> `136.68–143.95 FPS` output (`gpu_ms_per_real = 2.72–5.29 ms`, `gpu_engine_ms_p50 = 2.605 ms`, `gpu_engine_ms_p95 = 5.385 ms`, `pace_p99_ms = 0.00–0.03 ms`, `8,130` presented frames, `3` dropped, `0` errors).
  - *External FPS counters note:* Because `mfgl_host.exe` presents generated frames in an out-of-process overlay swapchain (like Lossless Scaling), external FPS overlays hooked to the game executable (`ff7remake_.exe`) report only the game's base frame rate (`~40–44 FPS`), while the real + generated output rate (`85–144 FPS`) is reported in the in-game ReShade **MFG for Legacy Games** tab (`Generating: 4x · 41 to 144 fps`).

## Package integrity

Diff vs `Ada4090Commander_v3.4.3_NGX310_Portable.zip`: `1,670` total files (`1,667` unchanged, `3` modified, `0` added, `0` removed).

| Artifact | Size (bytes) | SHA-256 | Notes |
|---|---:|---|---|
| `Ada4090Commander_v3.4.4_NGX310_Portable.zip` | 510,861,820 | `4f1bf90ad1499a83dbdf99a9ca5f0fea373eb7d7916d4a43eb296ae450af8a06` | Full portable package |
| `Ada4090Commander.exe` | 4,769,147 | `87097a9cf3d20392392b9896a8a333736cca20b199327f9add1637ff19f183c8` | Updated `APP_VERSION` & `KNOWN_PACK_SHA256` |
| `_internal/assets/mfgl/mfgl_host.exe` | 708,608 | `b14187ce1e345d48ec0b377367688c9ca1658178bbd03473c2f400adab3d6a06` | Decoupled WGC mailbox, priority boost & on-demand flow |
| `_internal/assets/ada4090-mfgl.addon64` | 221,696 | `c408c30059799cd8c87c17803635c4838b87d2e93348624b773402352271b0c0` | Unchanged from v3.4.3 |
