# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

HTML game prototype: a lab rat escapes a dark cardboard maze with a flashlight strapped to its back. All the code lives in `index.html` (inline CSS and JS, no dependencies, no build step). The only external resources are the Google Fonts fonts (Permanent Marker, Special Elite), with fallbacks. `concept/` holds the reference concept art (top-down view, cardboard walls with a corrugated edge, white rat with a harness) and the game doesn't load it.

The UI, the code comments and the README are in Spanish (Rioplatense, with voseo: "presioná", "escapaste"). Keep that tone.

## Run and test

There are no commands for building, linting or running tests. You open `index.html` in a browser, and with the built-in browser pane that's `preview_start` with `url: file:///C:/Claude/Laberinto/index.html`.

Quirks of the browser pane that affect testing:
- The page loads as a `data:` snapshot, so after each edit you have to navigate to the URL again.
- `requestAnimationFrame` is heavily throttled there, so simulated keypresses barely move the rat. To test logic, call the global functions directly from `javascript_tool`. Top-level `const` and `function` declarations are reachable from there. For example, `keys['arrowup']=true; for(...) update(1/60); render();`.
- `loadLevel(n)`, `startPlay()`, `resetRun()` and `castRays(x,y)` let you set up any situation. Setting `G.light=1` and calling `render()` gives you a lit frame for a screenshot.
- The canvas can be 0×0 when the page loads, so `resize()` keeps it at least 1 px. In `frame()`, `requestAnimationFrame` is scheduled before `update`/`render` so that an exception doesn't kill the loop.

## Script architecture (`index.html`)

**Tunable constants** at the top: `C` (cell size, 64 world units), `T` (wall thickness), `K` (apparent wall height), speeds, `LIGHT_R`/`CONE` (flashlight), `RAYS`. Progression comes from `SIZES`/`sizeFor(n)` (maze columns×rows), `viewCells(n)` (how many cells across fit on screen, i.e. the zoom, which gets closer with each level) and `timeFor(n, pathCells)` (time limit from the shortest path length).

**Maze** (`genMaze`): recursive backtracker on a W×H grid. Walls are stored as `hW[r][c]` (top wall of row r) and `vW[c][r]` (left wall of column c). The entrance is always on the right side (`entRow`) and the exit on the left (`exitRow`). From level 2 on, some walls are removed to create cycles. Everything is seeded with `mulberry32(G.baseSeed + n*7919)`. "Retry the same level" relies on not regenerating: `resetRun()` only repositions the rat and resets the timer.

**Geometry** (`buildRects`): walls are turned into rectangles (collinear runs merged, plus a start pen outside the entrance). That single list `G.rects` is used for collision (circle vs rectangle, two circles: body and head), for ray casting, and for drawing. `buildDeco` adds purely visual elements: sheet seams, floor tape and pencil marks, which work as landmarks.

**Rendering pipeline** (`render`). This is the core of the visual look and needs care when you touch it:
1. Fully lit scene: floor (`drawFloor`, using a tiled texture pattern) on the main canvas, and walls (`drawWalls`) on `wallCv`. For the 3D effect, each wall's top face is the base rectangle scaled by `(1+K)` around the camera, and only the side faces facing the camera are drawn.
2. Light map: `castRays` fires `RAYS` rays from the flashlight against the wall edges (all axis-aligned) and gets a visibility polygon. On `aCv` the beam sprite (`coneCv`, generated pixel by pixel at startup) is drawn, clipped with `destination-in` to that polygon. That's the floor light. On `bCv` the same beam is clipped to a polygon extended by `T+6` (plus its version projected by `(1+K)`) and to the shape of `wallCv`, so the top faces and sides of the walls get lit. Both are added (`lighter`) into `lightCv` over black.
3. `multiply` of `lightCv` over the scene: anything without light stays fully black. "Total darkness" is a design decision: lit areas are not remembered.
4. The rat (`drawMouse`, procedural) and the lens glow are drawn after the darkness, so they're always faintly visible.

**States** (`G.state`): `title` → `intro` → `play` ⇄ `paused` → `won` | `dying` → `lost`. The cards are HTML (`#card`), and the HUD (level, timer) is DOM over the canvas. When time runs out, the light flickers and goes out (`dying`) and you go back to the start of the same maze. The camera (`camTarget`) follows the rat with some lookahead and is clamped to the maze edges when the maze is larger than the screen.

**Sound** (`Snd`): all synthesized with WebAudio (oscillators and filtered noise, no files). `Snd.init()` runs on the first keypress because of the browsers' autoplay policy.

## Git / GitHub

Remote `git@github.com:PabloForconi/raton-laberinto.git` (private). The repo has `core.sshCommand` configured locally to use the `~/.ssh/DesktopPablo` key, so pushing over SSH works from the console.
