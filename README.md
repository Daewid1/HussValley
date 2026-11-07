# Huss Valley

Huss Valley with the original Giorgio/Lumen interface, animated background, opening film, and four-film viewer.

## Run in Potassium

```lua
local response = request({Url = "https://raw.githubusercontent.com/Daewid1/HussValley/main/Loader.lua", Method = "GET"})
assert(response.StatusCode == 200, "Huss Valley loader download failed")
local run, failure = loadstring(response.Body, "=HussValleyLoader")
assert(run, failure)
run()
```

The first run installs about **1.21 GB** of runtime and media files. Keep Roblox open while the installer runs; minimize its progress window if needed. Downloads use the executor `request` function. Failed or interrupted installs resume on rerun. SHA-256 checks cover the manifest, each download part, and each installed file, including the runtime before execution. Valid cached files are reused.

The installer now prioritizes the edit media. Playback begins as soon as verified frames have decoded, while the rest of the collection continues downloading. It holds the last frame when buffering, loops available edits, and advances as the next edit arrives. Audio starts muted; choose **UNMUTE EDITS** to enable it. Minimizing pauses playback, not downloads. Completion or failure stops the film and audio. Executors without custom-asset playback still install normally. The signed media release and its existing download cache remain unchanged.

Files install only to `HussValley.lua` and `HussValley/ui/giorgio/`. Existing `HussValley/configs` preferences are untouched. No GitHub token is needed by the public loader. Keep tokens and passwords out of scripts.

Click **Giorgio Armani?** in the header to open the original film viewer: play/pause, stop, next film, seek, volume, drag, and resize. The compact keybind HUD and Huss Valley features remain available.

The checked-in `Loader.lua` pins release `v1.0.0`; it verifies release content against the pinned manifest before execution. `HussValley.lua` is the full source. Running it directly does not download the films; use the loader for first installation.

## Verification

```powershell
py -3.13 tools/verify_distribution.py
```

The fixture suite requires the Luau CLI. Set the `LUAU` environment variable if it is not on PATH. It covers fresh and interrupted installation, cache reuse, corrupt downloads/writes, path traversal rejection, progress/minimize behavior, binary hash compatibility, and configuration preservation.

## Release rebuild

```powershell
py -3.13 tools/package_release.py --runtime HussValley.lua --assets PATH_TO_AUTHORIZED_ASSETS --output .releases/vNEXT --version vNEXT --manifest-url https://github.com/Daewid1/HussValley/releases/download/vNEXT/manifest.json
```

The asset directory must include the licensed icons, sounds, brand files, and complete `media/` frame/audio directories from the authorized Giorgio installation. Upload all generated chunks, manifest, and configured `Loader.lua` to a new immutable GitHub release. Copy the configured loader to the repository root only after its release assets are ready. Release binaries are not stored in Git history.

## Credits and permissions

- Giorgio/Lumen interface and installer/packager: Copyright 2026 upio, MIT; see `licenses/Giorgio-MIT.txt`.
- Animated line-md icons: Vjacheslav Trushkin, MIT; see `licenses/line-md-MIT.txt`.
- Kenney interface sounds: CC0; see `licenses/kenney-CC0.txt`.
- Artxmpl audio logo: CC BY 4.0, https://www.patreon.com/artxmpl; see `licenses/artxmpl-CC-BY-4.0.txt`.
- Armani names/logos remain trademarks of their owners. Film, audio, background, and branding assets retain their respective third-party rights; no MIT license is asserted over them. The repository owner confirmed permission to redistribute the supplied media.
