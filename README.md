# Experiments

A collection of small, self-contained test games and experiments. Each game lives in its own folder and runs by opening the HTML file directly in a browser — no build step, no dependencies.

## Games

| Game | Folder | Description |
| --- | --- | --- |
| **Neon Drift** | [`neon-glow-platformer/`](neon-glow-platformer/) | Endless neon platformer with procedurally generated levels, checkpoints, and a persistent best-distance score. |

### Neon Drift

- **Play:** open [`neon-glow-platformer/Neon Glow - Platformer.html`](neon-glow-platformer/Neon Glow - Platformer.html) in any modern browser.
- **Controls:** `A`/`D` or arrow keys to move, `Space` to jump / double-jump, `R` to restart, `M` to mute.
- **How it works:** levels are generated from seeded chunks (gaps, spikes, patrolling enemies, moving platforms, stairs, overdrive gauntlets) with a difficulty ramp. Chunks stream in ahead of the player and are culled behind, so the run is endless. Best distance is saved to `localStorage`.

## Adding a new experiment

1. Create a new folder at the top level (e.g. `my-new-game/`).
2. Drop the game files in it.
3. Add a row to the table above.