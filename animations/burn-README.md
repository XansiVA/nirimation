# Burn Animation on close/open of windows in Niri

A burn/dissolve effect where windows burn away from the edges inward with a glowing ember line.

## Variants

- **burn.kdl** - Classic orange/yellow fire glowy look
- **burn-multicolor.kdl** - Randomly picks from 8 colors per window (inspired by World of Warcraft mogs :)

## Customizing Colors

Colors are defined as RGB vec3 values (0.0 to 1.0). Each color has two parts:
- `ember_inner` - The bright core of the burn line
- `ember_outer` - The glow/fade around it

### Single Color (burn.kdl)

Find these lines in both `window-open` and `window-close` shaders:

```glsl
vec3 ember_inner = vec3(1.0, 0.3, 0.0);  // RGB for inner glow
vec3 ember_outer = vec3(1.0, 0.8, 0.2);  // RGB for outer glow
```

### Example Colors

| Color      | ember_inner              | ember_outer              |
|------------|--------------------------|--------------------------|
| Orange     | `vec3(1.0, 0.3, 0.0)`    | `vec3(1.0, 0.8, 0.2)`    |
| Blue       | `vec3(0.2, 0.4, 1.0)`    | `vec3(0.5, 0.8, 1.0)`    |
| Purple     | `vec3(0.6, 0.1, 0.9)`    | `vec3(0.9, 0.5, 1.0)`    |
| Green      | `vec3(0.1, 0.8, 0.2)`    | `vec3(0.5, 1.0, 0.3)`    |
| Pink       | `vec3(1.0, 0.1, 0.4)`    | `vec3(1.0, 0.5, 0.7)`    |
| Cyan       | `vec3(0.0, 0.8, 0.9)`    | `vec3(0.7, 1.0, 1.0)`    |
| Gold       | `vec3(0.9, 0.7, 0.1)`    | `vec3(1.0, 1.0, 0.8)`    |
| Deep Red   | `vec3(0.8, 0.2, 0.1)`    | `vec3(1.0, 0.5, 0.2)`    |

### Multicolor (burn-multicolor.kdl)

To change which colors are in the random pool, edit the `get_ember_colors` function. Each color is assigned a range of the random seed (0.0 to 1.0)

To use only 2 colors (50/50 chance):
```glsl
if (seed < 0.5) {
    inner = vec3(0.2, 0.4, 1.0);   // blue
    outer = vec3(0.5, 0.8, 1.0);
} else {
    inner = vec3(0.6, 0.1, 0.9);   // purple
    outer = vec3(0.9, 0.5, 1.0);
}
```

## Other Tweaks

- `duration-ms 500` - Animation speed (lower = faster)
- `noise(uv * 8.0 ...)` - Change `8.0` for coarser/finer burn edges
- `threshold * 0.8` - Change `0.8` to control how far the burn reaches
- `0.08` (ember width) - Increase for a wider glow line
