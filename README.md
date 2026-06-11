# Magnum

A Claude Code plugin that turns Claude into an **orchestrator**: it decomposes a task, picks the right model and effort level for each piece of work, and delegates everything to freshly spawned subagents instead of implementing things itself.

## Skills

### `orchestrate`

Decomposes a task into sequential **atomic phases**, each split into parallel **subtasks** (capped by `max-subagents`). For each subtask it selects a model, an effort level, and a name from the active profile, then spawns a dedicated subagent to do the work. The orchestrator never edits deliverables or runs task commands itself — it plans, briefs, spawns, and reviews.

### `swap-profile`

Switches the active model profile (`currently-selected-profile` in `.config/index.json`).

## Configuration

- `.config/index.json` — active profile name and `max-subagents` (max parallel subtasks per phase)
- `.config/profiles/<profile>/models.json` — available models, display names, colors, and effort-level ranges
- `.config/profiles/<profile>/model-guide.md` — model selection criteria, per-model effort mapping, and invocation details

## Status

Early and experimental (`v0.1.0`). The configuration format and the orchestrator's subagent-spawning mechanism are still evolving.
