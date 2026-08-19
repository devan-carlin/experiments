# Experiments — AI Game Benchmark

A collection of **AI-generated test games**. Each game is built from a
**working prompt** — a comprehensive, self-contained spec that a model can take
and build the game from. The working prompt is the canonical artifact committed
here; raw conversation is not.

The purpose is to compare model capabilities: give a model a well-specified
prompt and see what it builds. The working prompt is the controlled variable.

Every game is self-contained (single-file HTML, no build step, no
dependencies) and runs by opening the HTML file directly in a browser.

## Games

| Game | Model | Date | Status |
| --- | --- | --- | --- |
| [Neon Drift](neon-drift/) | 256K Context - llama.cpp - RTX 5090 | 2026-08-19 | Playable |

Each game folder contains the game files plus a `README.md` with the full
working prompt, exact model, and build notes.

## How a game gets added

1. A raw idea is refactored into a **working prompt** (see
   [.github/copilot-instructions.md](.github/copilot-instructions.md) for the
   9-section format).
2. A model builds the game to match the working prompt.
3. The game is verified in a browser (zero console errors).
4. The game's `README.md` is written and the index above is updated.
5. Committed with a `Generated-with: <model>` trailer and pushed.

## Structure

```
test-projects/
├── README.md                  ← this index
├── .github/copilot-instructions.md
└── <game-name>/               ← kebab-case, no date suffix
    ├── README.md              ← metadata + working prompt + notes
    └── <game-name>.html       ← the game (index.html if multi-file)
```

## Conventions

- One folder per game (kebab-case, no date suffix — git tracks dates).
- `README.md` per game: metadata + working prompt + notes.
- Exact model name recorded, never a vague label.
- Commit trailer: `Generated-with: <exact model name>`.