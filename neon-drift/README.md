# Neon Drift

| | |
| --- | --- |
| **Model** | 256K Context - llama.cpp - RTX 5090 |
| **Date** | 2026-08-19 |
| **Status** | Playable |
| **File** | [neon-drift.html](neon-drift.html) |

## Working Prompt

Build a single-file HTML5 canvas game called **Neon Drift** — an endless
neon-styled platformer with procedurally generated levels.

**Concept:** A glowing diamond drifts rightward through an infinite,
hue-shifting neon world, jumping gaps and dodging hazards as far as possible.

**Genre & core loop:** Endless side-scrolling platformer. Move right, jump
gaps, collect sparks, avoid spikes and enemies, hit checkpoints, and keep going
as the difficulty ramps. There is no end — the goal is distance.

**Aesthetic:**
- Dark near-black background (`#03010a`) with a cyan/magenta neon palette.
- Everything glows (canvas `shadowBlur`); colors continuously hue-shift over time.
- CRT overlay: scanlines + radial vignette (CSS, `mix-blend-mode: multiply`).
- Background: parallax grid + a rotating geometric mandala; expanding rings
  appear as intensity rises.
- **Terrain shift:** a movement-driven parallax effect. The background grid,
  mandala, and a layered terrain silhouette at the bottom stay flat when the
  player is idle and bank up/down with horizontal velocity (eased, frame-rate
  independent), so the world visibly tilts with your movement and settles back
  to flat when you stop.
- Camera: subtle tilt with velocity, slow zoom-in with progress, and
  full-screen "strobe" flashes.
- Audio: fully procedural Web Audio synth (no samples) at 110 BPM — sawtooth
  bass, sine kick, square hats, triangle pad, and a square lead that enters as
  intensity rises. Mute toggle.

**Controls:** `A`/`D` or `←`/`→` to move, `Space`/`↑`/`W` to jump (with double
jump), `R` to restart, `M` to mute. Coyote time and jump buffering for feel.

**Mechanics:**
- Gravity, capped fall speed, ground + air control.
- Double jump (2 jumps); an "overdrive" powerup grants a 3rd jump for 12s.
- Solid platforms (full collision) and one-way floating platforms (land from
  above only).
- Horizontally oscillating moving platforms that carry the player.
- Spikes (instant death) and patrolling triangular enemies (stomp to kill,
  touch from the side to die).
- **Shooter turrets** — stationary spiky enemies that aim and fire homing
  bullets at the player when in range (~640px, and only when the player is to
  their left). Bullets travel in a straight line toward where the player was
  when fired; a bullet hit is instant death. Shooters are stompable like other
  enemies. They appear in hazard and overdrive chunks. Visually a red spiked
  ball (sharp radiating spikes + pulsing core) so they read as a threat, not a
  collectible.
- Sparks (collectibles, +score) and star powerups (overdrive).
- Checkpoints: respawn point on death; the most recent one is active.
- **Death screen:** on death the game pauses on a stats screen (distance,
  sparks, score, best) and does **not** auto-respawn. The player must press any
  key or click to respawn at the last checkpoint. `R` restarts the whole run.

**Progression (procedural):**
- Levels are generated from seeded RNG chunks appended ahead of the player and
  culled behind (constant memory, endless).
- Chunk archetypes: warmup gaps, floating drift, spike/enemy hazards, moving
  platforms, stairs, overdrive gauntlet, tight gauntlet.
- A difficulty curve (0→1 over ~700 tiles) widens gaps, adds more platforms,
  and speeds up enemies.
- A strobe screen-flash every ~200 tiles.
- Every gap must be clearable with the jump arc (single ≈ 7 tiles, double ≈ 14).

**Scope:**
- In: endless procedural platformer, the systems above, persistent best
  distance (`localStorage`), death → stats screen → manual checkpoint respawn.
- Out: no multiplayer, no full run-state save, no image assets (all
  vector-drawn), no build step.

**Constraints:**
- One self-contained `.html` file. Vanilla JS + Canvas 2D + Web Audio. No
  external libraries, no network requests, no build step. Runs by opening the
  file in a browser.

**Success criteria:**
- Runs with zero console errors; generates and streams levels indefinitely.
- Feels responsive (coyote time, buffered jumps, capped fall).
- Difficulty clearly ramps; death pauses on the stats screen and respawns at
  the last checkpoint on input; best distance persists across reloads.

## Notes

- Built from a raw idea ("make procedurally generated levels to keep playing
  on") and refactored into the working prompt above.
- Converted the original hand-built level into seeded chunk generation with a
  difficulty ramp and streaming/culling.
- Verified in browser: generates, plays, dies, respawns at checkpoint, and
  saves best distance. 0 console errors.
- Added **shooter turrets** (2026-08-19): stationary spiky enemies that fire
  straight-line bullets at the player in range. Verified in browser — shooters
  spawn, fire, bullets kill on contact, and shooters are stompable. 0 console
  errors. First drawn as a diamond it read as a collectible, so it was
  redesigned as a red spiked ball to read as a threat.
- Changed death to **pause on the stats screen** (2026-08-19): removed the
  auto-respawn timer; the player now presses any key or clicks to respawn at
  the last checkpoint. Verified in browser — stays on the death screen until
  input, then respawns. 0 console errors.
- Added **terrain shift** (2026-08-19): a movement-driven parallax effect where
  the background grid, mandala, and a layered bottom terrain silhouette stay
  flat when idle and bank up/down with horizontal velocity. Verified the shift
  value eases 0 → +44 (right) → −40 (left) → 0 (release) with 0 console errors;
  feel/visuals confirmed by the player.