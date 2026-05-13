# Upstream Provenance

This plugin is derived from the ImageJ 1.x standard Brightness/Contrast
implementation.

- Upstream repository: https://github.com/imagej/ImageJ
- Upstream file: `ij/plugin/frame/ContrastAdjuster.java`
- Upstream commit: `d6bfee69e43b80bc551b1175930c2712e7a573a3`
- Upstream permalink: https://github.com/imagej/ImageJ/blob/d6bfee69e43b80bc551b1175930c2712e7a573a3/ij/plugin/frame/ContrastAdjuster.java
- Local upstream snapshot: `official-source/ContrastAdjuster.java`
- Retrieved from: `https://raw.githubusercontent.com/imagej/ImageJ/master/ij/plugin/frame/ContrastAdjuster.java`
- Retrieved date: 2026-05-13

This repository is not a GitHub fork of `imagej/ImageJ`. It is an independent
ImageJ/Fiji plugin project that carries a local copy of the upstream source file
for traceability.

## Local Changes

The forked implementation is:

- `src/main/java/ij/plugin/frame/ChannelStackContrastAdjuster.java`

The main behavioral change is that histogram and display-range statistics are
computed from all Z/T planes in the current channel, rather than only the
currently displayed plane.

The affected standard Brightness/Contrast behaviors are:

- initial default min/max range
- histogram display
- Auto range
- Reset range

Additional integration changes:

- The plugin registers as an `ImageListener` because ImageJ 1.x directly calls
  the standard `ij.plugin.frame.ContrastAdjuster.update()` from some slice
  change paths. An independent plugin does not receive that hardcoded callback.
- Channel stack statistics are cached for unchanged image/channel conditions to
  avoid rescanning all Z/T planes on every slider update.
- The plugin uses ImageJ's built-in `ContrastPlot` and `TrimmedLabel` helper
  classes instead of bundling forked copies, to avoid package-level class
  collisions with Fiji/ImageJ.

## License Notes

ImageJ 1.x is described by the ImageJ project as public domain software. The
ImageJ licensing notes also mention jurisdictional and contributor-status caveats
for ImageJ 1.x as a whole. This repository preserves the upstream source snapshot
and records the derivation path so downstream users can inspect the original
source and licensing context.
