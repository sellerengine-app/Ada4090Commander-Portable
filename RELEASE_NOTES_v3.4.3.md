# Ada 4090 Commander v3.4.3-NGX310 Portable

Includes everything in v3.4.2. The app changes and MFG for Legacy Games is added: a new program and a new ReShade add-on with its tab in the game. The NVIDIA runtimes, the Neural Rendering runtime, the tuner addon and MFG Unlock are the same files as in v3.4.2.

## MFG for Legacy Games
Our own frame generation (2x, 3x, 4x or Auto) for games that have no DLSS Frame Generation, such as Final Fantasy VII Remake. It is a separate program that captures the game window and shows the generated frames on top of it; a small ReShade add-on in the game starts it and gives you its tab.

- **You handle it in the game.** Open the ReShade panel (Home key) and use the **MFG for Legacy Games** tab: Off, Auto, 2x, 3x or 4x. The change applies at once, without closing the game, and your choice is kept for the next time.
- **It starts with the game, however you start it:** from the app, from its store or from a shortcut.
- **It is on after "Optimise game"** in games without DLSS Frame Generation, starting at 2x (what NVIDIA Smooth Motion gave in those games). In a game where the app detects anti-cheat it stays off unless you turn it on in the game page.
- **It replaces NVIDIA Smooth Motion in those games** (two frame generators cannot run together): the app turns Smooth Motion off for that game and Restore puts it back. To keep Smooth Motion in a game, switch "Use MFG for Legacy Games" off in its game page and optimise again.
- **No frame rate limit of ours.** The game runs free; the only ceiling is your display's refresh rate. When the game's frame rate moves, each generated frame is shown at the time its content belongs to.
- **Borderless window only.** Exclusive full screen is not supported, and the tab says so.
- **Panic key:** Ctrl+Alt+F12 turns it off.
- **It works from the final image only,** so it adds latency (about one real frame) and cannot match DLSS Frame Generation.
- If you change the game's resolution or move it to another monitor, it starts again by itself.
- If you used NVIDIA Smooth Motion in one of these games, the next optimisation moves it to MFG for Legacy Games at 2x.
- **What has been tested in a game:** in Final Fantasy VII Remake the add-on starts the program by itself, without launching from the app. A full session with this final build (generating, and changing the multiplier from the tab) has not been measured yet. Without a game, with a test image, the change from the tab's channel was tested: 2x, then 4x, then Auto, without restarting anything.

## What's new
- **Neural rendering look by default.** Optimising a game now writes a tested look for the neural pass (second pass with its own settings, detail stability always on, fine-tuned tone, detail and halo values). It is written at "Optimise game" and "Update all games"; what you change later in the in-game panel stays until the next optimisation.
- **Simpler texts.** Cards, help lines and dialogs say what each thing does for the player, without file names or engine variables. The technical detail is still there, folded under "Files in the game folder" and on the Health page.
- **"Launch game" starts the game the way its store does:** through Steam when it is a Steam game, through the game's protected launcher when it has one, otherwise the game's program. If the program asks for administrator rights, Windows shows its own prompt.
- **Nothing is written while the game is open.** "Optimise game" now refuses, like the other actions, and "Update all games" skips that game and says so. "Open" also counts the game's launcher or any other program running from the game folder, and the message names it.
- **Restore removes the files ReShade and the neural addon leave behind** (their logs and a settings backup), when they were created after the app started managing the game and the game had no ReShade of its own. The summary counts them and names the ones it leaves.
- **Auto multiplier:** what Auto writes is remembered with the game, so a multiplier you pick by hand is never mistaken for Auto's. If the in-game panel changes the multiplier you chose in the app, the game page says so.
- **Ray tracing options:** Ray Reconstruction and Hit Lighting say why they are pending; the Call of Duty option can be switched off when the settings file has conflicting lines.
- **Small windows:** the minimum window fits a 1920x1080 display at 150 % scaling, and no button or column is cut off at the minimum width.

## Fixes
- A game page no longer stays on "Reading…" when one card cannot read its state; that card says so and the rest of the page works.
- The activity log shows the same names as the game page (no internal values).
- "Quality (77%)" is no longer shown twice after changing the render resolution.

## Files

| File | Version | SHA-256 |
|---|---|---|
| `Ada4090Commander_v3.4.3_NGX310_Portable.zip` | — | `59bde06bc66fac507d6334b9f3d136637ffd44d6f64bab595b0171135ee2a9d2` |
| `mfgl_host.exe` | MFG for Legacy Games | `3b576aab44091d6fdc4660e9a3d8687438d0a4ec688a48aaf9929e60097feb76` |
| `ada4090-mfgl.addon64` | MFG for Legacy Games tab | `c408c30059799cd8c87c17803635c4838b87d2e93348624b773402352271b0c0` |
| `ada4090-sm89-tuner.addon64` | v3.4.2 | `d25c1af48c0aed5878373fd737ffc33af63528c1a27e9e1daa8fee0f13634682` |
| `renodx-mfgunlock.addon64` | v3.4.2 | `bf8b12fcd0ac4316cefa00eb99f5fdba3ee7a9f0cfc3770a712d43d5140a02eb` |
| `nvngx_dlssnr.dll` | 310.9.16.0 (custom, not signed by NVIDIA) | `9e731bce274065a475f725ae72bd030f9eb2ef83246b40e6ddf3972ec8305f53` |

## Known issues
- MFG for Legacy Games: when the game loses a frame, the image holds for one frame before continuing.
- MFG for Legacy Games: do not turn NVIDIA Smooth Motion on for the same game (in the NVIDIA app, or by optimising it with an older version of this app). Two frame generators at once make the game much slower.
- MFG for Legacy Games: after moving the app folder, optimise your games again. The game keeps the path of the helper program, and its NVIDIA driver profile is tied to the folder.
- MFG for Legacy Games: the tab has not been tried in games that are not DirectX 10, 11 or 12; there, exclusive full screen is only noticed after the helper program stops.
- In `Engine.ini`, a value you change by hand on a line the app manages is overwritten at the next optimisation.
- Tuner DLSS settings apply when the game creates DLSS, not instantly; DXR settings after a restart.
- The effect of the ray tracing bounces option depends on each game and has not been measured.
- Smooth Motion is 2x only.
- Do not use the pack in online games with anti-cheat. The app warns and does not block.

## Installation
1. Download `Ada4090Commander_v3.4.3_NGX310_Portable.zip`.
2. Extract it into a new folder you can write to.
3. Run `Ada4090Commander.exe`.
