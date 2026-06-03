# PixelForge 0.1.1 Release Notes

Date: 2026-06-03

## Changed

- Animated GIF inputs now save back as animated GIF results instead of only static PNG output.
- Animation processing now caches each processed frame, so changing frames or saving can reuse already processed results.
- During full animation processing, playback stops and a blocking progress overlay is shown.
- Graph edits that do not affect the connected Output path no longer invalidate all animation frame caches.
- Palette Extract now supports animated inputs with a fixed-frame option:
  - When the source is an animation, enable `Fixed Frame` and enter a frame number to extract colors only from that frame.
  - When the source is a static image, this option is hidden.
- The animation FPS field is placed on the right side of the animation frame strip.
- The release executable is built as a Windows GUI app, so launching it does not open a terminal window.

## Included

- `pixelforge.exe`
- `locales/ko.json`, `locales/en.json`
- `palettes/` and `palettes.cache.json`
- `presets/preset.pfgraph`
- Required fonts under `third_party/fonts/`

## Verification

- `pixelforge.exe --selftest`: passed
- `pixelforge.exe --graphtest`: passed
- Executable subsystem: Windows GUI
