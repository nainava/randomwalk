# Finder Page — Lattice Random Walk Header Animation Prompt

## What to build

A subtle lattice random walk animation rendered on a `<canvas>` element behind the Finder page header. Multiple random walks on a grid, moving in cardinal directions (up/down/left/right), each in a different faint color. Where two walks share the same grid cell, there's a visible intersection marker. This represents field crossings — separate paths of knowledge colliding on shared ground.

## Behavior

- On page load, 3-5 random walks begin simultaneously from different starting positions on an invisible grid.
- Each walk moves one grid cell per step, in a random cardinal direction (up, down, left, right — no diagonals). This is a classic lattice random walk.
- Each walk draws at its own pace — staggered slightly so they don't all step in sync. Maybe 1-3 steps per second per walk. Slow enough to watch if you stare.
- The path persists — you see the full trail for each walk, not just the current position.
- Each walk has its own faint color (see visual treatment below).
- When two walks occupy the same grid cell (or their paths cross through the same cell), a small dot or subtle mark appears at that intersection point. This is the key visual — the crossing. It should be slightly more visible than the paths themselves.
- The grid itself is NOT drawn. No gridlines. The walks imply the grid through their orthogonal movement. The background is clean.
- Walks continue indefinitely. After 30-60 seconds, there should be several tangled paths with a few intersection points visible.
- If a walk reaches the header edge, it reflects (turns around) or wraps.

## Visual treatment

- Each walk's path: very faint, different hue. Think `rgba(180, 80, 80, 0.08)`, `rgba(80, 180, 160, 0.08)`, `rgba(160, 140, 60, 0.08)`, `rgba(120, 80, 180, 0.08)`. Barely visible individually — like colored pencil on white paper viewed from across a room.
- Path width: 3-4px (slightly thicker than the Atlas line, because these are grid-aligned and need to read as distinct tracks).
- Grid cell size: roughly 20-30px. Large enough that the orthogonal steps are clearly visible, small enough that the walks cover meaningful ground.
- Current position of each walk: a small dot at the head of each path, same color as the path but slightly more opaque (maybe 0.15 alpha). No glow, no pulse.
- Intersection markers: where two different walks share the same grid cell, place a small filled circle (5-6px diameter) at that cell center. Color: darker than either path — maybe `rgba(0, 0, 0, 0.12)` or a blend. These should be the most visible element in the animation, but still subtle.
- No grid lines drawn. The grid is invisible. Only the walks and their intersections are rendered.
- Canvas background is transparent — white page shows through.

## What NOT to do

- No visible grid lines or dots at grid intersections (only at walk intersections)
- No arrows or direction indicators on the paths
- No animation of the intersection markers (no pulse, no glow, no grow-in)
- No labels or text
- No interactivity
- No trail fade or opacity decay along the path
- Nothing that looks like a game, a maze, or a circuit board
- Don't make it look exactly like the Wikipedia diagram — no thick saturated lines. Same concept, much fainter execution

## Technical notes

- Use `<canvas>` positioned absolutely behind the header content
- Track each walk's position and full path history
- Check for intersections by maintaining a grid-cell occupancy map: when walk N enters a cell already visited by walk M, mark it as an intersection
- Size canvas to header dimensions, resize on window resize
- requestAnimationFrame but only step walks every ~300-500ms (1-3 steps/second). The walks should feel deliberate, not frantic
- Grid doesn't need to align to anything — just pick an origin point and cell size and let the walks go

## The test

Same subtlety standard as Atlas and Radar: if someone reads the Finder title and lede without noticing the animation, and then later sees faint colored paths crossing on a grid behind the text with small dots where they meet, and thinks "oh — paths crossing, that's what the Finder does" — the implementation is correct. The intersections should be the thing that catches the eye, not the paths themselves.
