# Radar Page — Lava Lamp Header Animation Prompt

## What to build

A subtle, generative lava lamp animation rendered on a `<canvas>` element that sits behind the header area of the Radar page. Same role as the random walk line on the Atlas page — decorative, ambient, barely visible. It represents pre-formation: things that haven't crystallized into direction yet. Anomalies drifting, merging, splitting.

## Behavior

- On page load, 5-7 soft blobs begin drifting slowly within the header bounds.
- Each blob is an organic, rounded shape — not a circle, not a rectangle. Use metaball / implicit surface math or layered radial gradients with slight deformation over time. They should feel liquid, not geometric.
- Blobs drift in slow, lazy paths. No sudden movements. Think actual lava lamp speed — you watch for a few seconds and barely see movement, then you look away and look back and everything has shifted.
- When two blobs drift close to each other, they merge smoothly into one larger blob (metaball-style surface tension). When a merged blob drifts apart, it splits back into two. This merging/splitting is continuous and gentle.
- Blobs that hit the header edge reflect softly or wrap. No hard stops.
- The animation runs indefinitely. After 30-60 seconds the header should have a calm, slowly evolving field of organic shapes.

## Visual treatment

- Blob color: extremely faint. Something like `rgba(200, 180, 160, 0.04)` or `rgba(180, 160, 140, 0.05)` — warm, barely perceptible on white. Like looking at paper with very slight watermarks.
- No outlines, no borders. Pure soft gradient fills that blend into the background.
- No color variation between blobs. All the same faint warm tone.
- The canvas fills the entire header area and sits behind all text (z-index below the title). Text remains fully readable — the blobs are so faint they're like looking at text on slightly uneven paper.
- Background of the canvas is transparent — the page's white background shows through.

## What NOT to do

- No bright colors or saturated tones
- No sharp edges or geometric shapes
- No fast movement or bouncing
- No particle effects, sparkles, or trails
- No interactivity (no mouse tracking, no hover effects)
- No pulsing or breathing effects
- No outlined or stroked shapes — only soft fills
- Nothing that looks like a screensaver or a tech demo
- Nothing that references an actual lava lamp product (no container shape, no base, no cap)

## Technical notes

- Use a `<canvas>` element positioned absolutely behind the header content
- Metaball approach: render a scalar field from multiple point sources, threshold at a value that produces soft organic edges. Apply a very faint fill to the thresholded region. OR: use multiple overlapping radial gradients with positions that drift over time — simpler and may achieve the same visual result.
- Size the canvas to match the header dimensions
- On window resize, resize the canvas accordingly
- Keep the animation lightweight — requestAnimationFrame at a low effective framerate (15-20fps is fine, the movement is so slow it doesn't need 60fps)
- Blob drift speed: very slow. Maybe 0.2-0.5px per frame. The viewer should have to stare for several seconds to confirm movement.

## The test

Same test as the Atlas random walk animation: if someone opens the page and reads the title without noticing the animation, and then later glances up and sees soft, slowly evolving shapes behind the title and thinks "huh, that's nice" — the implementation is correct. If they notice it immediately, it's too prominent. If it looks like a lava lamp product or a tech demo, it's too literal. It should feel like the page itself is subtly alive.
