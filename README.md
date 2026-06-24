# slicard

A slick, configurable CSS card with a bright animated edge and a soft outer bloom.
**Pure CSS. Zero JavaScript. One `<div>`.**

Drop a single `.slicard` element into any page and tune it with CSS custom
properties — radii, hue, gradient angle, edge speed, outer glow. No framework,
no build step, no runtime dependencies.

```html
<div class="slicard"></div>
```

---

## Demo

Open [`index.html`](./index.html) in a browser. It ships with:

- A **hero** with a tilted, floating card and annotations.
- **Chapter 01 — Radii:** four independent corner radii.
- **Chapter 02 — Tones:** six preset palettes + custom picker.
- **Chapter 03 — Glow Edge:** the rotating conic-gradient ring.
- **Chapter 04 — Outer Glow:** the soft bloom that bleeds past the border.
- **Chapter 05 — Export:** copy a standalone block of CSS.
- A **playground:** drag to resize, drag corners to set radii, tweak hue and
  animation, then copy the generated CSS.

No server needed — just open the file.

---

## Configuration

Every knob is a CSS custom property on the `.slicard` element. Defaults are
defined on `.slicard` itself; override any of them inline or in a stylesheet.

### Size & shape

| Property            | Default | Description                                                    |
| ------------------- | ------- | ------------------------------------------------------------- |
| `--sc-w`            | `380px` | Card width.                                                   |
| `--sc-h`            | `250px` | Card height.                                                  |
| `--sc-radius`       | `34px`  | Radius for all four corners (used by the per-corner values). |
| `--sc-radius-tl`    | `--sc-radius` | Top-left radius.                                        |
| `--sc-radius-tr`    | `--sc-radius` | Top-right radius.                                       |
| `--sc-radius-br`    | `--sc-radius` | Bottom-right radius.                                    |
| `--sc-radius-bl`    | `--sc-radius` | Bottom-left radius.                                     |
| `--sc-pad`          | auto    | Content padding. Auto-grows with the largest corner radius.  |

### Color

| Property         | Default | Description                                                              |
| ---------------- | ------- | ----------------------------------------------------------------------- |
| `--sc-hue`       | `206`   | HSL hue (0–360). Drives fill, edge, and bloom together.                 |
| `--sc-sat`       | `55%`   | HSL saturation.                                                         |
| `--sc-light`     | `40%`   | HSL lightness. The card lightens/darkens from here.                     |
| `--sc-grad-angle`| `158deg`| Direction of the internal fill gradient.                               |
| `--sc-fill-1`    | derived | Top gradient stop (`hsl(hue sat (light + 13%))` by default).            |
| `--sc-fill-2`    | derived | Bottom gradient stop (`hsl(hue (sat - 8%) (light - 15%))` by default).  |

### Edge

| Property             | Default | Description                                                  |
| -------------------- | ------- | ----------------------------------------------------------- |
| `--sc-border-width`  | `1.6px` | Thickness of the rotating ring.                             |
| `--sc-border-speed`  | `6s`    | Period of one full rotation.                                |
| `--sc-border-glow`   | `0.7`   | Intensity of the edge's drop-shadow (0 disables).          |
| `--sc-edge-base`     | derived | Base color of the bright arc.                              |
| `--sc-edge-peak`     | derived | Peak (brightest) color of the arc.                         |

### Outer glow

| Property             | Default | Description                                                  |
| -------------------- | ------- | ----------------------------------------------------------- |
| `--sc-glow-strength` | `0.55`  | Strength of the outer bloom (0 = flat, 1.0 = heavy).        |
| `--sc-glow-color`    | derived | Color of the outer glow.                                    |

### Example

```html
<div class="slicard"
     style="--sc-w: 320px; --sc-h: 200px;
            --sc-radius: 28px;
            --sc-hue: 268; --sc-sat: 45%; --sc-light: 40%;
            --sc-border-speed: 4s;
            --sc-glow-strength: 0.7;">
</div>
```

---

## Preset palettes

| Name        | Hue  |
| ----------- | ---- |
| Azure       | 206  |
| Terracotta  | 18   |
| Ember       | 8    |
| Violet      | 268  |
| Teal        | 182  |
| Moss        | 140  |

---

## Disabling the animation

Set `data-anim="off"` on the element to remove the rotating ring and keep only
the static top-center highlight:

```html
<div class="slicard" data-anim="off"></div>
```

The animation also automatically pauses for users with
`prefers-reduced-motion: reduce`.

---

## Browser support

Works in evergreen browsers (Chrome, Edge, Firefox, Safari). Relies on:

- `@property` for animating a CSS angle (the rotating edge).
- `conic-gradient` for the ring.
- `mask-composite: exclude` / `-webkit-mask-composite: xor` to clip the ring to
  the border.
- `backdrop-filter` (in the playground UI only, not the card itself).

In browsers without `@property` support, the card still renders — the edge just
won't rotate.

---

## Project structure

```
.
└── index.html   # the entire site — markup, CSS, and the playground JS
```

The `.slicard` class is inlined near the bottom of `<style>`. To extract it,
copy everything between the `/* slicard */` comment and the closing `</style>`
into its own `.css` file.

---

## License

MIT.
