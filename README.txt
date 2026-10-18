EMPIRE PATCH {VERSION}  -  fixes and graphics upgrades for Empire: Total War
==============================================================================

This is a BETA. It has been tested on one PC (Windows 11, NVIDIA RTX 3080, 2560x1440).
Please report what works and what doesn't on other setups (see "Reporting problems").

Empire Patch changes the game while it runs. Empire.exe and the game's data files are not
modified, and no game files are included.


REQUIREMENTS
------------
- Empire: Total War, Steam version (v1.5.0, the current Steam build). Other versions are not
  supported: parts of the patch that don't find their code switch themselves off.
- Windows 10 or 11.
- A graphics card with Vulkan support and a recent driver, for DXVK (included):
  NVIDIA GeForce GTX 900 series or newer, AMD Radeon RX 400 series or newer, Intel 6th generation
  Core (Skylake) or newer. The recommended graphics settings are made for a card with 4 GB or more.
- DXVK is required. Without it the patch switches itself off and tells you so at startup.


INSTALL
-------
1. Open the game folder: in Steam, right-click Empire: Total War > Manage > Browse local files.
   It is the folder with Empire.exe in it.
2. Extract ALL files from this archive into that folder:
     version.dll          loads the patch (Windows loads it with the game)
     empire_patch.dll     the patch
     empire_patch.ini     the settings
     d3d9.dll             DXVK {DXVK_VERSION} (Direct3D 9 on Vulkan)
     empire_patch_fonts   the font Libre Caslon Text and the tool that makes the game's fonts from it
     README.txt, CHANGELOG.txt, LICENSE.txt, THIRD-PARTY-NOTICES.txt
   If you already use DXVK, you can keep your own d3d9.dll.
3. Start the game. The first start (and the first campaign and battle) take longer once, because
   the shaders are compiled again and the fonts are made (about 5 seconds before the game window).

Updating: extract the new version over the old one. If you changed settings, keep your
empire_patch.ini (new settings then use their defaults until you add them).


UNINSTALL
---------
Delete version.dll, empire_patch.dll, empire_patch.ini and the folder empire_patch_fonts from the
game folder, the folder data\font\custom (the generated fonts), and d3d9.dll if you didn't use
DXVK before. The patch also writes empire_patch.log, crash dumps in the
crashes folder and DXVK writes Empire_d3d9.log / *.dxvk-cache: these can be deleted too.


SETTINGS
--------
In the game: Esc > Options > Patch Options (campaign and battle), or in the main menu
Options > Patch Options. The recommended values are marked "(Recommended)", and
"Reset to defaults" sets them. Settings marked * apply after restarting the game.

Everything else is in empire_patch.ini (a text file, each setting is explained there).


WHAT IT DOES
------------
Fixes
- Battles at higher speed: the battle AI always runs in the background. Before, with a still
  camera above 1x speed, the frame rate fell to about 15 fps.
- No lag spikes at maximum battle speed (the simulation catch-up per frame is capped).
- Fast alt-tab: returning to a battle no longer freezes for ~7 seconds while all unit sprites
  are rebuilt.
- No crash when changing the resolution (DXVK on NVIDIA).
- UI scaling: above 1280x960 the game drew its menus and HUD in a small box. The UI now scales
  with the screen (Auto) or by a fixed factor, with sharp text instead of stretched letters.
- The main menu background fills 16:9 and other screens instead of leaving black bars.
- Fullscreen uses your monitor's highest refresh rate (Windows sometimes picked a lower one).
- Frame limiter: the main menu no longer renders thousands of frames per second (60 fps), and
  an optional limit for the campaign and battles.
- The game no longer sets your Windows microphone level to 100% at every start.
- Faster campaign end turn: AI turns run 8x faster (single player; see Multiplayer).
- Faster battle loading (about twice as fast in big battles) and faster sea battle loading.
- Unit shadows are no longer cut off for the soldiers nearest to the camera.
- Less memory use with DXVK on PCs with both a graphics card and an Intel iGPU.
- Crash logging: a crash writes its location to empire_patch.log and a dump to crashes\.

Graphics
- Sharper shadows (shadow map up to 8192), soft shadow edges, darker shadows, longer range.
- Ambient occlusion on the ambient light only (no grey veil over the image), grass shading.
- Water reflections at full resolution, with less distortion.
- Anti-aliasing for grass and tree foliage, and cleaner anti-aliased edges against the sky.
- Grass drawn further, soldiers drawn as 3D models further before they turn into sprites.
- A new typeface for the game's text, Libre Caslon Text (Font = Game restores the original).
- Optional: highlight roll-off, bloom, exposure, vibrance, sea ripple distance, campaign
  terrain detail (see empire_patch.ini).


MULTIPLAYER
-----------
Not tested. Several fixes change the battle and campaign simulation, so all players should use
the same patch version and the same empire_patch.ini. For multiplayer campaigns set
"End turn speed" to Off (AiTurnSpeed=1): it only works when every player's game speeds up.


LINUX / STEAM DECK (untested)
-----------------------------
Proton already uses DXVK. Wine must be told to load the patch's version.dll, with these Steam
launch options:
    WINEDLLOVERRIDES="version=n,b" %command%


KNOWN ISSUES
------------
- Only tested on NVIDIA. On AMD and Intel, soft shadows and vegetation anti-aliasing may do
  nothing, because the game uses other shader paths there.
- Without DXVK (the system Direct3D 9) the patch doesn't work and switches itself off.
- "Unit sprite distance: Never (3D only)" costs a lot of frame rate in big battles.
- The fort defence AI improvements are not included yet (they need a rewrite).


REPORTING PROBLEMS
------------------
Please open an issue on the GitHub page of Empire Patch and attach:
- for a crash: the newest .dmp and .log file pair from the crashes folder in the game folder
  (the patch saves them at every crash and keeps the last 5),
- otherwise: empire_patch.log from the game folder (written again at every start, so copy it
  right after the problem).
Describe your PC (graphics card, resolution) and what you did.

Privacy: a crash dump contains part of the game's memory at the moment of the crash. Besides
the game's own data this can include your Windows user name (in file paths) and your PC's
name. The log lists your graphics card, screen resolution and the game folder path. Nothing
is sent anywhere automatically: you decide what you attach.


DISCLAIMER
----------
Empire Patch is a free fan project. It is not made, endorsed or supported by Creative Assembly
or SEGA. Empire: Total War, Total War and their logos are trademarks of their owners. Use at
your own risk; keep a backup of your save games.
