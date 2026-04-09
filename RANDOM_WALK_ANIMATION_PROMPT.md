# Random Walk Header Animation Prompt

## What to build

A subtle, generative 2D random walk animation rendered on a `<canvas>` element that sits behind the header area of the main page (the title, byline, and whitespace above the lede). The animation is decorative — like a watermark or a paper texture. It should feel mathematical and calm, not flashy.

## Behavior

- On page load, a single particle begins a 2D random walk from a random starting position within the header bounds.
- At each step, it moves a small fixed distance in a random direction (continuous angles, not grid-locked — this should look like Brownian motion, not a maze).
- The path is drawn as a continuous thin line. The line persists — you see the full trail, not just the current position.
- The walk draws slowly — maybe 3-5 steps per frame at 60fps, so you can watch it wander if you stare, but it doesn't demand attention.
- The walk continues indefinitely while the page is open. After ~30-60 seconds the header should have a nice organic tangle of path.
- If the walk hits the edge of the header bounds, it wraps or reflects gently (no hard stops).

## Visual treatment

- Line color: very faint — something like `rgba(0, 0, 0, 0.06)` on the warm off-white background, or a muted warm tone like `rgba(180, 160, 140, 0.12)`. It should be barely visible, like pencil on cream paper.
- Line width: 1px, no anti-aliasing tricks. Thin and precise.
- No dots at the current position. No trail fade. No glow. Just the line.
- The canvas fills the entire header area and sits behind all text (z-index below the title, byline, etc). Text remains fully readable — the line is so faint it's like looking at text printed on lightly textured paper.
- Background of the canvas is transparent — the page's warm off-white (#f8f5f0 or similar) shows through.

## What NOT to do

- No color changes or gradients along the path
- No multiple particles
- No pulsing, glowing, or animated endpoints
- No interaction (no mouse tracking, no hover effects)
- No 3D perspective
- No grid lines or axes
- Nothing that looks like a screensaver or a tech demo
- No fade-in on page load — the walk just starts immediately, quietly

## Technical notes

- Use a `<canvas>` element positioned absolutely behind the header content
- Size the canvas to match the header dimensions (including the whitespace above and below the title)
- On window resize, resize the canvas accordingly
- Keep the animation lightweight — this should use negligible CPU
- The step size should be small enough that the path looks smooth but large enough that it actually covers ground over 30-60 seconds. Something like 2-3px per step.

## The test

If someone opens the page and reads the title and lede without noticing the animation, and then 30 seconds later glances up and sees a beautiful tangled line behind the title and thinks "oh, that's a random walk" — the implementation is correct. If they notice it immediately, it's too prominent. If they never notice it, it's too faint.
