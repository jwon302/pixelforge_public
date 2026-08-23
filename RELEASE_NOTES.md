# PixelForge 0.1.2 Release Notes

Date: 2026-08-23

## Added

- New node **Color Extract (Exp)** — an experimental palette extractor based on
  max-distortion PCA splitting (Orchard-Bouman) in Oklab.
  - Raising the color count never makes the result worse. The split objective is
    non-increasing in the color count, so detail no longer disappears when you
    increase the palette size.
  - Adjacent color counts share all but one color, so the palette stops
    reshuffling as you drag the size slider.
  - A large flat background can no longer dominate the palette, because a
    uniform region has almost no distortion left to split.
  - `Vivid` reserves palette slots for small but chromatic details (trim, eyes,
    ornaments) that pure error minimization always drops.
- Paste an image from the clipboard with `Ctrl+V` while the image view is
  focused. A confirmation dialog shows the incoming size before replacing the
  current image. Supports PNG clipboard data, DIB/DIBV5, and files copied from
  Explorer.

## Fixed

- GPU SLIC produced different results from the CPU path on images with
  transparency. The shader was missing the opacity gate, so removed-background
  pixels leaked color into superpixels along the subject silhouette.
- The GPU compute context was bound to a worker thread that never ran any
  pipeline work, so compute actually ran inside the UI rendering context. The
  context is now acquired only for the duration of each compute call, and the
  previous context is always restored.
- GPU failures were reported as success, so a failed dispatch produced a
  plausible but wrong image instead of falling back to the CPU path. GL errors
  are now checked and the CPU fallback runs.
- Shader compile and link error messages were truncated to nothing by an
  embedded NUL byte.
- SLIC output alpha was point-sampled from a smoothed cluster center, so a
  cluster containing no opaque pixels emitted its grid seed color as an opaque
  cell. Alpha now follows the actual coverage of the cluster.
- Background exclusion in Palette Extract dropped background tones from the
  palette entirely, so background pixels were remapped onto subject colors.
  Background pixels are now excluded from the palette computation only, and the
  background tones themselves are kept.

## Included

- `pixelforge.exe`
- `locales/ko.json`, `locales/en.json`
- `palettes/` (25 palettes) and `palettes.cache.json`
- `presets/` — default, Pixel Snap, Line Cleanup, PIA Portrait, water demos
- Required fonts under `third_party/fonts/`

## Verification

- `pixelforge.exe --selftest`: passed
- `pixelforge.exe --graphtest`: passed (43 checks)
- `pixelforge.exe --gputest`: passed
- Executable subsystem: Windows GUI
