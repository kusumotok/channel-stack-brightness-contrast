# Channel Stack Brightness/Contrast

This ImageJ/Fiji plugin is based on ImageJ 1.x `ij.plugin.frame.ContrastAdjuster`.
It keeps the standard Brightness/Contrast UI but computes the histogram, Auto
range, Reset range, and default slider range from all Z/T planes in the current
channel instead of only the current plane.

The upstream source used as the base is stored in
`official-source/ContrastAdjuster.java`. See `UPSTREAM.md` for provenance and
license notes.

## Behavior

For multi-stack and hyperstack images, this plugin aggregates statistics from
the currently selected channel across all Z slices and T frames. It does not
aggregate across other channels.

The channel-wide statistics are used for:

- initial default min/max range
- histogram display
- Auto range
- Reset range

The plugin listens for ImageJ image update events so it follows channel changes
made through the hyperstack channel slider or mouse wheel. Expensive channel
stack statistics are cached while the active image, channel, stack size, bit
depth, and histogram range are unchanged.

It appears in Fiji/ImageJ as:

```text
Plugins > Adjust > Channel Stack Brightness/Contrast
```

## Requirements

- Fiji/ImageJ with ImageJ 1.x
- Maven
- JDK 8 or newer for compiling this plugin

Build:

```sh
mvn -q package
```

The plugin JAR is created at:

```text
target/channel-stack-brightness-contrast.jar
```

Install by placing the JAR in Fiji's `plugins/` directory and restarting Fiji.

## License

This project is intended to be distributed on the same public-domain basis as
ImageJ 1.x. See `LICENSE`, `NOTICE.md`, and `UPSTREAM.md`.
