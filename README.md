# 🧊 CubeLab

A fully interactive **3D Rubik's Cube simulator** in a single self-contained HTML file — no libraries, no frameworks, no CDNs, no build step. Pure HTML + CSS + vanilla JavaScript, with the whole cube rendered on one `<canvas>`.

**▶ Live demo: [vcruz305.github.io/cubelab](https://vcruz305.github.io/cubelab/)**

> ⚡ **Built in 2 hours using the new Qwen4 Max Preview** (`qwen4-max-preview`).

---

## Features

- **Real 3D cube** — perspective-projected cubies with rounded stickers, per-face lighting and depth sorting, drawn on a single canvas.
- **Standard color scheme** — white ↔ yellow, green ↔ blue, red ↔ orange.
- **Smooth face turns** — eased 90°/180° rotations driven by an animation queue.
- **Full interaction** — drag the background to orbit, drag a sticker to turn that layer, or use the keyboard.
- **Scramble · Solve · Undo · Reset** — one click each.
- **Built-in solver** — a layer-by-layer (beginner method) solver that genuinely solves any scramble, with a guaranteed history-reversal fallback.
- **Live move notation** — current move, full history chips, move counter, and a solved badge.
- **Responsive** — clean layout on desktop and mobile.

## Controls

| Input | Action |
|---|---|
| Drag background | Orbit the whole cube |
| Drag a sticker | Turn that face/layer |
| `U D L R F B` | Turn a face (clockwise) |
| `Shift` + key | Turn counter-clockwise (`'`) |
| `Space` | Scramble |
| `Ctrl/⌘ + Z` | Undo |

Buttons: **Scramble**, **Solve**, **Undo**, **Reset**.

## The solver

The Solve button runs a classic beginner / layer-by-layer method on a copy of the cube state, then animates the resulting moves:

1. Daisy → bottom cross
2. Bottom-layer corners
3. Middle-layer edges
4. Last-layer cross (edge orientation)
5. Last-layer corner orientation
6. Last-layer corner + edge permutation

It's not move-optimal — it's the reliable, human-readable method — and adjacent same-face turns are merged/cancelled before playback. If the solver ever fails, it falls back to reversing your full move history, so **Solve always returns you to a solved cube.**

## Run it

It's one file. Either open it directly:

```
open index.html        # macOS
# or just double-click index.html in any modern browser
```

…or use the hosted version: **[vcruz305.github.io/cubelab](https://vcruz305.github.io/cubelab/)**.

No server, no dependencies, no internet required once loaded.

## Tech notes

- **State:** 26 cubies, each with a position, an orientation matrix, and colored stickers. Moves are `{axis, layer, quarter-turns}` applied as exact integer rotations — no floating-point drift, no illegal states.
- **Rendering:** painter's-algorithm depth sort of body + sticker polygons, backface culling, and a directional light for shading.
- **Verified:** engine invariants (move⁴ = identity, move + inverse = identity, sticker conservation) and the solver across hundreds of random scrambles.

---

<sub>Single-file vanilla JS · canvas rendering · layer-by-layer solver · built in 2 hours with Qwen4 Max Preview.</sub>