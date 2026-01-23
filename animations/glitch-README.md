# Glitch Animation for Niri

A clean digital glitch effect with chromatic aberration and CRT scanlines. Windows open and close with RGB channel splitting.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `split` | `0.04` | RGB channel separation intensity (0.02-0.08) |
| `0.08` in scanline | `0.08` | Scanline visibility (0.05-0.15) |
| `uv.y * 400.0` | `400.0` | Scanline density (200-600) |

## Customization

### RGB Split Intensity

Find this line in both shaders:
```glsl
float split = glitch * 0.04;  // or progress * 0.04
```
- `0.02` - Subtle, barely noticeable
- `0.04` - Default
- `0.08` - Strong chromatic aberration

### Scanline Strength

```glsl
float scanline = 1.0 - 0.08 + 0.08 * sin(uv.y * 400.0);
```
The two `0.08` values control visibility. Set both to `0.0` to disable scanlines entirely.

### Scanline Density

Change `400.0` to adjust how many scanlines appear:
- `200.0` - Fewer, thicker lines
- `400.0` - Default
- `600.0` - More, finer lines

## Config Tool

For easier customization without editing GLSL, check out [burn-shader](https://github.com/rocklobstr/burn-shader) - a config-driven generator with TOML config file.
