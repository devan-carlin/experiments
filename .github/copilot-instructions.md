# Copilot Instructions — AI Game Benchmark

This repo is a benchmark of **AI-generated games**. Each game is built from a
**working prompt** — a comprehensive, self-contained spec that a model can take
and build the game from. The working prompt is the canonical artifact that gets
committed to git; raw conversation is not.

## What this repo is

- A collection of small, self-contained test games (single-file HTML, no build
  step, no dependencies, no network).
- Each game records which model built it, the working prompt used, and notes.
- Purpose: compare model capabilities by giving a model a well-specified prompt
  and seeing what it builds. The working prompt is the controlled variable.

## Repo layout

- One folder per game (kebab-case, **no date suffix** — git tracks dates).
- Each game folder contains:
  - The game files (e.g. `<game-name>.html`, or `index.html` if multi-file).
  - `README.md` — metadata + the working prompt + notes.
- Top-level `README.md` — index table of all games.
- This file (`.github/copilot-instructions.md`) — the project system prompt.

## The working prompt

A working prompt is the comprehensive spec a model builds from. When the user
gives a raw idea, **refactor it into a working prompt before building.** Write
it as a prompt you could hand to a model to reproduce the game.

A working prompt has these sections:

1. **Concept** — one-line description.
2. **Genre & core loop** — the fundamental gameplay cycle.
3. **Aesthetic** — visual and audio direction.
4. **Controls** — input scheme.
5. **Mechanics** — detailed gameplay systems.
6. **Progression** — difficulty scaling / endless behavior.
7. **Scope** — what's in and out.
8. **Constraints** — technical limits (single-file HTML, no deps, etc.).
9. **Success criteria** — what "done" and "good" look like.

The working prompt is the **source of truth** and a **living document**. Build
the game to match it. As the project evolves — new features, refactors, bug
fixes, changed mechanics — **update the working prompt in the game's
`README.md` to reflect the game's current state.** The prompt should always
describe what the game
*does now*, not what it originally did. If the build reveals the prompt was
missing something, add it. If a feature is removed or changed, revise the
prompt to match.

Treat the working prompt as the canonical context for the project: it is what
a model (or a human) needs to understand and continue the game. Keep it
current so it stays a faithful, self-contained description of the game as it
exists today.

## Conventions
README.md`** per game:
  - Metadata table: Model (exact name), Date, Status, File link.
  - The full working prompt.
  - Notes: what worked, what didn't, how it was verified.
- **Top-level Notes: what worked, what didn't, how it was verified.
- **`README.md`** index table: `Game | Model | Date | Status`.
- **Commit trailer**: end the commit body with
  `Generated-with: <exact model name>` for a git-native audit trail.
- **Model name**: record the exact model string (e.g.
  `256K Context - llama.cpp - RTX 5090`), never a vague label.

## Workflow

**Initial build:**

1. User gives a raw idea.
2. Refactor it into a working prompt (all 9 sections).
3. Confirm the working prompt with the user.
4. Build the game to match the working prompt.
5. Verify it runs (open in browser, check for console errors).
6. Write the game's `README.md` (metadata + working prompt + notes).
7. Update the top-level `README.md` index.
8. Commit with the `Generated-with:` trailer and push.

**Ongoing work (features, refactors, fixes):**

1. Make the change to the game.
2. Verify it runs (open in browser, check for console errors).
3. **Update the working prompt in the game's `README.md`** so it reflects the
   game's current state — this is required, not optional.
4. Add a note to the game's `README.md` describing the change.
5. Commit with the `Generated-with:` trailer and push.