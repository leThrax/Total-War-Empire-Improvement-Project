# Empire Patch

**Fixes, performance and graphics upgrades for _Empire: Total War_**

![Version](https://img.shields.io/badge/version-0.9.0--beta-orange)
![Game](https://img.shields.io/badge/Empire%3A%20Total%20War-Steam%20v1.5.0-8b0000)
![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-blue)
![Requires](https://img.shields.io/badge/requires-DXVK%20(included)-green)
![Discord](https://img.shields.io/discord/1560935812110098492?link=https%3A%2F%2Fdiscord.com%2Finvite%2Fgb272tA58n)

Join the Discord Server: https://img.shields.io/discord/1560935812110098492?link=https%3A%2F%2Fdiscord.com%2Finvite%2Fgb272tA58n

Empire Patch changes the game while it runs: `Empire.exe` and the game's data files are not modified, and no game
files are included. Most settings can be changed in the game, in a **Patch Options** menu in the game's own style.

> [!WARNING]
> **This is a beta.** It has been tested on one PC (Windows 11, NVIDIA RTX 3080, 2560×1440).
> Please [report](#reporting-problems) what works and what doesn't on your setup.

**[⬇ Download the latest release](../../releases/latest)**

---

## Contents
- [Features](#features)
- [Requirements](#requirements)
- [Install](#install)
- [Settings](#settings)
- [Uninstall](#uninstall)
- [Multiplayer](#multiplayer)
- [Linux / Steam Deck](#linux--steam-deck)
- [Known issues](#known-issues)
- [Reporting problems](#reporting-problems)

---

## Features

### 🔧 Fixes
| | |
|---|---|
| **Battle speed** | The battle AI always runs in the background. Before, with a still camera above 1x speed, the frame rate fell to about 15 fps. |
| **No lag spikes** | At maximum battle speed the simulation catch-up per frame is capped. |
| **Fast alt-tab** | Returning to a battle no longer freezes for ~7 seconds while all unit sprites are rebuilt. |
| **Resolution change** | No more crash when changing the resolution (DXVK on NVIDIA). |
| **UI scaling** | Above 1280×960 the game drew its menus and HUD in a small box. The UI now scales with the screen (Auto) or by a fixed factor, with sharp text instead of stretched letters. |
| **Main menu** | The background fills 16:9 and other screens instead of leaving black bars. |
| **Refresh rate** | Fullscreen uses your monitor's highest refresh rate (Windows sometimes picked a lower one). |
| **Frame limiter** | The main menu no longer renders thousands of frames per second (60 fps), plus an optional limit for the campaign and battles. |
| **Microphone** | The game no longer sets your Windows microphone level to 100% at every start. |
| **Unit shadows** | Shadows are no longer cut off for the soldiers nearest to the camera. |
| **Memory** | Less memory use with DXVK on PCs with both a graphics card and an Intel iGPU. |
| **Crash logging** | A crash writes its location to `empire_patch.log` and a dump to `crashes\`. |

### ⚡ Performance
- **Faster campaign end turn:** AI turns run 8× faster (single player, see [Multiplayer](#multiplayer)).
- **Faster battle loading:** about twice as fast in big battles, and faster sea battle loading.

### 🎨 Graphics
- **Shadows:** sharper (shadow map up to 8192), soft edges, darker, longer range.
- **Ambient occlusion** on the ambient light only (no grey veil over the image), and grass shading.
- **Water:** reflections at full resolution, with less distortion.
- **Anti-aliasing** for grass and tree foliage, and cleaner edges against the sky.
- **Draw distances:** grass drawn further, soldiers stay 3D models further before they turn into sprites.
- **Typeface:** the game's text in Libre Caslon Text, a classic serif that stays sharp at every size.
- **Optional:** highlight roll-off, bloom, exposure, vibrance, sea ripple distance, campaign terrain detail
  (see `empire_patch.ini`).

---

## Requirements
- **Empire: Total War, Steam version** (v1.5.0, the current Steam build). Other versions are not supported: parts of
  the patch that don't find their code switch themselves off.
- **Windows 10 or 11.**
- **A graphics card with Vulkan support** and a recent driver, for DXVK (included):

  | Vendor | Supported |
  |---|---|
  | NVIDIA | GeForce GTX 900 series or newer |
  | AMD | Radeon RX 400 series or newer |
  | Intel | 6th generation Core (Skylake) or newer |

  The recommended graphics settings are made for a card with **4 GB or more**.

> [!IMPORTANT]
> **DXVK is required** (`d3d9.dll`, included in the download). Without it the patch switches itself off and
> tells you so at startup.

---

## Install
1. **Open the game folder:** in Steam, right-click *Empire: Total War* → *Manage* → *Browse local files*.
   It's the folder with `Empire.exe` in it.
2. **Extract all files** from the archive into that folder:

   | File | |
   |---|---|
   | `version.dll` | loads the patch (Windows loads it with the game) |
   | `empire_patch.dll` | the patch |
   | `empire_patch.ini` | the settings |
   | `d3d9.dll` | DXVK {DXVK_VERSION} (Direct3D 9 on Vulkan) |
   | `empire_patch_fonts\` | the font Libre Caslon Text and the tool that makes the game's fonts from it |
   | `README.txt`, `CHANGELOG.txt`, `LICENSE.txt`, `THIRD-PARTY-NOTICES.txt` | |

   If you already use DXVK, you can keep your own `d3d9.dll`.
3. **Start the game.** The first start (and the first campaign and battle) take longer once: the shaders are
   compiled again and the fonts are made (about 5 seconds before the game window appears).

**Updating:** extract the new version over the old one. If you changed settings, keep your `empire_patch.ini`
(new settings then use their defaults until you add them).

---

## Settings
In the game:
- **Campaign and battle:** `Esc` → *Options* → **Patch Options**
- **Main menu:** *Options* → **Patch Options** (also a tab on the options screen)

The recommended values are marked **(Recommended)**, and **Reset to defaults** sets them. Settings marked `*`
apply after restarting the game.

Everything else is in `empire_patch.ini`, a text file where each setting is explained.

---

## Uninstall
Delete from the game folder:
- `version.dll`, `empire_patch.dll`, `empire_patch.ini` and the folder `empire_patch_fonts`
- the folder `data\font\custom` (the generated fonts)
- `d3d9.dll`, if you didn't use DXVK before

The patch also writes `empire_patch.log` and crash dumps in `crashes\`, and DXVK writes `Empire_d3d9.log` and
`*.dxvk-cache`. These can be deleted too.

---

## Multiplayer
**Not tested.** Several fixes change the battle and campaign simulation, so all players should use the **same
patch version and the same `empire_patch.ini`**.

For multiplayer campaigns set **End turn speed** to *Off* (`AiTurnSpeed=1`): it only works when every player's
game speeds up.

---

## Linux / Steam Deck
**Untested.** Proton already uses DXVK. Wine must be told to load the patch's `version.dll`, with these Steam
launch options:

```
WINEDLLOVERRIDES="version=n,b" %command%
```

---

## Known issues
- **Only tested on NVIDIA.** On AMD and Intel, soft shadows and vegetation anti-aliasing may do nothing, because
  the game uses other shader paths there.
- **Without DXVK** (the system Direct3D 9) the patch doesn't work and switches itself off.
- **Unit sprite distance: Never (3D only)** costs a lot of frame rate in big battles.
- **The fort defence AI improvements are not included yet** (they need a rewrite).

---

## Reporting problems
Please [open an issue](../../issues) and attach:
- **For a crash:** the newest `.dmp` and `.log` file pair from the `crashes` folder in the game folder (the patch
  saves them at every crash and keeps the last 5).
- **Otherwise:** `empire_patch.log` from the game folder. It's written again at every start, so copy it right after
  the problem.

Describe your PC (graphics card, resolution) and what you did.

<details>
<summary><b>Privacy: what's in these files</b></summary>

A crash dump contains part of the game's memory at the moment of the crash. Besides the game's own data this can
include your Windows user name (in file paths) and your PC's name. The log lists your graphics card, screen
resolution and the game folder path. Nothing is sent anywhere automatically: you decide what you attach.
</details>

---

## Licence
Free to use; redistribution only as the unmodified release archive. See [LICENSE.txt](LICENSE.txt), and
[THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt) for DXVK, MinHook and Libre Caslon Text.

<sub>Empire Patch is a free fan project. It is not made, endorsed or supported by Creative Assembly or SEGA.
Empire: Total War, Total War and their logos are trademarks of their owners. Use at your own risk; keep a backup of
your save games.</sub>
