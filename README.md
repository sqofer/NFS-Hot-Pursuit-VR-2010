# NFS Hot Pursuit VR 0.7.5

A ready-to-install OpenXR VR mod for the **original Steam Need for Speed Hot Pursuit (2010), executable version 1.0.5.0s**. This package includes the branded installer, English launcher, VR icon and logo, runtime files, removal tool, source code and third-party notices.

## Install and play

1. Extract the entire archive. Close the game and VR launcher.
2. Run **Setup.exe**. It reads Steam's libraries and selects the game folder. Use **Browse** if necessary.
3. Click **Install VR mod**. Leave the desktop shortcut option enabled. Missing Visual C++ components can be installed through the Microsoft components option.
4. Start your VR runtime and put on the headset. Open **NFS Hot Pursuit VR** from the desktop.
5. Click **OPEN MOD** on the welcome page. Select your per-eye resolution, then click **Save and launch**. The game starts through Steam.

Install once. Use the desktop shortcut for subsequent launches. Run Setup again for an update; existing VR settings are preserved. Keep the archive available for removal or reinstalling.

## Welcome page

Every launcher opening starts with the supplied thank-you page. **OPEN MOD** opens the settings page; it does not launch the game or save settings. **STEAM** and **META QUEST** open these links in your default browser:

- [CYBRID on Steam](https://store.steampowered.com/app/1636850/CYBRID/)
- [CYBRID on Meta Quest](https://www.meta.com/en-gb/experiences/cybrid/24008454042113681/)

The button-free image is embedded as the background. Working native buttons use the supplied reference skins, so no special font or external image files are required. Buttons support mouse, Tab, Enter and Space. The welcome page does not appear in Setup or headless removal.

## Compatibility

- 64-bit Windows 10 or 11, Steam, the original supported game build and a working OpenXR headset/runtime.
- Uses the active OpenXR runtime; no Pimax-specific runtime is required. Race rendering has been checked with SteamVR and Pimax 8KX. Other headset/runtime combinations still need their own validation.
- Native D3D9 stereo: both eyes are drawn from the same source frame, with headset view projections and head tracking. No alternating-eye rendering (AFR).
- The game remains x86; a bundled x64 host handles OpenXR and optional OFXR frame generation. Ready images travel through shared GPU resources.
- The installer checks the supported executable SHA-256 before changing files. The Remastered edition and other executables are unsupported.
- An existing foreign `d3d9.dll` is not overwritten. Remove conflicting injectors through their own installation tools first.

Microsoft Visual C++ v14 x86 and x64 runtimes are required. Setup opens without them, checks their installed versions and can fetch missing components from the [official Microsoft download links](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Windows may request administrator permission for Microsoft component installation. Restart Windows if Setup reports that a restart is needed.

## Settings and controls

The initial resolution is **1600 × 1800 per eye**, independently of the monitor. Presets range from 1280 × 1440 to 3840 × 4320; custom sizes are available. The launcher reports runtime limits. Higher resolutions increase rendering cost; change settings with the game closed, then restart it.

Menus and pre-race screens use a flat panel. Stereo activates when the engine enters the actual race. The race HUD is a central transparent panel shared between eyes; its **closer / farther** slider controls distance.

| Control | Action |
| --- | --- |
| Ctrl or F10 | Recenter the headset |
| F9 | Enable or disable VR |
| P / semicolon | Move the camera forward / back |
| L / apostrophe | Move left / right |
| O / K | Move up / down |
| + / −, including keypad | Tilt forward / back |

Camera movement requires **Adjust the internal camera position** and the hood/bumper camera. Keys correspond to the displayed physical keyboard positions; no Alt modifier is required. The initial camera offset is an adjustable starting point, rather than a detected driver-head anchor. Movement starts at 0.15% of a 1 metre/second reference speed. Offsets and pitch are saved.

The launcher also controls near clipping, the nearby driver-head/hair/glasses filter, and windshield visibility. **Hide windshields on all cars** changes the known vehicle files and affects both VR and the monitor. Close the game before saving this change. It supports 118 recognized stock/hidden vehicle files; unknown car modifications disable the switch instead of being overwritten.

**OFXR frame generation** is optional and enabled by default. It uses the bundled official OFXR Bridge 0.2.12.2, enabled privately for this mod's host. Try disabling it if your runtime or GPU has problems with it. The OFXR FPS overlay is off. No separate FPS unlocker, DLSS or FSR upscaler is bundled; the game's original FPS limit remains unless changed separately.

## Removal and recovery

Close the game and launcher, then run **Uninstall.cmd**. It finds the game or asks for the folder, restores recognized windshield files, removes the owned mod files and its desktop shortcut, and preserves the game executable and unrelated files. Unknown vehicle files are left unchanged.

Updates and removal save backups in `NFSHP_OpenXR_Backups` inside the game folder. The installer refuses altered owned binaries instead of silently replacing them. Preserve any modified files before recovering an installation. Empty mod directories may remain after removal.

For a custom folder or unattended installation:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\Install-Mod.ps1 -GamePath "D:\Games\Hot Pursuit" -CreateShortcut -InstallDependencies -NonInteractive
```

`Ready-To-Copy` contains the payload. Use Setup rather than copying it over an existing mod installation: Setup performs ownership checks, makes backups and preserves settings.

## Troubleshooting

If the headset is blank, start the runtime, ensure it is the active OpenXR runtime, put on the headset, and restart the game through the launcher with **Enable OpenXR on launch** checked. Start with the fixed 1600 × 1800 preset. Try frame generation off if the problem remains.

For low performance, reduce per-eye resolution and compare OFXR on/off in the same race. Performance depends on CPU draw submission, GPU, runtime and selected resolution; frame generation does not remove every bottleneck. This release preserves the previously working 0.7.1 GPU renderer and host. It does not enable the D3D9On12 diagnostic mode.

If installation fails, Setup shows the error and its log path. Check that the game and launcher are closed, the executable is supported, and the folder is writable.

## Source and validation

`Source` contains the mod's source and installer scripts, the official OFXR release source, and pinned dependency source/notices. See `Source/BUILDING.md`. Original mod code is provided under the MIT license; third-party components retain their own terms, including OFXR's LGPL-3.0-or-later license.

`Validation` records installation, update, rollback, removal, branding and settings checks. These ran in separate test folders, including Unicode Steam-library paths. Removal restored all 118 recognized vehicle files to their exact original hashes. This package has not been race-tested on every other computer or headset. `SHA256SUMS.txt` lists package checksums. No game executable, personal camera profile or captured gameplay logs are included.
